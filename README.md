# Promotional Login System - Dynamic Marketing CMS

[![PHP Version](https://img.shields.io/badge/PHP-7.4%2B-blue.svg)](https://php.net)
[![MySQL](https://img.shields.io/badge/MySQL-5.7%2B-orange.svg)](https://mysql.com)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Sistem login dan registrasi yang inovatif dengan **promotional sidebar dinamis** dan panel admin untuk mengelola konten marketing. Cocok untuk SaaS, e-commerce, atau platform apapun yang ingin menampilkan promosi menarik di halaman autentikasi.

## 🎯 Fitur Unggulan

### 🎨 Promotional Login Experience
- **Dynamic Promo Sidebar** - Tampilkan promosi real-time di halaman login/register
- **Discount Display** - Showcase multiple discount dengan animasi menarik
- **Domain Pricing** - Tampilkan harga khusus dan penawaran terbatas
- **Visual Effects** - Gradient backgrounds dan animasi CSS yang smooth

### 🔐 Authentication System
- **User Registration** - Form registrasi dengan validasi lengkap
- **Secure Login** - Sistem login dengan session management
- **Admin Authentication** - Panel admin terpisah dengan akses terbatas
- **User Dashboard** - Dashboard pengguna setelah login berhasil

### 🛠️ Admin Management Panel
- **Promotion Manager** - Buat, edit, dan kelola promosi secara real-time
- **Content Editor** - Kelola hero section, services, dan testimonials
- **Landing Page CMS** - Edit konten landing page tanpa coding
- **User Statistics** - Monitor registrasi dan aktivitas pengguna

### 📱 Modern Design
- **Responsive Layout** - Optimal di desktop, tablet, dan mobile
- **Split-Screen Design** - Promo di kiri, form di kanan
- **Gradient Themes** - Kombinasi warna yang eye-catching
- **Micro-interactions** - Hover effects dan smooth transitions

## 🚀 Demo Screenshots

```
┌─────────────────────────────────────────────────────────┐
│  PROMO SIDEBAR          │         LOGIN FORM            │
│  ┌─────────────────┐    │    ┌─────────────────────┐    │
│  │ 🔥 SPECIAL      │    │    │  Welcome Back!     │    │
│  │ Up to 50% OFF   │    │    │  ┌───────────────┐  │    │
│  │     +           │    │    │  │ Email         │  │    │
│  │   15% Extra     │    │    │  └───────────────┘  │    │
│  └─────────────────┘    │    │  ┌───────────────┐  │    │
│  ┌─────────────────┐    │    │  │ Password      │  │    │
│  │ DOMAIN PROMO    │    │    │  └───────────────┘  │    │
│  │ From 299K/month │    │    │  [  Login  ]        │    │
│  └─────────────────┘    │    └─────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

## 📋 Requirements

- PHP 7.4+ dengan PDO extension
- MySQL 5.7+ atau MariaDB 10.3+
- Web Server (Apache/Nginx)
- Modern browser untuk optimal experience

## 🛠️ Quick Installation

1. **Clone & Setup**
   ```bash
   git clone https://github.com/username/promotional-login-system.git
   cd promotional-login-system
   ```

2. **Database Setup**
   ```sql
   CREATE DATABASE promo_login_db;
   CREATE USER 'login'@'localhost' IDENTIFIED BY '@Login2025';
   GRANT ALL PRIVILEGES ON promo_login_db.* TO 'login'@'localhost';
   ```

3. **Import Database Schema**
   ```sql
   -- Users table
   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       email VARCHAR(255) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL,
       phone VARCHAR(20),
       company VARCHAR(255),
       status ENUM('active', 'inactive') DEFAULT 'active',
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );

   -- Promotional content table (CORE FEATURE)
   CREATE TABLE promotional_content (
       id INT AUTO_INCREMENT PRIMARY KEY,
       title VARCHAR(255) NOT NULL,
       subtitle TEXT,
       type ENUM('discount', 'domain', 'special') NOT NULL,
       content JSON,
       price VARCHAR(100),
       status ENUM('active', 'inactive') DEFAULT 'active',
       display_order INT DEFAULT 1,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );

   -- Landing page settings
   CREATE TABLE landing_settings (
       setting_key VARCHAR(100) PRIMARY KEY,
       setting_value TEXT,
       updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
   );

   -- Services for landing page
   CREATE TABLE landing_services (
       id INT AUTO_INCREMENT PRIMARY KEY,
       icon VARCHAR(10) NOT NULL,
       title VARCHAR(255) NOT NULL,
       description TEXT NOT NULL,
       status ENUM('active', 'inactive') DEFAULT 'active',
       display_order INT DEFAULT 1
   );

   -- Customer testimonials
   CREATE TABLE landing_testimonials (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       company VARCHAR(255),
       content TEXT NOT NULL,
       rating INT DEFAULT 5,
       status ENUM('active', 'inactive') DEFAULT 'active',
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

4. **Configure Database Connection**
   
   Update database config in all PHP files:
   ```php
   $host = 'localhost';
   $dbname = 'promo_login_db';
   $username = 'login';
   $password = '@Login2025';
   ```

## 📁 Project Structure

```
promotional-login-system/
├── 📄 index.php              # Landing page with services showcase
├── 🔐 login.php              # LOGIN WITH PROMOTIONAL SIDEBAR ⭐
├── 📝 register.php           # REGISTRATION WITH PROMO DISPLAY ⭐
├── 📊 dashboard.php          # User dashboard after login
├── ⚙️ admin_panel.php        # ADMIN: Manage promotions ⭐
├── 🎨 admin_landing.php      # ADMIN: Landing page editor
├── 🚪 logout.php             # Logout functionality
└── 📖 README.md              # This documentation
```

## 🎮 How to Use

### 👤 User Experience
1. **Landing Page**: Visit `index.php` to see the main website
2. **See Promos**: Go to `login.php` or `register.php` to see **live promotions**
3. **Register**: Create account with promotional offers visible
4. **Login**: Access dashboard with promotional incentives

### 👨‍💼 Admin Management
1. **Admin Login**: 
   - Email: `admin@yoursite.com`
   - Password: `admin123`
2. **Manage Promos**: Use `admin_panel.php` to create/edit promotional content
3. **Update Landing**: Use `admin_landing.php` to manage website content

### 🎯 Promotional Features

#### Discount Promotions
```php
// Example: Create stacked discounts
$promotion = [
    'title' => 'Black Friday Special',
    'type' => 'discount',
    'content' => json_encode([
        ['label' => 'Disc up to', 'value' => '70%'],
        ['label' => 'Extra', 'value' => '15%'],
        ['label' => 'Cashback', 'value' => '10%']
    ])
];
```

#### Domain/Product Pricing
```php
// Example: Special pricing display
$domainPromo = [
    'title' => 'Domain Flash Sale',
    'type' => 'domain',
    'price' => '199K/year',
    'subtitle' => 'Buy 1 Get 1 Free + Transfer'
];
```

## 🎨 Customization Guide

### 🌈 Change Color Scheme
```css
/* Primary gradient - Update in all CSS sections */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Accent color for buttons and highlights */
background: #4CAF50;

/* Promotional badges */
background: linear-gradient(45deg, #ff6b6b, #ffa726);
```

### ✨ Add New Promotion Types
1. Add new ENUM value in database:
   ```sql
   ALTER TABLE promotional_content 
   MODIFY COLUMN type ENUM('discount', 'domain', 'special', 'flash_sale');
   ```

2. Update admin panel form and display logic
3. Add corresponding CSS styling

### 📱 Mobile Optimization
The system is fully responsive, but you can customize breakpoints:
```css
@media (max-width: 768px) {
    .container {
        flex-direction: column;
    }
    .promo-section {
        order: 2; /* Show promo after form on mobile */
    }
}
```

## 🔥 Advanced Features

### Real-time Promo Updates
Promotions update immediately after admin changes - no caching issues!

### A/B Testing Ready
Easy to implement different promotional layouts:
```php
// Example: Random promo display
$promoLayout = (rand(1,2) == 1) ? 'layout_a' : 'layout_b';
```

### Analytics Integration
Add tracking to promotional elements:
```javascript
// Track promo clicks
document.querySelectorAll('.promo-card').forEach(card => {
    card.addEventListener('click', () => {
        gtag('event', 'promo_click', {
            'promo_type': card.dataset.type,
            'promo_title': card.dataset.title
        });
    });
});
```

## 🛡️ Security Features

- ✅ SQL Injection protection with prepared statements
- ✅ XSS prevention with input sanitization
- ✅ Session management with proper logout
- ✅ Admin access control
- ⚠️ **Note**: Password hashing uses MD5 (consider upgrading to bcrypt)

### Recommended Security Upgrade
```php
// Upgrade password hashing
$hash = password_hash($password, PASSWORD_DEFAULT);

// Verify password
if (password_verify($inputPassword, $storedHash)) {
    // Login successful
}
```

## 📊 Database Schema Focus

### 🎯 Promotional Content Table (Core Feature)
| Field | Type | Purpose |
|-------|------|---------|
| type | ENUM | discount/domain/special |
| content | JSON | Flexible promo data storage |
| display_order | INT | Control promo sequence |
| status | ENUM | Enable/disable promos |

### Example JSON Content Structure
```json
{
  "discounts": [
    {"label": "Save up to", "value": "50%"},
    {"label": "Extra", "value": "15%"}
  ],
  "features": ["Free Setup", "24/7 Support"],
  "deadline": "2024-12-31"
}
```

## 🎯 Use Cases

### 🛍️ E-commerce Platform
- Show product discounts during checkout
- Display seasonal promotions
- Highlight member benefits

### 💼 SaaS Application
- Promote plan upgrades
- Show trial extensions
- Highlight new features

### 🎓 Educational Platform
- Course discounts
- Certification promotions
- Early bird pricing

### 🏢 Business Services
- Service packages
- Limited-time offers
- Referral bonuses

## 🐛 Troubleshooting

### Promotions Not Showing
1. Check database connection
2. Verify promotional_content table exists
3. Ensure status = 'active' in admin panel

### CSS Not Loading
1. Check file paths are correct
2. Verify web server serves CSS properly
3. Clear browser cache

### Admin Access Issues
```php
// Default admin credentials
Email: admin@yoursite.com
Password: admin123

// Create new admin user manually in database if needed
```

## 🔄 Roadmap

- [ ] **Email marketing integration** for promotional campaigns
- [ ] **Scheduled promotions** with start/end dates
- [ ] **User-specific promotions** based on behavior
- [ ] **Promotion analytics** dashboard
- [ ] **A/B testing framework** for promotional layouts
- [ ] **Mobile app integration** APIs
- [ ] **Social media sharing** for promotions
- [ ] **Multilingual support** for global reach

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/PromoFeature`)
3. Commit changes (`git commit -m 'Add promotional feature'`)
4. Push to branch (`git push origin feature/PromoFeature`)
5. Create Pull Request

**Focus Areas for Contribution:**
- New promotional layouts
- Additional authentication methods
- Performance optimizations
- Security enhancements

## 📄 License

MIT License - feel free to use in commercial projects!

## 🌟 Star History

If this promotional login system helps your project, please give it a ⭐!

## 📞 Support

- 📧 Email: support@yourproject.com
- 💬 Discussions: Use GitHub Discussions
- 🐛 Issues: Report bugs via GitHub Issues
- 📖 Wiki: Check the project wiki for advanced guides

**Project Link**: [https://github.com/username/promotional-login-system](https://github.com/username/promotional-login-system)

---

**💡 Perfect for**: Marketing-focused startups, e-commerce platforms, SaaS applications, or any business that wants to convert visitors during the login process!
