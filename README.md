# YSFReflector-Dashboard2

Modern web application dashboard for viewing connected gateways, repeaters, active users, and system statistics for YSFReflector and pYSFReflector.
Version 2 Official

![License](https://img.shields.io/badge/license-GPL--3.0-blue.svg)
![PHP](https://img.shields.io/badge/PHP-7.4%20%7C%208.x-purple.svg)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4.svg)

## Features

- **Modern UI** - Beautiful glass-morphism design with Tailwind CSS
- **Fully Responsive** - Works seamlessly on desktop, tablet, and mobile devices. App ready!
- **Real-time Monitoring** - View connected gateways, last heard list, and system stats
- **Improved TX Detection** - Faster more responsive TX update logic
- **Easy Setup** - Initial setup wizard for first-time configuration
- **Branding** - Customize dashboard name, tagline, and logo
- **System Monitoring** - CPU load, temperature, disk usage, and uptime
- **Privacy Options** - GDPR-compliant callsign anonymization
- **QRZ Integration** - Optional links to QRZ.com for callsigns

## Screenshots

### Running Dashboard
![YSFReflector-Dashboard2 Screenshot](https://github.com/user-attachments/assets/fb5440a7-7be5-4132-9010-4816d935daad)

*Dashboard showing real-time connection with pYSFReflector, including connected gateways, system information, and last heard list*

## Installation

### Requirements

- PHP >= 7.4 - 8.3
- Node.js >= 16.x (for building CSS)
- Web server (Apache, Nginx, or lighttpd)
- YSFReflector or pYSFReflector installed and running

### Compatibility

This dashboard has been tested and confirmed to work with:
- **PHP Versions**: 7.4, 8.0, 8.1, 8.2, 8.3
- **YSFReflector**: G4KLX YSFReflector (C++ implementation)
- **pYSFReflector**: IU5JAE Python implementation (confirmed working)

### Step 1: Clone the Repository

```bash
cd /var/www/html
git clone https://github.com/ShaYmez/YSFReflector-Dashboard2.git
cd YSFReflector-Dashboard2
```

### Step 2: Install Dependencies and Build CSS

```bash
npm install
npm run build:css
```

### Step 3: Configure Web Server Permissions

```bash
# Give write permissions for config directory
sudo chown -R www-data:www-data /var/www/html/YSFReflector-Dashboard2
sudo chmod -R 755 /var/www/html/YSFReflector-Dashboard2
```

### Step 4: Configure Web Server

#### For Apache

Create a virtual host configuration:

```apache
<VirtualHost *:80>
    ServerName your-domain.com
    DocumentRoot /var/www/html/YSFReflector-Dashboard2
    
    <Directory /var/www/html/YSFReflector-Dashboard2>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    
    ErrorLog ${APACHE_LOG_DIR}/ysf-dashboard-error.log
    CustomLog ${APACHE_LOG_DIR}/ysf-dashboard-access.log combined
</VirtualHost>
```

Enable the site and restart Apache:

```bash
sudo a2ensite ysf-dashboard
sudo systemctl restart apache2
```

#### For Nginx

Add to your Nginx configuration:

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/html/YSFReflector-Dashboard2;
    
    index index.php index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    }
    
    location ~ /\.ht {
        deny all;
    }
}
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

### Step 5: Initial Setup

![Setup Wizard](https://github.com/user-attachments/assets/fb5440a7-7be5-4132-9010-4816d935daad)

1. Open your browser and navigate to `http://your-domain.com/setup.php`
2. Fill in the configuration form:
   - **Dashboard Branding**: Name, tagline, and logo URL
   - **YSFReflector Configuration**: Paths to log files, ini file, and executable
   - **Global Settings**: Timezone, refresh interval, and display options
3. Click "Save Configuration"
4. **Important**: Delete `setup.php` for security:

```bash
sudo rm /var/www/html/YSFReflector-Dashboard2/setup.php
```

5. Access your dashboard at `http://your-domain.com/index.php`

## Configuration

### YSFReflector Log Files

Ensure your YSFReflector is configured to write logs:

```ini
[Log]
FilePath=/var/log/YSFReflector/
FileRoot=YSFReflector
```

### Dashboard Settings

After initial setup, you can manually edit `config/config.php`:

```php
// Example configuration
define("YSFREFLECTORLOGPATH", "/var/log/YSFReflector/");
define("YSFREFLECTORLOGPREFIX", "YSFReflector");
define("YSFREFLECTORINIPATH", "/etc/");
define("YSFREFLECTORINIFILENAME", "YSFReflector.ini");
define("TIMEZONE", "America/New_York");
define("REFRESHAFTER", "15"); // No longer used - dashboard updates via JavaScript
define("DASHBOARD_NAME", "My YSF Reflector");
define("LOGO", "https://example.com/logo.png"); // URL or local path
```

**Note**: The `REFRESHAFTER` setting is now deprecated as the dashboard uses JavaScript for live updates and no longer requires page refreshes.

### Logo Configuration

The dashboard supports multiple ways to add a logo:

**Option 1: Local Image File (Recommended)**

1. Place your logo file in the `img/` directory with the filename `logo.png`, `logo.jpg`, or any supported format
2. Supported formats: PNG, JPEG, JPG, BMP, WebP, GIF, SVG
3. The dashboard will automatically detect and display it
4. No configuration needed!

Example:
```bash
# Copy your logo to the img directory
cp /path/to/your/logo.png /var/www/html/YSFReflector-Dashboard2/img/logo.png
```

**Option 2: External URL**

Set the `LOGO` constant in `config/config.php` to a full URL:
```php
define("LOGO", "https://example.com/your-logo.png");
```

**Option 3: Custom Local Path**

Set the `LOGO` constant to a relative path:
```php
define("LOGO", "assets/custom-logo.png");
```

The logo will be automatically scaled to fit within the header while maintaining aspect ratio, and the responsive design ensures it looks great on all devices.

### Responsiveness Features

The dashboard provides a fully dynamic, real-time experience without page reloads:

- **Live Dashboard Updates**: JavaScript polls the dashboard API every 5 seconds for all data
- **Real-Time TX Status**: Instant transmission detection with dynamic show/hide of TX alert
- **Live Last Heard List**: Automatically updates as new transmissions are logged
- **Live Gateway List**: Real-time connected gateway updates
- **180-Second TX Timeout**: Matches standard amateur radio transmission timeout for proper QSO handling
- **Smart End Detection**: Properly detects transmission end markers to support multimode networks with shared callsigns
- **No Page Reloads**: Smooth, uninterrupted experience with all data updating in the background

## Customization

### Custom Styling

Edit `src/styles.css` to customize colors and styling, then rebuild:

```bash
npm run build:css
```

### Live Development

For live CSS development with auto-reload:

```bash
npm run dev
```

## Security

- Always delete `setup.php` after initial configuration
- Ensure proper file permissions (755 for directories, 644 for files)
- Keep PHP and dependencies up to date
- Use HTTPS in production environments
- Enable GDPR mode to anonymize callsigns if required

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the GPL-3.0 License - see the LICENSE file for details.

## Credits
- Designed by [M0VUB Aka ShaYmez](https://github.com/shaymez/YSFReflector-Dashboard2)
- Based on the original [YSFReflector-Dashboard](https://github.com/dg9vh/YSFReflector-Dashboard) by DG9VH
- Compatible with [pYSFReflector](https://github.com/iu5jae/pYSFReflector) by IU5JAE
- Built with [Tailwind CSS](https://tailwindcss.com/)

## 💬 Support

For issues, questions, or suggestions:
- Open an issue on [GitHub](https://github.com/ShaYmez/YSFReflector-Dashboard2/issues)
- Check existing documentation and issues first

## Updates

To update the dashboard:

```bash
cd /var/www/html/YSFReflector-Dashboard2
git pull origin main
npm install
npm run build:css
```

---

**Made with ❤️ for the Amateur Radio Community**
