## About Package

Simple Laravel app with RabbitMQ implementation.

## Requirements

- PHP 7.2
- Laravel 5.5
- Akun CloudAMQP (RabbitMQ Server). [Daftar disini](https://cloudamqp.com)

## Installation

1. Clone Repository menjadi dua project. Satu akan bertindak sebagai publisher dan lainnya sebagai subscriber.
```bash
# Sebagai Publisher
git clone git@github.com:fendi-idn/laravel-rabbitmq.git rabbitmq-publisher.idntimes.com/

# Sebagai Subscriber
git clone git@github.com:fendi-idn/laravel-rabbitmq.git rabbitmq-subscriber.idntimes.com/
```

2. Copy `.env` dari file `.env.example` untuk repo publisher & subscriber. Dan atur kredensial RabbitMQ. Untuk konfigurasi bisa melihat di video berikut.
    - https://www.loom.com/share/044a3c87a3d84b278b752feb0627c0a9
```bash
cp .env.example .env
```

3. Install package
```bash
composer install
```

4. Generate application key
```bash
php artisan key:generate
```

5. Khusus repo subscriber (`rabbitmq-subscriber.idntimes.com`), un-comment pada file `app/Jobs/PingJob.php` line `33`. Ini berfungsi sebagai penanda ketika subscriber menerima request dari RabbitMQ.
```php
public function handle()
{
    // Uncomment this code bellow, if you're a subscriber / consumer
    echo 'Ping Event Received!' . PHP_EOL;
}
```

6. Pada repo subscriber (`rabbitmq-subscriber.idntimes.com`) jalankan perintah berikut untuk listen queue.
```bash
php artisan queue:work
```

7. Pada repo publisher (`rabbitmq-publisher.idntimes.com`) jalankan perintah berikut untuk mengirim notifikasi / me-trigger job
```bash
php artisan ping:job
```

8. Buka terminal pada repo subscriber, dan pastikan ada event baru disana yang barusan di kirim oleh publisher.


## Demo

- Setup env dari AMQP
  https://www.loom.com/share/044a3c87a3d84b278b752feb0627c0a9
- Demo aplikasi
  https://www.loom.com/share/3ec04477d31548fabd6180393adff7dd

