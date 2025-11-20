# BAKE4U – Technical Administrator Manual
This manual provides developers and technical administrators with the required knowledge to maintain the BAKE4U system, resolve errors, ensure data integrity, and support managers and drivers.

---

# 📚 Table of Contents
1. [Role Overview](#1-role-overview)  
2. [System Components](#2-system-components)  
3. [Database Overview](#3-database-overview)  
4. [Troubleshooting Common Errors](#4-troubleshooting-common-errors)  
5. [Managing the Geocode Cache](#5-managing-the-geocode-cache)  
6. [Fixing Stuck Deliveries or Sessions](#6-fixing-stuck-deliveries-or-sessions)  
7. [Driver GPS Issues](#7-driver-gps-issues)  
8. [System Security Notes](#9-system-security-notes)  
9. [Maintenance Checklist](#10-maintenance-checklist)

---

# 1. Role Overview

Technical Administrators are responsible for:

- Maintaining database integrity  
- Monitoring dashboards for errors  
- Resolving system bugs  
- Ensuring geolocation and tracking accuracy  
- Supporting managers & drivers  
- Ensuring API endpoints work correctly  
- Checking error logs  
- Performing data corrections when required  

---

# 2. System Components

The system includes:

### ✔ Backend
- PHP-based API  
- Session authentication  
- PDO database connections  

### ✔ Database
- MySQL/MariaDB  
- Foreign key relations  

### ✔ Frontend
- Manager dashboard  
- Driver dashboard  
- Customer tracking UI  

### ✔ Geolocation
- Leaflet.js  
- OpenStreetMap tiles  
- Nominatim geocoder  
- Geocode caching  

---

# 3. Database Overview

Important tables:

| Table | Purpose |
|-------|---------|
| `users` | Base user accounts |
| `drivers` | Driver profiles |
| `orders` | Customer orders |
| `deliveries` | Delivery tasks |
| `driver_locations` | Location history |
| `geocode_cache` | Address → coords cache |

---

# 4. Troubleshooting Common Errors

### ❗ "Undefined array key"
Cause: Missing or incorrect GET/POST parameter  
Fix: Validate request & add fallback checks  

### ❗ Driver not appearing on map
Cause:  
- No recent GPS entry  
- Driver offline  
- JS error in map modal  

Fix:  
- Check driver_locations table  
- Ask driver to refresh the app  

### ❗ Delivery not showing for driver
Cause: Incorrect driver_id or session  
Fix: Reassign driver in manager dashboard  

### ❗ Repeated geolocation failures
Cause: Nominatim rate limit  
Fix: Ensure cache table is functioning  

---

# 5. Managing the Geocode Cache

### View cache entries:
```sql
SELECT * FROM geocode_cache ORDER BY created_at DESC;
```

### Delete corrupted entries:
```sql
DELETE FROM geocode_cache WHERE address = '...';
```

### Clear entire cache:
```sql
TRUNCATE geocode_cache;
```

---

# 6. Fixing Stuck Deliveries or Sessions

### Destroying corrupted sessions
```php
session_unset();
session_destroy();
```

---

# 7. Driver GPS Issues

### Check latest coordinates:
```sql
SELECT * FROM driver_locations
WHERE driver_id = ?
ORDER BY recorded_at DESC
LIMIT 1;
```

### If lat/lng are NULL:
- Restart the driver browser/app  
- Ensure GPS permissions are granted  
- Verify POST payload includes correct keys  

---

# 8. System Security Notes

- Always use prepared statements (PDO)  
- Validate all user inputs  
- Enforce role-based access control  
- Regenerate sessions on login  
- Avoid exposing SQL errors to end users  

---

# 9. Maintenance Checklist

Weekly tasks:
- Review `driver_locations` table for size bloat  
- Clear stale geocode cache entries  
- Confirm API endpoints work as expected  
- Verify Leaflet map loading  
- Check for undefined array warnings  
- Test GPS update workflow manually  

---

#  End of Document
