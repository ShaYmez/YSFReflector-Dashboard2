# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.1] - 2025-12-26

### Security
- **XSS Protection** - Added htmlspecialchars() escaping for all user-facing output to prevent cross-site scripting attacks
- **Input Validation** - Added parameter sanitization in getConfigItem() to prevent potential injection attacks
- **Command Injection Prevention** - Enhanced security of git output in getGitVersion() function
- **Safe File Operations** - Added file existence and readability checks in getYSFReflectorConfig()

### Fixed
- **TXing Disappearing Issue** - Increased TX timeout from 30 to 180 seconds to match standard amateur radio transmission timeout and prevent TX indicator from disappearing during active transmissions
- **TXing Duration Display** - Fixed getCurrentlyTXing() to display accurate QSO duration by calculating from transmission start instead of most recent data packet
- **TXing Callsign Accuracy** - Improved callsign tracking during overlapping transmissions to always show the correct active transmitter
- **Transmission End Detection** - Enhanced logic to properly detect when a transmission has ended by checking for end markers after the most recent data packet
- **Duration Calculation** - Now tracks backwards from most recent data to find when the same callsign started transmitting, providing accurate total QSO time
- **Error Handling** - Improved getConfigItem() with better bounds checking and empty array handling

### Changed
- Increased TX timeout from 30 to 180 seconds to align with standard amateur radio transmission timeout practices
- Updated package.json version to 2.0.1
- Updated browserslist database for latest browser compatibility

### Removed
- **Code Cleanup** - Removed unused functions: getMHZ(), isProcessRunning(), getOldYSFReflectorLog()
- **Dead Code** - Eliminated unused $oldlogLines variable

### Technical
- Rewrote getCurrentlyTXing() function with improved three-step algorithm:
  1. Find most recent transmission data to identify current transmitter
  2. Check for end markers after most recent data
  3. Calculate duration from actual transmission start time
- Increased `$txTimeout` from 30 to 180 seconds in getCurrentlyTXing() function to match standard ham radio timeout
- Added input validation with regex pattern matching in getConfigItem()
- Enhanced error logging in getYSFReflectorConfig()
- All PHP files pass syntax validation
- Zero NPM security vulnerabilities
- Updated documentation to reflect 180-second TX timeout
- Removed unused transmissionStartIndex variable for cleaner code
- Added comprehensive test coverage for TX detection scenarios

## [2.0.0] - 2025-12-25

### Added
- **Modern Glossy UI** - Complete redesign with beautiful glass-morphism design using Tailwind CSS 3.4
- **Fully Responsive Design** - Seamless experience across desktop, tablet, and mobile devices
- **Real-time Monitoring Dashboard** - Enhanced view of connected gateways, last heard list, and system statistics
- **Currently Transmitting (TXing) Indicator** - Prominent real-time alert showing active transmissions with pulsing animation, callsign, target, and gateway information
- **Initial Setup Wizard** - Easy first-time configuration with guided setup process
- **Branding Support** - Customizable dashboard name, tagline, and logo options
- **System Monitoring** - Comprehensive CPU load, temperature, disk usage, and uptime monitoring
- **Privacy Options** - GDPR-compliant callsign anonymization feature
- **QRZ Integration** - Optional clickable links to QRZ.com for callsigns in last heard list
- **Animated Background** - Beautiful gradient background with animated pulse effects
- **System Stats Grid** - Four-card grid showing connected gateways, CPU load, temperature, and disk usage
- **Connected Gateways Table** - Real-time display of currently connected gateways with timestamps
- **System Information Panel** - Detailed system uptime, load averages, and version information
- **Last Heard List** - Complete table of recent activity with callsign, target, and gateway information
- **Version Display** - Dashboard version shown in footer with YSFReflector version
- **Auto-refresh Support** - Configurable automatic page refresh interval
- **Page Generation Time** - Performance metrics displayed in footer

### Changed
- **Complete UI Overhaul** - Migrated from legacy design to modern Tailwind CSS-based interface
- **Enhanced Performance** - Optimized page generation and rendering
- **Improved Readability** - Better contrast and modern typography throughout the dashboard
- **Better Mobile Experience** - Responsive tables and card layouts for all screen sizes

### Technical
- **PHP Compatibility** - Tested and confirmed working with PHP 7.4, 8.0, 8.1, 8.2, and 8.3
- **YSFReflector Support** - Compatible with G4KLX YSFReflector (C++ implementation)
- **pYSFReflector Support** - Confirmed working with IU5JAE's Python implementation
- **Node.js Build System** - Integration with npm for CSS building and development
- **Tailwind CSS 3.4** - Modern utility-first CSS framework for styling
- **Chart.js Integration** - Support for future data visualization features
- **Modular Architecture** - Separated functions and tools into dedicated include files

### Security
- **Setup Security** - Instructions to remove setup.php after initial configuration
- **File Permissions** - Proper guidelines for secure file and directory permissions
- **HTTPS Ready** - Prepared for secure production deployments
- **GDPR Compliance** - Optional callsign anonymization for privacy requirements

### Documentation
- **Comprehensive README** - Complete installation and configuration guide
- **Installation Guide** - Step-by-step setup instructions for Apache and Nginx
- **Configuration Examples** - Sample configurations for web servers and YSFReflector
- **Screenshot Documentation** - Visual reference for dashboard appearance
- **Customization Guide** - Instructions for custom styling and branding

## Release Information

Version 2.0.0 represents a complete rewrite and modernization of the YSFReflector Dashboard. This major version includes a brand-new user interface, improved compatibility, and enhanced features while maintaining full backward compatibility with YSFReflector configurations.

### Upgrade Notes
- This is a major version release with significant UI changes
- All existing configuration from previous versions should be migrated through the setup wizard
- Ensure Node.js >= 16.x is installed for building CSS assets
- Run `npm install` and `npm run build:css` after updating

### Credits
- Designed by M0VUB (ShaYmez)
- Based on the original YSFReflector-Dashboard by DG9VH
- Compatible with pYSFReflector by IU5JAE
- Built with Tailwind CSS

---

**For more information, visit:** [GitHub Repository](https://github.com/ShaYmez/YSFReflector-Dashboard2)
