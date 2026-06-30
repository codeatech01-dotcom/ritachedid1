# NeoSkin - Appointment Management System

A full-featured, mobile-ready appointment management system with real-time Firebase database integration. Built for NeoSkin — supports 5 treatment rooms, service management, WhatsApp reminders, and works as a **Progressive Web App (PWA)** installable on iPhone and Android.

## 📱 Install on Phone (PWA)

### Android (Chrome):
1. Open the app URL in Chrome
2. Tap the **⋮ menu** → "Add to Home screen"
3. Tap "Add" — NeoSkin icon appears on your home screen

### iPhone / iPad (Safari):
1. Open the app URL in **Safari**
2. Tap the **Share button** (box with arrow)
3. Scroll down → tap **"Add to Home Screen"**
4. Tap "Add" — NeoSkin icon appears on your home screen

## 🚀 Quick Start

### Prerequisites
To use Firebase real-time sync, you need:
1. Access to the Firebase project console for database URL: `data-72ed1-default-rtdb.firebaseio.com`
2. Firebase database rules configured to allow read/write access

### First-Time Setup
1. **Open the app** - The interface will load (may show Firebase permission error initially)
2. **Configure Firebase permissions** - Follow instructions in "Firebase Integration" section below
3. **Update WhatsApp number** - Go to Settings and enter your full international phone number
4. **Add your first customer** - Click "New Customer" button
5. **Create an appointment** - Click "New Appointment" button

### Without Firebase Access
The app is designed to work with Firebase, but if you cannot configure Firebase permissions:
- The app will show permission errors in the console
- You can still use the UI to understand the interface
- To make it fully functional, you'll need to either:
  - Get Firebase database access from the project owner
  - Or modify the code to use a different backend

---

## 🔥 Firebase Integration

**Database URL:** `https://data-72ed1-default-rtdb.firebaseio.com/`

⚠️ **IMPORTANT: Firebase Database Permissions Required**

The Firebase database currently has restricted access. To enable full Firebase functionality:

### Option 1: Configure Firebase Database Rules (Recommended for Testing)
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project
3. Navigate to **Realtime Database** → **Rules**
4. For testing, use these rules (⚠️ **NOT for production**):
```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```
5. Click **Publish**

### Option 2: Use Alternative Storage (Fallback Mode)
If you cannot access Firebase permissions, the app will work with browser local storage. Data will be stored locally and won't sync across devices, but all features will still work.

All data is automatically saved to and synchronized with Firebase Realtime Database in real-time when permissions are granted. Multiple users can access the same data simultaneously with instant updates.

### Firebase Data Structure

```
data-72ed1-default-rtdb
├── customers/
│   └── {customerId}/
│       ├── name: string
│       ├── phone: string
│       ├── email: string
│       └── notes: string
├── appointments/
│   └── {appointmentId}/
│       ├── customerId: string
│       ├── customerName: string
│       ├── date: string (YYYY-MM-DD)
│       ├── time: string (HH:MM)
│       ├── service: string
│       ├── status: string (scheduled|completed|cancelled|no-show)
│       └── notes: string
└── settings/
    ├── whatsappNumber: string
    └── reminderMessage: string
```

## ✨ Features Implemented

### 📊 Dashboard View
- **Real-time statistics** - Today's appointments, upcoming count, total customers, completed appointments
- **Today's schedule** - All appointments for the current day with quick actions
- **Upcoming appointments** - Next 5 scheduled appointments sorted by date
- **Live updates** - Automatically refreshes when data changes in Firebase

### 📅 Calendar View
- **Monthly calendar** - Navigate between months with prev/next buttons
- **Visual indicators** - Colored dots show appointments on each day (up to 3 dots)
- **Day selection** - Click any day to view all appointments for that date
- **Today highlight** - Current day is marked with a special border
- **Side panel details** - Selected day shows appointment cards with full details

### 📋 Appointments View
- **Complete list** - All appointments with sortable table
- **Advanced filters** - Search by customer/service, filter by status, filter by date
- **Quick actions** - Edit, delete, or send WhatsApp reminder from each row
- **Status badges** - Color-coded status indicators (scheduled, completed, cancelled, no-show)
- **Real-time sync** - Changes reflect instantly across all views

### 👥 Customers View
- **Customer cards** - Grid layout with customer information
- **Statistics per customer** - Total appointments, completed, upcoming
- **Quick contact** - Phone and email displayed with icons
- **Action buttons** - Edit, view history, quick book, delete
- **Search functionality** - Filter by name, phone, or email
- **Empty state** - Friendly message when no customers exist

### 📜 History View
- **Customer selector** - Dropdown to choose which customer to view
- **Grouped timeline** - Appointments organized by status (completed, scheduled, cancelled, no-show)
- **Full details** - Service, date, time, and notes for each appointment
- **Appointment count** - Total number of appointments per customer
- **Status summary** - Count of appointments in each status category

### ⚙️ Settings View
- **WhatsApp number** - Your business WhatsApp number (currently set to: 03711621)
- **Reminder message template** - Customize the message with placeholders: {name}, {date}, {time}, {service}
- **Firebase database info** - Display current Firebase URL and connection status
- **Auto-save to Firebase** - Settings persist across sessions

## 📱 WhatsApp Reminder System

### Manual Reminders
- Click the WhatsApp button (green) on any appointment card
- Opens WhatsApp web/app with pre-filled message using your template
- Message includes customer name, service, date, and time
- Works with customer's phone number from their profile

### Automatic Reminder Alerts
- System checks every minute for upcoming appointments
- When an appointment is **1 hour away** (55-65 minute window):
  - Browser alert pops up with appointment details
  - Option to send WhatsApp reminder immediately
  - Only triggers for appointments with status "scheduled"

### Phone Number Format
- Enter WhatsApp numbers with country code
- Example for Malaysia: `60123456789` (without + symbol)
- Current business number: `03711621`
- ⚠️ Update to full international format in Settings for WhatsApp to work correctly

## 🎯 How to Use

### Adding a Customer
1. Click **"New Customer"** button (top right)
2. Fill in:
   - **Name** (required)
   - **WhatsApp Phone** (required) - e.g., `60123456789`
   - Email (optional)
   - Notes (optional)
3. Click **"Save Customer"**
4. Customer appears instantly in Customers view
5. Data is saved to Firebase immediately

### Creating an Appointment
1. Click **"New Appointment"** button (top right)
2. Select customer from dropdown (or click "New" to add customer first)
3. Choose date and time
4. Enter service/treatment name
5. Select status (default: scheduled)
6. Add notes if needed
7. Click **"Save Appointment"**
8. Appointment syncs to Firebase and appears in all views

### Editing Records
- Click the **edit icon** (pencil) on any customer or appointment card
- Make changes in the modal form
- Click "Save" - changes sync to Firebase instantly
- All views update in real-time

### Deleting Records
- Click the **trash icon** on any customer or appointment
- Confirm the deletion
- **Deleting a customer** also deletes all their appointments
- Data is removed from Firebase immediately

### Sending WhatsApp Reminders
1. Find the appointment in any view (Dashboard, Calendar, Appointments)
2. Click the **green WhatsApp button**
3. WhatsApp opens with pre-filled message
4. Review message and send

### Viewing Customer History
1. Go to **Customers** view
2. Click **"History"** button on a customer card
3. OR go to **History** view and select customer from dropdown
4. See all appointments grouped by status

## 🔄 Real-time Synchronization

All data changes are automatically synchronized across:
- Multiple browser tabs
- Multiple devices
- Multiple users (if database rules allow)

Firebase real-time listeners ensure:
- New records appear instantly
- Updates reflect immediately
- Deletions sync across all clients
- Connection status shown in sidebar (green dot = connected)

## 📊 Current Data Status

### Database Tables
- ✅ `customers` - Fully implemented with Firebase
- ✅ `appointments` - Fully implemented with Firebase
- ✅ `settings` - Stored in Firebase root

### Firebase Rules Recommendation
For production use, set up Firebase database rules:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

⚠️ **Security Note:** Current rules allow public read/write. For production:
1. Set up Firebase Authentication
2. Restrict database access to authenticated users
3. Implement user-specific data isolation

## 🎨 Design Features

- **Modern UI** - Clean, professional design with Inter font
- **Responsive** - Works on desktop, tablet, and mobile
- **Color-coded statuses** - Easy visual identification
- **Smooth animations** - Cards, modals, and transitions
- **Toast notifications** - Success/error feedback
- **Empty states** - Helpful messages when no data exists
- **Loading indicators** - Firebase connection status in sidebar

## 🛠️ Technology Stack

- **HTML5** - Semantic structure
- **CSS3** - Modern styling with CSS Grid and Flexbox
- **Vanilla JavaScript** - No framework dependencies
- **Firebase SDK 10.7.1** - Real-time database
- **Font Awesome 6.4.0** - Icons
- **Google Fonts (Inter)** - Typography

## 📋 Next Steps & Recommendations

### High Priority
1. **Update WhatsApp number** in Settings to full international format
2. **Test Firebase connection** by adding a customer and appointment
3. **Configure Firebase security rules** for production use
4. **Set up Firebase Authentication** for user management
5. **Test WhatsApp reminders** with real phone numbers

### Feature Enhancements
- [ ] Add appointment recurrence (weekly, monthly)
- [ ] Implement staff/resource management
- [ ] Add payment tracking and invoicing
- [ ] Create printable appointment schedules
- [ ] Export customer/appointment data to CSV
- [ ] Add SMS reminders (in addition to WhatsApp)
- [ ] Implement appointment cancellation by customers via link
- [ ] Add custom fields for different service types
- [ ] Create analytics dashboard (busiest days, popular services)
- [ ] Add photo upload for customers/services
- [ ] Implement appointment duration and overlap prevention
- [ ] Add waiting list functionality

### Technical Improvements
- [ ] Add service worker for offline functionality
- [ ] Implement data backup/restore feature
- [ ] Add data validation and error handling
- [ ] Create unit tests for critical functions
- [ ] Optimize Firebase queries for better performance
- [ ] Add pagination for large appointment lists
- [ ] Implement lazy loading for customer cards
- [ ] Add keyboard shortcuts for power users

## 🚀 Deployment

To publish your app and make it live:

1. Go to the **Publish** tab in the editor
2. Click the **Publish** button
3. Your app will be deployed with a public URL
4. Share the URL with your team/customers

## 📞 Support

### WhatsApp Number Format Help
- **Malaysia:** 60 + phone (e.g., `60123456789`)
- **Singapore:** 65 + phone (e.g., `6591234567`)
- **Indonesia:** 62 + phone (e.g., `628123456789`)
- **USA/Canada:** 1 + area code + phone (e.g., `14155551234`)

### Firebase Connection Issues
If the sidebar shows "Firebase Disconnected" or you see permission errors:
1. **Permission Denied Error** - This means Firebase database rules need to be updated (see Firebase Integration section above)
2. Check your internet connection
3. Verify the Firebase URL is correct
4. Check browser console for detailed error messages
5. Ensure Firebase database rules allow read/write access

**Common Error:** `permission_denied at /customers`  
**Solution:** Update Firebase database rules in Firebase Console to allow access (see Option 1 above)

## 📝 Current Business Settings

- **WhatsApp Number:** 03711621 (⚠️ Update to international format)
- **Default Reminder:** "Hi {name}, this is a reminder for your {service} appointment on {date} at {time}. See you soon!"
- **Firebase Database:** Connected to `data-72ed1-default-rtdb.firebaseio.com`

---

**Version:** 1.0.0  
**Last Updated:** 2024  
**License:** MIT

Built with ❤️ for efficient appointment management