# Task 2 - Hello World for RTOS

## Deskripsi Projek
Proyek ini merupakan pengenalan awal untuk penggunaan RTOS (Real-Time Operating System) pada mikrokontroler STM32. Tujuannya adalah untuk memahami cara kerja RTOS dengan membuat beberapa task yang memiliki prioritas berbeda. Setiap task menjalankan fungsinya masing-masing, seperti membaca tombol, mengendalikan LED, membaca nilai dari ADC, dan berkomunikasi melalui UART.

Proyek ini menggunakan STM32 untuk:
- **pickButtonTask**: Mendeteksi input dari tombol fisik dan menampilkan status tombol melalui UART.
- **getADCTask**: Membaca nilai ADC dan memberikan data ke task lain.
- **dispLEDTask**: Mengontrol LED berdasarkan nilai ADC.
- **dispUARTTask**: Berinteraksi dengan pengguna melalui UART, menampilkan menu, dan memproses input.

![rtos_task diagram](https://github.com/user-attachments/assets/33d9a5e2-b3fc-4c24-8a00-f5e6ab444e35)

## Foto Hardware
![foto hardware task 2](https://github.com/user-attachments/assets/9c4259d6-ec8d-46e1-8ea5-fbfb56483c3b)

## Short Video Hardware
s
