# Metrum Genie — Feature Guide

> 📋 See also: [RELEASE_NOTES.md](./RELEASE_NOTES.md) for the versioned changelog of what changed and when.

**Version:** 1.0.0 (Build 20) | **Platform:** Android | **Updated:** August 2026

This guide describes the app as it currently exists — screen by screen, matching the live navigation structure. It is a reference document, not a tutorial. For what changed between versions, see the Release Notes.

---

## Table of Contents

1. [Onboarding & Authentication](#1-onboarding--authentication)
2. [Dashboard](#2-dashboard)
3. [My Lab](#3-my-lab)
4. [Asset Monitor](#4-asset-monitor)
5. [QC Hub (Run QC)](#5-qc-hub-run-qc)
6. [Reports Hub](#6-reports-hub)
7. [App Menu (Secondary Navigation)](#7-app-menu-secondary-navigation)
   - [Lab Configuration](#71-lab-configuration)
     - [Lab Profile](#711-lab-profile)
     - [Equipment Manager & Equipment Profile](#712-equipment-manager--equipment-profile)
     - [Zone Manager & Zone Profile](#713-zone-manager--zone-profile)
     - [Sensor Manager & Sensor Profile](#714-sensor-manager--sensor-profile)
     - [Alarm Manager](#715-alarm-manager)
   - [Settings](#72-settings)
     - [User Profile](#721-user-profile)
     - [License Management](#722-license-management)
     - [Email Configuration](#723-email-configuration)
     - [Console Settings](#724-console-settings)
     - [Backup Data](#725-backup-data)
     - [Software Updates](#726-software-updates)
8. [System Screens](#8-system-screens)
9. [Cross-Cutting Systems Reference](#9-cross-cutting-systems-reference)
   - [Alarm System](#91-alarm-system)
   - [Security & Roles](#92-security--roles)
   - [Offline & Data Logging](#93-offline--data-logging)
   - [Sensor Lifecycle](#94-sensor-lifecycle)

---

## 1. Onboarding & Authentication

### 1.1 Welcome / Onboarding Screen
The first screen shown to any unauthenticated user. Provides entry points to:
- **Log In** to an existing account
- **Sign Up** to create a new account

### 1.2 Login
Standard email and password login via Firebase Authentication. A "Forgot Password" link redirects to the password reset flow.

### 1.3 Sign Up
New account creation with email and password.

### 1.4 Activate License
After authentication, users without an active license are directed here. Enter a license key to activate. Pending licenses display payment instructions.

### 1.5 Enter Lab PIN
Users who are authenticated and licensed but not yet associated with a lab on the current device must enter the lab's PIN. This is the entry gate for joining an existing lab configuration on this phone.

### 1.6 Tutorial (First-Time Setup)
Triggered automatically when a new license is activated and no lab has been registered on the device. The tutorial is a linear, non-skippable flow:

| Step | Screen | Purpose |
|---|---|---|
| 1 | Tutorial Welcome | Introduces the setup wizard |
| 2 | Create Lab | Enter lab name, type, and optional clinic / address |
| 3 | Create Lab PIN | Set the lab's access PIN for device-sharing security |
| 4 | Tutorial Complete | Confirms setup and launches the Dashboard |

After completing the tutorial, the user lands on the Dashboard and the wizard does not appear again on this device.

### 1.7 Wi-Fi Onboarding
A dedicated Wi-Fi connection screen (`/wifi-onboarding`) that can be reached before authentication. When "Continue" is tapped after connecting, the app automatically triggers timezone detection to set the correct local time. This screen is accessible even in forced-update mode.

---

## 2. Dashboard

**Navigation:** Bottom nav → Dashboard (tab 1)

The Dashboard is the app's home screen after login. It is a vertically scrollable feed of contextual sections.

### Sections (top to bottom)

| Section | Always Shown | Content |
|---|---|---|
| **Alerts** | Yes | Active alarm cards or "No active alarms" state. If lab setup is incomplete, shows a "Lab setup incomplete" prompt instead. |
| **Notifications** | Only when notifications exist | Setup reminders, license reminders, software update notices |
| **Pending Sign-Offs** | Yes | QC runs awaiting review and sign-off by the current user |
| **Ongoing QC** | Yes | Actively running QC tasks with progress |
| **Upcoming QC** | Yes | Scheduled QC tasks due today |

### App Bar
- Displays the logged-in user's name and role
- The menu button (⋮) opens the secondary navigation modal

### Alarm Interaction
- When one or more alarms are active, the Alerts card shows the alarm summary with an action button (Silence or Acknowledge depending on state).
- Tapping "Acknowledge" opens the full alarm acknowledgement modal.
- For alarm configuration, see [§9.1 Alarm System](#91-alarm-system).

### Floating Action Button (FAB)
The alarm FAB is **not shown** on the Dashboard. It is shown on all other main tabs (My Lab, QC Hub, Reports Hub) when there are active alarms.

---

## 3. My Lab

**Navigation:** Bottom nav → My Lab (tab 2)

Provides a live digital twin of the lab through a 3-tab interface.

### App Bar
- Shows the lab name and the current date/time
- The menu button (⋮) opens the secondary navigation modal

### Tabs

| Tab | Default | Content |
|---|---|---|
| **Zones** | No | Zone cards with environmental zone name, location, and live parameter values |
| **Equipment** | **Yes** | Equipment cards with asset name, location, and live parameter readings |
| **Sensors** | No | Sensor cards showing last reading, online/offline state, and last-seen time |

Each tab header shows the count of items in that category (e.g. `Equipment (3)`).

### Empty States
When a tab has no configured items, a contextual empty state is shown with a call-to-action button that navigates directly to the relevant manager (Zone Manager, Equipment Manager, or Sensor Manager).

### Zone Cards
Each zone card shows:
- Zone name and location
- Per-parameter value chips (type, value, status color)
- Overall zone alarm status

Tapping a Zone card navigates to the [Asset Monitor](#4-asset-monitor) for that zone.

### Equipment Cards
Each equipment card shows:
- Equipment name and location
- Per-parameter value chips (type, value, status color)
- Overall equipment alarm status

Tapping an Equipment card navigates to the [Asset Monitor](#4-asset-monitor) for that equipment.

### Sensor Cards
Each sensor card shows:
- Sensor name
- Last reading and its timestamp
- Online/offline indicator

Tapping a Sensor card navigates to the Sensor Profile.

### Floating Action Button (FAB)
The alarm FAB is shown on My Lab when there are active alarms. See [§9.1 Alarm System](#91-alarm-system).

---

## 4. Asset Monitor

**Navigation:** Tap any Zone or Equipment card in My Lab

The Asset Monitor is the detailed live view for a single piece of equipment or an environmental zone. The same screen serves both asset types.

### App Bar
- Title: asset name
- Subtitle: asset location
- Settings icon: navigates to the asset's profile in Equipment Manager or Zone Manager

### Fixed Content Area

**Alarm Acknowledge Button**
- Shows count of active alarms + count of past unacknowledged alarms
- Tapping opens the Alarm Acknowledgement modal (see [§9.1](#91-alarm-system))

**Parameter Selector**
- Horizontal scrollable row of chip buttons, one per configured parameter
- Each chip shows: parameter type label, current value, and status color
- An Add (+) button at the end opens the Add Parameter modal

### Scrollable Content Area

**Current Reading Window**
- Large, prominent display of the currently selected parameter's value, unit, and status

**Trend Chart**
- Line chart of the selected parameter's historical readings
- Time range selector (chip row): Live | H | D | W | M | Y
- When alarms are enabled for the parameter: Low Threshold and High Threshold lines are drawn on the chart
- Chart color reflects current alarm status

**Assigned Sensor Tile**
- Shows the sensor currently assigned to feed the selected parameter
- Displays sensor name and last-seen timestamp
- Swap button (sync icon) opens the Change Sensor modal

### Data Logging
All readings from asset-bound sensors are logged automatically once per minute. Historical data is available immediately in the trend chart for any configured time range.

---

## 5. QC Hub (Run QC)

**Navigation:** Bottom nav → Run QC (tab 3)

**This section is not yet accessible in v1.0.0.** The screen displays a "Coming Soon" overlay. The underlying functionality exists in the codebase and will be enabled in a future release.

When available, the QC Hub will provide:

### Action Grid
Six task type buttons in a 3-column grid:

| Type | Description |
|---|---|
| **Profiling** | Recovery Profile, Stability Profile, Vulnerability Profile |
| **Validation** | Set Point Validation |
| **Calibration** | Quick Offset Calibration, Smart Offset Calibration |
| **Mapping** | Standard Mapping, Custom Mapping |
| **Monitoring** | Simple Threshold Monitoring |
| **Custom** | Custom SOP (marked Coming Soon within the grid) |

---

## 6. Reports Hub

**Navigation:** Bottom nav → Reports (tab 4)

The Reports Hub is the central screen for generating, viewing, and distributing reports.

### App Bar
- Title: "Reports Hub" with subtitle "Audit-ready reports & logs"
- The menu button (⋮) opens the secondary navigation modal

### Action Grid
Three action buttons in a 3-column grid:

| Button | Navigates to |
|---|---|
| Quick Report | Quick Report wizard |
| Custom Report | Custom Report wizard |
| Export Logs | Export Logs wizard |

### Reports List
Below the action grid, a scrollable list of all previously saved reports. Each item shows:
- Report title and type label
- Date and time of generation

**Filtering:** A filter bar allows filtering by report type and by date. A "Clear Filter" action removes all active filters.

**Selection Mode:** Long-pressing any report tile enters selection mode (checkboxes appear). In selection mode:
- **Delete** selected reports
- **Share** selected reports via the Share modal

### Floating Action Button (FAB)
The alarm FAB is shown on Reports Hub when there are active alarms.

### Report Wizards

**Quick Report**
A step-by-step wizard for generating a rapid summary report for selected assets and parameters.

**Custom Report**
A step-by-step wizard to generate an aggregated report for selected assets and parameters over a user-selected date range. Statistics (Min, Max, Average, Uptime) are included automatically.

**Export Logs**
A step-by-step wizard to export raw log data.

### Report Document View
After a report is generated or when an existing report is tapped, the Report Document view opens.

Features:
- **Editable title and remarks** — tap to edit inline before saving
- **Unique Report ID** — auto-generated in the format `MGRLLLYYMMDDXXXX`
- **Save** — saves the report to the device and reveals the Share button
- **Share** — send the saved report by email (configured in Email Configuration)
- **Export to PDF / CSV** — download the report in your preferred format

---

## 7. App Menu (Secondary Navigation)

**Navigation:** Tap the ⋮ menu button in the app bar of any main screen

A bottom sheet modal with two sections: Lab Configuration and Settings.

---

### 7.1 Lab Configuration

#### 7.1.1 Lab Profile

View and manage all core lab metadata in a single screen. The screen uses a tab layout:

**Header (always visible)**
- Lab profile picture
- Lab type badge (editable when in edit mode)
- Lab name, clinic name, and address (all editable)
- Lab PIN (viewable/editable by Admin and Lab Director roles only)

**Tabs**

| Tab | Content |
|---|---|
| **Locations** | List of all physical locations defined in the lab. Add, rename, or delete locations. |
| **Users** | List of all users associated with the lab. Each user row shows their name, role, and delete option. |

**Role restrictions:** Editing lab info, adding/removing locations, and deleting users are restricted to users with Admin or Lab Director (Owner) roles. See [§9.2 Security & Roles](#92-security--roles).

---

#### 7.1.2 Equipment Manager & Equipment Profile

**Equipment Manager** lists all registered equipment in the lab.

Actions per equipment item:
- View the Equipment Profile
- Add new equipment (registration form: name, type, location)

**Equipment Profile** (reached by tapping an equipment item)

- Edit equipment name, type, and location
- **Activate / Deactivate** the equipment (dedicated action buttons)
- Manage parameters: add, configure (Low Threshold, High Threshold, alarm enable), or remove
- Delete equipment (restricted to Admin and Lab Director roles)

---

#### 7.1.3 Zone Manager & Zone Profile

**Zone Manager** lists all registered environmental zones.

**Zone Profile** (reached by tapping a zone item)

- Edit zone name and location
- **Activate / Deactivate** the zone
- Manage parameters: add, configure, or remove
- Delete zone (restricted to Admin and Lab Director roles)

Zone management is structurally identical to Equipment management. Zones are differentiated in code by an `isZone` flag and display with distinct card styles.

---

#### 7.1.4 Sensor Manager & Sensor Profile

**Sensor Manager** lists all registered sensors.

Actions:
- Register a new sensor (by serial number entry or barcode scan)
- Filter sensors by parametric type
- View individual Sensor Profiles

**Sensor Profile** (reached by tapping a sensor's serial number)

- Sensor name and automatically identified type (MG-TM, MG-GASCO2, MG-LAB1)
- Correct sensor type image displayed automatically
- Online/offline status
- List of parameters the sensor is currently assigned to

**Sensor type display:** The Sensor Manager and Sensor Profile display distinct visual images for each hardware model family.

---

#### 7.1.5 Alarm Manager

Global alarm configuration. All settings here apply across the entire lab. For per-parameter alarm enable/disable, use the Equipment/Zone Profile.

| Setting | Options | Description |
|---|---|---|
| **Alarm Sound** | On / Off | Enable or disable auditory alarm indication globally |
| **Vibration** | On / Off | Enable or disable vibration alarm feedback globally |
| **Alarm Tone** | Alarm Tone 1 / Alarm Tone 2 | Choose which audio tone plays for active alarms |
| **Silence Timeout** | 1 min, 2 min, 5 min, 10 min, 15 min, 30 min, 1 hour | Duration the silence button suppresses alarm audio |
| **Acknowledgement Timeout** | 1 min, 2 min, 5 min, 10 min, 15 min, 30 min, 1 hour | Duration alarm audio stays silent after a user acknowledges an alarm, even if the breach continues |

---

### 7.2 Settings

#### 7.2.1 User Profile

Displays the current user's account details: display name and email. Available sub-actions:
- **Change Username**
- **Change Password**
- **Delete Account** (with confirmation — see [§9.2](#92-security--roles) for Owner account protection)

---

#### 7.2.2 License Management

Shows the status of the current Metrum Genie license:
- License key
- Status (Active / Pending)
- Validity period

If a license is pending payment, payment instructions are shown.

---

#### 7.2.3 Email Configuration

Configure the email addresses used when sharing reports:
- **Primary Recipient** — the main "To" address
- **CC** — carbon copy address(es)
- **BCC** — blind carbon copy address(es)

These addresses are pre-filled when a report is shared from the Report Document view or the Reports Hub.

---

#### 7.2.4 Console Settings

The Console Settings screen replaces Android system settings for device management. All sections are accessible without logging in (the screen is reachable before authentication).

**Connectivity**
- Wi-Fi toggle (enable/disable)
- Network list: scan, select, and enter password to connect
- Connected network shown with a checkmark
- "Refresh Networks" button to rescan

**Display & Theme**
- Theme toggle: Light / Dark mode
- Adaptive Brightness toggle
- Manual Brightness slider (shown when Adaptive Brightness is off)

**Date & Time**
- Timezone: auto-detect or manual selection from a timezone list
- Automatic detection triggers on first launch and when connecting to Wi-Fi

**Sound & Feedback**
- Volume level slider

**Screen Timeout**
- Screen sleep timer configuration

**Kiosk Mode Exit**
Long-pressing the "Powered by VeroxLabs" footer text at the bottom of the screen initiates a timed exit sequence. After the hold timer expires, a security code confirmation dialog appears. This is a device management feature — exiting kiosk mode permanently removes device ownership and requires re-provisioning.

---

#### 7.2.5 Backup Data

Three operations available:

| Section | Description |
|---|---|
| **Export** | Export a full backup of all local lab data to a file |
| **Import** | Restore a previously exported backup file |
| **Reset** | Clear all local lab data (factory reset of local storage) |

---

#### 7.2.6 Software Updates

Displays the current installed app version and checks for available updates.

- **Forced Updates**: If a mandatory update is published, the app intercepts all navigation and redirects users to this screen (or the Forced Software Update screen) until the update is installed. Wi-Fi Onboarding and Console Settings remain accessible during a forced update.
- **Manual Update Check**: Users can also proactively check for updates here.

---

## 8. System Screens

### Fatal Error Screen
If the database migration fails during app startup, a fatal error screen is displayed instead of the normal app flow. The screen:
- Explains that a critical issue was encountered during app data updates
- Provides a "Copy Error Details" button to copy technical details to the clipboard for support
- Prompts the user to contact support

This screen cannot be dismissed — the user must contact VeroxLabs support to resolve.

### Forced Software Update Screen
Shown when a mandatory app update is available. Blocks all other navigation until the update is applied. Wi-Fi Onboarding and Console Settings remain accessible so the user can connect to the internet to download the update.

---

## 9. Cross-Cutting Systems Reference

These systems span multiple screens. Screen sections link here rather than restating the full behavior.

---

### 9.1 Alarm System

#### How Alarms Trigger
An alarm activates automatically the moment a sensor reading crosses the configured **Low Threshold** or **High Threshold** for a parameter. Alarms only trigger if alarms are enabled for that parameter.

#### Visual Indication
- The Alerts section on the Dashboard shows an alarm card with the alarm summary
- The Asset Monitor's Alarm Acknowledge Button shows the count of active alarms in red
- Parameter chips in the Asset Monitor and My Lab cards reflect alarm status via color
- Trend chart threshold lines appear in the Asset Monitor when alarms are enabled

#### Auditory & Vibration Indication
- The alarm tone (Alarm Tone 1 or 2) plays when an alarm is active
- Vibration (if enabled) accompanies the auditory alert
- Both can be independently disabled in [Alarm Manager](#715-alarm-manager)

#### Alarm FAB (Floating Action Button)
A floating action button appears on My Lab, QC Hub, and Reports Hub screens (not Dashboard) when there are active alarms. The button's appearance reflects alarm state:
- Tapping when alarms are unsilenced: silences the current alarm sound immediately
- Tapping when alarms are already silenced or acknowledged: opens the Alarm Acknowledgement modal

#### Silence
Pressing the Alarm FAB (or the Silence button in the Alerts card on Dashboard) suppresses alarm audio for the configured **Silence Timeout** duration. After the timeout, the alarm sound resumes if the breach is still active.

Silence timeout options: 1 min, 2 min, 5 min, 10 min, 15 min, 30 min, 1 hour.
Configure in: [Alarm Manager](#715-alarm-manager).

#### Acknowledgement
Acknowledging an alarm logs the event with the user's name and a text comment. After acknowledgement:
- The alarm is marked as acknowledged
- The auditory indication is suppressed for the **Acknowledgement Timeout** duration, even if the breach continues
- The "Acknowledged By" field in Alarm Log reports shows the user's display name

Acknowledgement can be triggered from:
- The Dashboard Alerts card action button
- The Asset Monitor Alarm Acknowledge Button

Acknowledgement Timeout options: same as Silence Timeout.
Configure in: [Alarm Manager](#715-alarm-manager).

#### Alarm Lifecycle Record
Every alarm event is permanently recorded:
- Trigger time and triggering parameter/asset
- Duration
- Which user silenced it and when
- Which user acknowledged it, when, and with what comment
- Resolution time

This record is preserved permanently on the device.

#### Alarm Enable/Disable (Per Parameter)
Each parameter has its own alarm enable/disable toggle. When disabled, threshold lines are not shown in the trend chart and no alarm events are raised even if the sensor reading crosses the threshold.

Configure in: Equipment Profile or Zone Profile.

---

### 9.2 Security & Roles

#### Role Definitions

| Role | Admin Privileges | Notes |
|---|---|---|
| **Lab Director** (Owner) | Yes | Highest authority; cannot be deleted without ownership transfer |
| **Admin** | Yes | Can manage all lab assets, users, and locations |
| **User** | No | Standard operational access |

#### Admin-Restricted Actions
The following actions require Admin or Lab Director (Owner) role:
- Edit lab profile information (name, clinic, address, type)
- Add or delete lab locations
- Delete lab users
- Edit user profiles of other users

#### Owner Account Protection
Deleting the Lab Director (Owner) account requires:
1. Password re-confirmation
2. An ownership transfer check (if a lab is registered under the account, ownership must be transferred first)

This prevents accidental permanent lockout of the lab account.

#### Lab PIN
The lab PIN is a device-level access gate. Any user wishing to access the lab configuration on a new device must enter the PIN. This is in addition to cloud authentication — it prevents unauthorized access via a stolen or shared device. The PIN is set during the tutorial and can be changed in the Lab Profile by Admin and Lab Director roles.

---

### 9.3 Offline & Data Logging

#### Offline Operation
The app operates fully offline once the lab is configured. BLE sensor readings are received and processed without internet access. All parametric data logging continues offline.

Internet is required for:
- Initial authentication (login/signup)
- License validation
- App updates

#### Parametric Data Logging
- All sensor readings assigned to a parameter are logged **once per minute**
- Logs are stored permanently on the device (Isar local database)
- Historical data is available via the Trend Chart in Asset Monitor and via reports

#### Sensor Offline Detection
If a sensor stops transmitting, its last known reading is preserved and displayed in My Lab and Asset Monitor cards with a "last seen" indicator showing the timestamp of the most recent reading.

The offline detection threshold is 5 minutes — a sensor is not flagged as offline until it has been silent for at least 5 minutes, preventing false alerts from transient disconnections.

---

### 9.4 Sensor Lifecycle

#### Sensor Registration
Sensors are registered in Sensor Manager by:
- Entering the serial number manually, or
- Scanning the sensor barcode

After registration, the sensor type is automatically identified from the serial number format. The Sensor Manager and Sensor Profile display the correct image for each hardware model (MG-TM variants, MG-GASCO2, MG-LAB1).

#### Sensor Assignment
Sensors are assigned to parameters within Equipment/Zone Profile or via the Asset Monitor Change Sensor button. A sensor can only feed parameters whose parametric type matches the sensor channel type.

Multi-channel sensors (MG-LAB1, MG-TM) expose individual channels for assignment. Sensor selection shows as `<sensorName>-<channelName>` to distinguish channels.

#### Sensor Reassignment
A sensor can be reassigned from one parameter to another using the swap button in the Asset Monitor. After reassignment:
- New readings from the sensor are added to the new parameter's history
- The old parameter's data history is preserved

#### BLE Scanning
The app operates a permanent continuous BLE scan in the background, receiving data from all registered sensors in range without requiring manual scans.

---

*For technical support, contact the Metrum Genie team at VeroxLabs.*
