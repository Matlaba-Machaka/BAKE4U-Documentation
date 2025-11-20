# BAKE4U – Manager & Admin User Manual
This document provides step-by-step instructions for managers and admin users responsible for handling orders, creating deliveries, assigning drivers, reviewing statuses, and monitoring real-time delivery activity on the BAKE4U platform.

---

# 📚 Table of Contents
1. [Overview](#1-overview)  
2. [Logging In](#2-logging-in)  
3. [Manager Dashboard Overview](#3-manager-dashboard-overview)  
4. [Managing Orders](#4-managing-orders)  
5. [Creating Deliveries](#5-creating-deliveries)  
6. [Assigning Drivers](#6-assigning-drivers)  
7. [Tracking Drivers Live](#7-tracking-drivers-live)  
8. [Updating Delivery Statuses](#8-updating-delivery-statuses)  
9. [Filtering & Searching Deliveries](#9-filtering--searching-deliveries)  
10. [Handling System Errors](#10-handling-system-errors)  
11. [Best Practices](#11-best-practices)

---

# 1. Overview
Managers use the dashboard to:

- View all recent orders  
- Convert orders into deliveries  
- Assign drivers  
- Monitor real-time delivery progress  
- Resolve basic data issues  
- Communicate with drivers  
- Ensure accurate status updates  

This manual explains how to use all features effectively.

---

# 2. Logging In

1. Navigate to the Manager Login page.  
2. Enter your **username** and **password**.  
3. Press **Login**.  
4. You will be redirected to the Manager Dashboard.

If you see `"auth_failed"` — contact technical support to reset your session.

---

# 3. Manager Dashboard Overview

The dashboard includes:

### ✔ Orders Table
- All customer orders  
- Their payment status  
- Delivery type (collection or delivery)

### ✔ Deliveries Table
- Pending, assigned, in-progress, and completed deliveries  
- Driver details  
- Status updates  

### ✔ Tools
- **Create Delivery** button  
- **Assign Driver** modal  
- **Live Map** modal (Leaflet)  
- Filters & Sorting options  

---

# 4. Managing Orders

Managers can:

- Verify payment  
- View order details  
- Inspect customer information  
- Prepare items  
- Mark an order as ready for delivery  

To view details:
- Click **View Order** → opens full order breakdown.

---

# 5. Creating Deliveries

1. Open an order.  
2. Press **Create Delivery**.  
3. System automatically:  
   - Sets delivery address  
   - Looks up geolocation (cached or via geocoding)  
   - Creates a new delivery record  
4. Delivery status becomes **pending**.

Manager may now assign a driver.

---

# 6. Assigning Drivers

1. Go to **Deliveries Table**.  
2. Locate the delivery entry.  
3. Click **Assign Driver** dropdown.  
4. Select the driver name.  
5. Status changes to **assigned**.

Driver will see the delivery on their dashboard instantly.

---

# 7. Tracking Drivers Live

1. Click the **Map** icon on a delivery row.  
2. A modal opens with a Leaflet map.  
3. The map shows:  
   - Driver marker  
   - Delivery destination marker  
   - Popups for coordinates  

The system auto-refreshes every 5 seconds.

If the driver is not appearing:
- They may have no GPS permissions  
- They may be offline  
- They may not have moved yet  

---

# 8. Updating Delivery Statuses

Managers can manually update statuses if needed:

- **pending** → waiting for assignment  
- **assigned** → driver selected  
- **out_for_delivery** → driver started  
- **arriving** → driver near destination  
- **delivered** → customer received items  
- **completed** → admin confirmation  

Drivers also update statuses automatically via their UI.

---

# 9. Filtering & Searching Deliveries

Use the dashboard tools:

- Filter by status  
- Search by order ID  
- Sort by driver, status, or date  

This helps managers focus on active deliveries first.

---

# 10. Handling System Errors

Common issues & how to handle them:

### ❗ Missing driver location  
Solution: Ask driver to refresh and allow location access.

### ❗ Undefined address or coordinates  
Solution: Re-open order → recreate delivery (forces re-geocoding).

### ❗ Driver not seeing delivery  
Solution: Reassign the driver → ensures dashboard refresh.

### ❗ Map not loading  
Solution:
- Check network  
- Clear browser cache  
- Reopen the delivery modal  

Any persistent issues should be reported to **Technical Admin**.

---

# 11. Best Practices

- Always verify order information before creating a delivery  
- Assign drivers promptly  
- Monitor map activity for delays  
- Keep communication clear with drivers  
- Escalate repeated errors to Technical Admin  
- Maintain accurate status progression  

---

# 📌 End of Document
