# Laravel Telegram Uploader

This is a simple web application allows users to upload files to a Telegram chat more than 50mg.
please fork it and create new Future and help me to Improve this application.
## Languages/libraries/packages used
- Laravel 11
- Vue.js 3
- Telegram-upload (https://github.com/Nekmo/telegram-upload)
- Laravel Queue
- Tailwind CSS
- FilePond (https://github.com/pqina/filepond, https://github.com/pqina/vue-filepond)

## Prerequisites

- PHP 8.0 or higher
- Node.js and npm
- Python 3.6 or higher (max version 11) (for telegram-upload)
- Composer
## Installation Steps
### 1. Basic Setup
- Clone the repository
- Run `composer install`
- Run `npm install`
- Copy `.env.example` to `.env`
- Run `php artisan key:generate`
- Run `php artisan storage:link`
- Run `php artisan migrate`
### 2. Install telegram-upload
  ```bash
  pip3 install -U telegram-upload
  ```

- Create Telegram API credentials:
  1. Visit https://my.telegram.org/apps
  2. Create new application
  3. Save `api_id` and `api_hash`
  4. Run `telegram-upload --configure`
  5. Enter your phone number, api_id, and api_hash
  6. Enter the verification code sent to your Telegram

### 3. SQLite Setup
```bash
sudo apt-get install sqlite3
touch database/database.sqlite
```
Update .env file:
```
DB_CONNECTION=sqlite
DB_DATABASE=/absolute/path/to/database/database.sqlite
```

### 4. Environment Configuration
Update the following in .env :
```
TELEGRAM_CHAT_ID=your_chat_id
TELEGRAM_UPLOAD_PATH_TO_BINARY=/usr/local/bin/telegram-upload
```

## Running Locally

Run these commands in separate terminals:
```bash
npm run dev
php artisan serve
php artisan queue:work
```

## Server Deployment

### One-Command Setup Script
Create `setup.sh` in your project root:
```bash
#!/bin/bash
composer install --no-dev
npm install
npm run build
php artisan key:generate
php artisan storage:link
php artisan migrate
```
Make it executable:
```bash
chmod +x setup.sh
```

### Auto-start Configuration

1. Create systemd service for Laravel Queue:
```bash
sudo nano /etc/systemd/system/laravel-queue.service
```
Add:
```ini
[Unit]
Description=Laravel Queue Worker
After=network.target

[Service]
User=your_user
Group=your_group
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/php artisan queue:work
Restart=always

[Install]
WantedBy=multi-user.target
```

2. Create systemd service for Laravel Web Server:
```bash
sudo nano /etc/systemd/system/laravel-server.service
```
Add:
```ini
[Unit]
Description=Laravel Web Server
After=network.target

[Service]
User=your_user
Group=your_group
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/php artisan serve --host=0.0.0.0 --port=8000
Restart=always

[Install]
WantedBy=multi-user.target
```

3. Enable and start services:
```bash
sudo systemctl enable laravel-queue
sudo systemctl enable laravel-server
sudo systemctl start laravel-queue
sudo systemctl start laravel-server
```

## Server Deployment Steps

1. Clone repository
2. Run `./setup.sh`
3. Configure environment variables
4. Start services:
```bash
sudo systemctl start laravel-queue
sudo systemctl start laravel-server
```

## Checking Service Status
```bash
sudo systemctl status laravel-queue
sudo systemctl status laravel-server
```

## Improvement Steps

1. **Improve Error Handling:**
   - Add comprehensive error handling in the Laravel controllers and Vue components.
   - Implement logging for critical errors.

2. **Enhance Security:**
   - Implement authentication and authorization.
   - Use HTTPS for secure communication.

3. **Optimize Performance:**
   - Use caching mechanisms to reduce database load.
   - Optimize database queries.

4. **Add Unit Tests:**
   - Write unit tests for Laravel controllers and services.
   - Write unit tests for Vue components.

5. **Improve User Interface:**
   - Enhance the UI/UX with better design and user feedback.
   - Add progress indicators for file uploads.

6. **Documentation:**
   - Improve the documentation with detailed setup instructions.
   - Add API documentation for the backend endpoints.

## Future Goals

1. **Add Support for Multiple File Uploads:**
   - Allow users to upload multiple files at once.

2. **Implement WebSocket for Real-time Updates:**
   - Use WebSocket to provide real-time updates on file upload status.

3. **Add Admin Dashboard:**
   - Create an admin dashboard to manage uploads and users.

4. **Integrate with Other Cloud Storage Services:**
   - Add support for uploading files to other cloud storage services like AWS S3, Google Drive, etc.

5. **Mobile App:**
   - Develop a mobile app for easier file uploads on the go.
**Note:**
- You need to install and configure Telegram-upload first. Go to it's repository for more information.
- Change the database configuration and the following variables in the `.env` file:
    - `TELEGRAM_CHAT_ID` - Chat ID where the files will be uploaded
    - `TELEGRAM_UPLOAD_PATH_TO_BINARY` - Path to the telegram-upload binary


❤️ Thanks
=========
This project developed by `Kamal Ashraf Gill  <https://github.com/Nekmo>`_ & `Mohammad Ah <https://github.com/mohammadham>`_ .

