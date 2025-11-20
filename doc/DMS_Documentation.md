# BAKE4U – Delivery Management System (DMS)
Comprehensive technical documentation for the Delivery Management System (DMS) of the BAKE4U platform.  
This document describes delivery creation, driver assignment, geolocation logic, tracking functionality, and dashboard interfaces.

---

# 📚 Table of Contents
1. [Overview](#1-overview)  
2. [Delivery Workflow Summary](#2-delivery-workflow-summary)  
3. [System Architecture](#3-system-architecture-high-level)  
4. [Delivery Creation](#4-delivery-creation-flow)  
5. [Driver Assignment](#5-driver-assignment)  
6. [Leaflet Mapping & Geolocation](#6-leaflet-mapping--geolocation)  
7. [Real-Time Driver Tracking](#7-real-time-driver-tracking)  
8. [Geocode Caching](#8-geocode-caching-system)  
9. [Delivery Status Workflow](#9-delivery-status-workflow)  
10. [Manager Dashboard](#10-manager-dashboard-dms)  
11. [Driver Dashboard](#11-driver-dashboard-dms)   
12. [Error Handling](#13-error-handling--logging)  
13. [Future Improvements](#14-future-improvements)

---

# 1. Overview
The BAKE4U Delivery Management System (DMS) manages the full delivery lifecycle:

- Delivery creation  
- Driver assignment  
- Live geolocation tracking  
- Status updates  
- Dashboard interfaces  

It interacts with the OMS (Order Management System) to convert ready orders into delivery tasks.

---

# 2. Delivery Workflow Summary

```txt
Order Confirmed
      ↓
Delivery Created
      ↓
Driver Assigned
      ↓
Driver Starts Delivery
      ↓
Out for Delivery → Arriving → Delivered → Completed
```

Delivery Statuses:
- `pending`
- `assigned`
- `out_for_delivery`
- `arriving`
- `delivered`
- `completed`

---

# 3. System Architecture (High-Level)

```txt
+----------------------+       +----------------------+
|  Manager Dashboard   |       |   Driver Dashboard   |
|  (PHP + JS + Leaflet)|       |      (PHP + JS)      |
+----------+-----------+       +----------+-----------+
           |                                  |
           | AJAX / Fetch API                 |
           v                                  v
   +----------------------+        +-----------------------------+
   |   Delivery API       | <----> |   driver_locations Table    |
   |       (PHP)          |        +-----------------------------+
   +----------+-----------+
              |
              v
     +--------------------+
     | deliveries Table   |
     | orders Table       |
     +--------------------+
```

---

# 4. Delivery Creation Flow

### 4.1 Trigger Events
Deliveries are created when:

- The manager manually creates one  
- An order reaches **Ready for Delivery**  

### 4.2 Required Data
- `order_id`  
- `delivery_address`  
- `gps_latitude`  
- `gps_longitude`  
- `driver_id` *(optional)*  
- `status` = `pending`  

### 4.3 SQL Insert

```sql
INSERT INTO deliveries (order_id, delivery_address, gps_latitude, gps_longitude, status)
VALUES (?, ?, ?, ?, 'pending');
```

---

# 5. Driver Assignment

### 5.1 Assignment Flow
1. Manager selects driver  
2. System updates `driver_id`  
3. Status changes to `assigned`  
4. Driver sees delivery on dashboard  

### 5.2 Assignment Query

```sql
UPDATE deliveries
SET driver_id = ?, status = 'assigned'
WHERE delivery_id = ?;
```

---

# 6. Leaflet Mapping & Geolocation

Used for:
- Delivery destination map  
- Driver current location  
- Route visualization  
- Map popups and styling  

### Example Leaflet Initialization:

```js
const map = L.map('map').setView([lat, lng], 15);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png')
    .addTo(map);

L.marker([deliveryLat, deliveryLng]).addTo(map)
    .bindPopup("Delivery Destination");
```

---

# 7. Real-Time Driver Tracking

Tracking is implemented through **polling** (every 5 seconds).

### 7.1 Driver Sends Location

**Endpoint:**
```
POST /driver/update-location.php
```

**Payload:**
```json
{
  "driver_id": 12,
  "gps_latitude": -26.1234,
  "gps_longitude": 28.5678
}
```

### 7.2 Manager Dashboard Polling

```
GET /api/get-driver-location.php?driver_id=12
```

### 7.3 Fetch Latest Location Query

```sql
SELECT driver_id, gps_latitude, gps_longitude, recorded_at
FROM driver_locations
WHERE driver_id = ?
ORDER BY recorded_at DESC
LIMIT 1;
```

---

# 8. Geocode Caching System

This reduces external geocoding calls (Nominatim).

### Table Structure

```txt
geocode_cache
-------------
id
address
latitude
longitude
created_at
```

### Lookup Logic

```txt
IF address exists → return cached
ELSE → geocode → store → return
```

### Example SELECT

```sql
SELECT * FROM geocode_cache WHERE address = ? LIMIT 1;
```

---

# 9. Delivery Status Workflow

### Manager Status Updates
- Assign driver  
- Verify order  
- Cancel/Reset  

### Driver Status Updates
- Start → `out_for_delivery`  
- Arriving → `arriving`  
- Delivered → `delivered`  
- Auto-complete → `completed`  

Status flow diagram:

```txt
pending → assigned → out_for_delivery → arriving → delivered → completed
```

---

# 10. Manager Dashboard (DMS)

Key Features:
- View all deliveries  
- Assign drivers  
- Track drivers in real time  
- Open map modal with live markers  
- Filter deliveries by status  
- View customer details  

UI elements:
- Tables  
- Dropdowns  
- Modals (Leaflet Map)  
- Status tags  

---

# 11. Driver Dashboard (DMS)

Key Features:
- View assigned deliveries  
- Update status step-by-step  
- Send GPS location automatically  
- Access navigation map  
- Refresh delivery list  

UI elements:
- Delivery list  
- Action buttons  
- Map preview  
- Geolocation permission prompts  

---

# 12. Error Handling & Logging

Common errors logged:
- Undefined array keys  
- Missing coordinates  
- No driver linked to user  
- Geocode API failure  
- SQL errors  

### Logging Pattern:

```php
error_log("[DMS] Missing driver ID in request");
error_log("[DMS] Failed to fetch driver location: ID = $driver_id");
```

---

# 13. Future Improvements

Potential enhancements:
- Switch from polling → WebSockets  
- Add ETA calculations  
- SMS/Push notifications  
- Driver offline mode  
- Heatmap of delivery locations  

---

# 📌 End of Document
