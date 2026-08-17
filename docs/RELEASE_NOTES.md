# Metrum Genie — Release Notes

**Version 1.0.0 | August 2026 | Initial Release**

Welcome to Metrum Genie. This is the first release, so everything below is new. For a
detailed, screen-by-screen walkthrough of how to use each feature, see the
[Feature Guide](./FEATURE_GUIDE.md).

---

## What's New

### Lab Setup
- Register your lab as a central profile for all locations, equipment, zones, and team members.
- Organize your lab into physical Locations (e.g. "Embryology Room", "ICSI Station").
- Register Equipment (incubators, fridges, CO₂ cabinets, etc.) and environmental Zones, each with its own live digital record.
- Define measurement Parameters (Temperature, CO₂, Humidity, etc.) with custom Low and High Threshold values that drive both alarms and reports.
- Bind Metrum Genie sensors (**MG-TM**, **MG-GASCO2**, **MG-LAB1**) by entering a serial number or scanning the sensor barcode.

### Real-Time Monitoring
- A dashboard showing active alerts, notifications, and quality-control status at a glance.
- A unified view of all your Zones, Equipment, and Sensors, with live parameter readings and alarm status on every card.
- A detailed view for any asset, including live readings, a historical trend chart (from 5 minutes up to 1 year), and the sensor currently feeding it.
- Continuous data logging — every sensor reading is recorded once per minute and kept as a permanent record.
- If a sensor goes temporarily offline, its last known reading stays visible with a clear "last seen" time.

### Alarms
- Automatic alarm detection the moment a reading crosses a configured threshold, with visual and audible alerts.
- Enable or disable alarms individually per parameter or asset.
- Configurable silence timeouts (1 minute up to 1 hour) and separate acknowledgement grace periods.
- Two alarm tone options, with sound and vibration independently switchable.
- A quick-silence button available from anywhere in the app.
- Every alarm's full history — trigger, duration, who acknowledged it and when — is preserved for audit purposes.

### Reports
- Three report types: Quick Report, Custom Report, and Export Logs (data and alarm).
- Every report gets a unique, traceable ID automatically.
- Editable title and remarks before saving.
- Built-in statistics — Min, Max, Average, and Uptime — calculated automatically for every parameter.
- Save, then share reports instantly by email, individually or in bulk.
- Export any report as PDF or CSV.
- Filter and search your report history by type and date.

### Roles & Access Control
Team members are currently assigned one of two roles, each with a different level of access:

| Role | Access Level |
|---|---|
| **Lab Director** (Owner) | Full control — the highest authority on the account |
| **User** | Standard view and operate access |

Only Lab Director can delete team members, remove locations, or edit user profiles. Deleting the Lab Director account itself requires password confirmation and an ownership transfer, so the lab account can never be accidentally locked out.

### Device & Console Settings
- Connect to Wi-Fi, including secured WPA2 networks, directly from within the app.
- Switch between Dark and Light theme.
- Adjust screen brightness, including adaptive brightness.
- Control alarm and notification volume.
- Set screen timeout to your preference.
- Timezone is detected automatically on setup and after connecting to a new network — or set it manually if your lab operates across regions.

### Team Onboarding
- A guided first-time setup wizard walks you through creating your lab and setting a lab PIN.
- Manage multiple team members under one lab account, each with their own role and profile.
- Secure, cloud-based authentication for every account.
- New users joining an existing lab need the lab PIN, adding an extra layer of protection.

### Offline Reliability
- The app works fully offline once your lab is set up — sensor monitoring and data logging continue without an internet connection.
- Internet is only needed for signing in, license management and installing app updates.

---

## Known Issues

- **Run QC** is not yet available in this release and currently shows a "Coming Soon" notice. It will be enabled in a future update.
- **Alarm Silence FAB** is yet to be implemented on the menu and settings screens. Currently it is only available on the My Lab and Reports screens.

---

## Platform Information

| Detail | Value |
|---|---|
| **Version** | 1.0.0 (Build 20) |
| **Release Date** | August 2026 |
| **Platform** | Android |
| **Connectivity** | Direct Wireless Communication + Wi-Fi |
| **Data Storage** | Local on-device (offline-capable) |
| **Internet Requirement** | Required for sign-in and app updates only |
| **Offline Operation** | Fully supported — sensor measurements continue without internet |
| **App Updates** | Managed updates ensure your device always runs the latest validated version |

---

*For technical support, contact the Metrum Genie team at VeroxLabs.*