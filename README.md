# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)
 
- **Diva Sakananda (3222600013)**
- **Billy Lukito Danuharja (3222600027)**

# Task 2 - Hello World for RTOS

## Deskripsi Projek
Proyek ini merupakan pengenalan awal untuk penggunaan RTOS (Real-Time Operating System) pada mikrokontroler STM32. Tujuannya adalah untuk memahami cara kerja RTOS dengan membuat beberapa task yang memiliki prioritas berbeda. Setiap task menjalankan fungsinya masing-masing, seperti membaca tombol, mengendalikan LED, membaca nilai dari ADC, dan berkomunikasi melalui UART.

Proyek ini menggunakan STM32 untuk:
- **pickButtonTask**: Mendeteksi input dari tombol fisik dan menampilkan status tombol melalui UART.
- **getADCTask**: Membaca nilai ADC dan memberikan data ke task lain.
- **dispLEDTask**: Mengontrol LED berdasarkan nilai ADC.
- **dispUARTTask**: Berinteraksi dengan pengguna melalui UART, menampilkan menu, dan memproses input.

![rtos_task diagram](https://github.com/user-attachments/assets/33d9a5e2-b3fc-4c24-8a00-f5e6ab444e35)

1. pickButtonTask (Prioritas: Normal) 
- Task ini terhubung dengan `dispUARTTask`. Jika tombol ditekan, 
‘button1_pressed’ akan muncul pada serial monitor, dan pada `dispUARTTask`, 
variabel ini akan diperiksa untuk menampilkan nilai ADC melalui UART. 
- Karena fungsi tombol tidak kritis dalam hal kecepatan dan hanya melibatkan 
debounce, maka prioritas normal cukup untuk task ini. 
2. getADCTask (Prioritas: Above Normal) 
- Nilai `x_val` yang dihasilkan oleh task ini digunakan oleh `dispLEDTask` untuk 
menentukan kondisi LED, serta digunakan oleh `dispUARTTask` untuk 
mengirimkan data melalui UART ketika tombol ditekan. 
- Task ini diberi prioritas lebih tinggi karena proses pembacaan sensor ADC penting 
dan harus lebih cepat daripada fungsi lainnya untuk menjaga akurasi data sensor 
yang digunakan oleh task lain. Misalnya, LED harus diatur berdasarkan nilai ADC, 
dan jika pembacaan ADC terlambat, respons sistem terhadap perubahan kondisi 
lingkungan juga akan terlambat. Dengan demikian, pembacaan ADC harus 
mendapat prioritas lebih tinggi. 
3. dispLEDTask (Prioritas: Normal) 
- Jika `override_led_control` diaktifkan melalui uart, semua LED akan dimatikan. 
Jika tidak aktif, task ini akan menyalakan atau mematikan LED sesuai dengan 
rentang nilai ADC: 
- Task ini bergantung pada nilai ADC yang diperoleh dari `getADCTask`. Tanpa nilai 
ADC yang terbaru, task ini tidak dapat mengatur LED dengan benar. Selain itu, 
`override_led_control` dapat diaktifkan oleh `dispUARTTask` saat menerima input 
dari pengguna melalui UART. 
- Meskipun mengendalikan LED penting, ini tidak mendesak dibandingkan dengan 
pembacaan sensor ADC, sehingga prioritas normal sudah cukup. Kontrol LED 
hanya bereaksi berdasarkan pembacaan sensor, jadi responsnya bisa sedikit lebih 
lambat tanpa mempengaruhi keseluruhan fungsi sistem. 
4. dispUARTTask (Prioritas: Normal) 
- Task ini berhubungan dengan `dispLEDTask` melalui `override_led_control`. 
Ketika pengguna memilih opsi untuk mematikan LED, `dispLEDTask` akan 
merespons dengan mematikan LED. 
- Task ini berhubungan dengan `pickButtonTask`. Jika tombol fisik ditekan, task ini 
akan mengirimkan nilai ADC melalui UART. 
- Mengirimkan data melalui UART dan menampilkan menu merupakan tugas yang 
tidak mendesak, sehingga prioritas normal sudah cukup. Fungsi komunikasi ini 
tidak berpengaruh besar pada respons sistem terhadap perubahan kondisi 
lingkungan. 

Hubungan Antara Task : 
- getADCTask: Task ini mengambil nilai dari ADC dan menyediakan informasi ke task 
lain, seperti `dispLEDTask` (untuk kontrol LED) dan `dispUARTTask` (untuk 
menampilkan nilai ADC). 
- pickButtonTask: Task ini memonitor tombol fisik dan berhubungan dengan 
`dispUARTTask`, yang akan menampilkan nilai ADC ketika tombol ditekan. 
dipengaruhi 
- dispLEDTask: Task ini mengandalkan nilai dari `getADCTask` untuk mengontrol LED, 
serta 
oleh 
`override_led_control`. 
`dispUARTTask` 
yang 
dapat 
mengaktifkan 
- dispUARTTask: Task ini menampilkan menu dan menerima input dari pengguna, yang 
akan mempengaruhi fungsi LED dan menampilkan nilai ADC jika tombol ditekan.

## Foto Hardware
![foto hardware task 2](https://github.com/user-attachments/assets/9c4259d6-ec8d-46e1-8ea5-fbfb56483c3b)

## Short Video Hardware

https://github.com/user-attachments/assets/44bb5adc-e802-4848-826e-1fee36dd8c6a


