# BAKE4U – Delivery & Tracking System Documentation

Welcome to the official documentation repository for **BAKE4U**, a Order & Delivery Management System (OMS/DMS) built with PHP, MySQL, JavaScript, and Leaflet.js.

This repository contains complete **technical and user-facing documentation** covering:

- Delivery Management System (DMS)
- Real-time Driver Tracking System
- System architecture & infrastructure
- Manager & admin processes
- Technical maintenance procedures
- Troubleshooting workflows
- User training manuals

This documentation demonstrates full-stack engineering, system maintenance, troubleshooting, data integrity handling, and communication skills relevant to real operational environments.

---

## 📁 Repository Structure

```
BAKE4U-Documentation/
│
├── README.md                 ← You are here
│
└── doc/
    ├── DMS_Documentation.md
    ├── Tracking_System.md
    ├── User_Manual_Managers.md
    ├── User_Manual_TechAdmin.md
```

---

## Core Features

### **Delivery Management System (DMS)**
- Delivery creation  
- Driver assignment  
- Status workflow  
- Manager dashboard  
- Driver dashboard  
- Real-time location tracking  
- Map integration using Leaflet + OpenStreetMap  
- Geocode caching (performance optimization)  

---

### **Tracking System**
- Customer-facing order tracking API  
- Live driver location  
- Last-known coordinates  
- Distance calculation using Haversine formula  
- Auto-refresh client updates  

---

### **System Infrastructure**
- PHP backend (API-based structure)  
- MySQL/MariaDB schema  
- Session-based authentication  
- Data validation  
- Error logging & debugging workflows  

---

## 📄 Documentation Index

###  **Delivery Management System Documentation**
➡️ `/docs/DMS_Documentation.md`  

---

###  **Tracking System Documentation**
➡️ `/docs/Tracking_System.md`  

---

###  **Manager & Admin User Manual**
➡️ `/docs/User_Manual_Managers.md`  

---

###  **Technical Administrator Manual**
➡️ `/docs/User_Manual_TechAdmin.md`  

---

##  System Architecture Summary

```
+----------------------+         +----------------------+
|  Manager Dashboard   | <-----> |   Delivery API       |
|  (PHP/JS + Leaflet)  |         |   (PHP, MySQL)       |
+----------------------+         +-----------+----------+
                                             |
                                             v
                                   +----------------------+
                                   |  Database (MySQL)    |
                                   |  - orders            |
                                   |  - deliveries        |
                                   |  - driver_locations  |
                                   |  - geocode_cache     |
                                   +----------------------+
                                             ^
                                             |
+----------------------+         +-----------+----------+
|   Driver Dashboard   | <------ |   Tracking API       |
| (Mobile-friendly UI) |         | (GPS updates + JSON) |
+----------------------+         +----------------------+
```

---

## 🎯 Purpose of This Repository

This repository is designed to demonstrate:

- Real-world system documentation  
- End-to-end operational workflows  
- Technical writing skills  
- System maintenance processes  
- API design and backend logic  
- User training and support documentation  
- System optimization and debugging methodology  

---

## 🧩 Technologies Used

- **PHP (Backend)**
- **MySQL / MariaDB (Database)**
- **Leaflet.js + OpenStreetMap (Mapping)**
- **JavaScript (Frontend Logic)**
- **HTML/CSS**
- **Session Authentication**
- **REST-like API Structure**

---

## 🛡 Security Considerations

- PDO prepared statements  
- Role-based access enforcement  
- Sanitized user inputs  
- Session hardening  
- Sensitive data hidden from UI  
- Error logs protected  

---

## Future Enhancements

- WebSocket-based live tracking  
- Automated ETA predictions  
- Push notifications to customers  

---

##  Author

**Matlaba Tshepiso Clayton Machaka**  
BSc Computer Science | Systems Dev & Cybersecurity, 
Johannesburg, South Africa

# 📌 End of README.md
