# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0+20] - 2026-08-11

### Added
- **QC Hub**: Added an overlay to the QC hub displaying "feature coming soon" text.
- **Time & Location**: Introduced automatic time zone detection that triggers when a user first starts the app or connects to WiFi.
- **Database Migrations**: Implemented new database migration scripts to transition the schema from v0.16.0+16 to current version. Added a dedicated view to display fatal errors if a database migration fails.
- **Alarms**: Added dropdown selections in the alarm manager to configure alarm silence timeouts and acknowledgement grace periods. Introduced an option to select specific alarm tones.
- **Reports**: Implemented a new 'Share Report' button that only becomes visible after a report is saved. Reports now automatically generate an ID in the format MGRLLLYYMMDDXXXX.
- **UI Components**: Added an empty state content display for both zone and equipment cards. Added extra horizontal lines to the line chart widget to represent minY, maxY, and set-point threshold lines.
- **Roles**: Added an administrative privilege check to restrict user deletion, location deletion, and profile editing strictly to users with Admin or Owner roles.

### Changed
- **Terminology**: Renamed "Equipment" to "Assets" across the Quick Report wizard, Custom Report wizard, and Export Logs screens. Changed the "Export Data" section name to "Export Logs" within the Report Hub.
- **Parameter Settings**: Changed parameter labeling by replacing "Minimum" and "Maximum" with "Low Threshold" and "High Threshold," respectively.
- **Navigation & Layout**: Changed the default initial index of the My Lab screen to display the equipment tab upon opening. Modified the Lab Profile view by replacing the old chip button group with a tab bar for locations and users.
- **User Roles**: Updated the user profile view to display the lab role dynamically based on the current user, mapping the "Owner" role to display as "Lab Director".
- **Alarms**: Renamed the "alert manager" folder and page route to "alarm manager".

### Refactored & Enhanced
- **Global Navigation**: Refactored application-wide top app bars using a new `MGAppBar.simple` constructor to ensure clean UI consistency across menus, authentication pages, reports, and profile screens.
- **Branding**: Upgraded the splash screen, welcome, login, and signup pages to integrate the finalized "Genie" logo with updated dark green color theming.
- **Security**: Enhanced the KIOSK mode exit mechanism by requiring a security code check and introducing an exit trigger timeout to prevent accidental application exits. Added additional deletion protection for Lab Owner accounts, which now require password reconfirmation and ownership transfer checks.
- **Forms & Inputs**: Refactored equipment and zone parameter modals using updated `MGFormTextField` and `MGDropDownFields` for better input handling, auto-focusing, and UI consistency.
- **Reports**: Refactored the Report Document view to allow users to edit the Report Title and Remarks directly.
- **Equipment Control**: Refactored the Equipment and Zone profile views to feature dedicated "Activate" and "Deactivate" action buttons instead of the previous monitor toggle switches.

### Fixed
- **Sensors**: Fixed a bug in the Sensor Manager where the "All Types" parametric filter failed to work due to a typo. Resolved a race condition within the change sensor workflow that previously conflicted with the alarm monitoring coordinator.
- **Hardware Integration**: Fixed an OS BLE (Bluetooth Low Energy) throttling bug by wrapping `bluetoothAdapter.enable()` in `MainActivity.kt` and transitioning the BLE Data Source to a Permanent Continuous Scan.
- **Reports**: Fixed an issue in the Custom Report module where statistics values were missing by explicitly defaulting the `includeStatistics` variable to `true`. Fixed a bug where report statuses failed to update to 'Reviewed' immediately after saving.
- **Alarms**: Corrected the Alarm Log report so the "Acknowledged By" field correctly displays the user's name rather than their system ID.
- **Inputs**: Fixed floating-point calculation errors for parameter values and enabled input formatters to correctly accept signed values for thresholds.
- **UI & Navigation**: Fixed incorrect routing that navigated to the My Lab screen after deleting a Zone or Equipment. Removed a buggy `toTitleCase` function implementation that broke capitalization on whole words (e.g., rendering "iPhone" as "I Phone").

### Removed
- **Sensors**: Removed legacy parameter type filtering that only supported single-channel sensors, replacing it with channel parameter type-based filtering.
- **Alarms**: Disabled and removed the auto-alarm acknowledgement behavior that previously triggered during the `delete_sensor` use case or when alarms were manually disabled.
- **UI Components**: Removed the "Check Point Restoration" feature card from the Data Storage Settings view. Removed outdated tutorial placeholder screens and their associated path registrations.

---

## [0.16.0] - 2026-08-10 (Intermediate release without a DB change for Database Migration Baseline)

### Added
- **Database Migration Baseline**: Introduction of the database migration protocol. This release contains `Database Version 1`

### Refactored
- **Tutorial Section**: Simplified to have the tutorial flow as Wecome -> Create Lab -> Enter Lab pin -> Tutorial Complete -> Dashboard.

---

## [0.15.0] - 2026-07-20

### Added
- **Timezone Management**: Added timezone configuration options under Console Settings, allowing users to manually select their preferred timezone or auto-detect it from the host device.

### Refactored
- **App Lifecycle & Services**: Removed redundant background service initializations in `metrum_genie_app.dart` and cleaned up unused QC service bootstrap code to optimize startup efficiency.

---

## [0.14.0] - 2026-07-14

### Added
- **User Profile Integration**: Updated the primary Dashboard to display real, dynamic user profile details.

### Refactored
- **Zone Architecture**: Cleaned up the temporary ESHRE deployment workaround by properly decoupling Zone Management from General Equipment structures into an isolated module.

---

## [0.13.0] - 2026-07-10

### Added
- **Dashboard & Alerts**: Integrated live notification hub and active alert banners (e.g., reminding users when Lab Setup is incomplete).
- **Alarm System Revamp (Phase 1)**: Added a convenient floating action button (FAB) for direct alarm interactions and silenced warning sounds.
- **Equipment Management**: Enhanced equipment mapping frontend and backend architecture.

### Refactored
- **Parameter & Card Displays**: Persistent parameter readings on equipment cards now fall back smoothly to the last recorded value.
- **Debug Logging**: Wrapped console print statements inside standard debug wrappers to prevent logs in production release builds.
- **Hardware Integrations**: Reverted the temporary offline sensor registration workaround used during ESHRE.
- **JSON Engine**: Upgraded JSON response structures for compliance protocol calculation results.

### Fixed
- **Sensor Discovery**: Increased scanning duration during sensor registration to resolve intermittent detection dropouts.
- **Device Compatibility**: Removed MAC address restrictions for `MG-TM` modules.

### UX & Polishing
- Standardized and enhanced loading indicators across the Equipment Monitor screens.
- Capped maximum scroll heights on Sensor and Equipment Manager views to prevent UI overflow issues.
- Fixed layout and styling issues on the Equipment Profile screen's top App Bar.

---

## [0.12.0] - 2026-07-07

### Changed
- Updated the default user profile avatar across the app to privacy-compliant vector graphics.

---

## [0.11.0] - 2026-07-06

### Added
- **Dashboard Overview**: Activated the primary Dashboard view to display live compliance summaries and lab metrics.
- **Compliance Workflow**:
  - Completed dedicated views for Equipment Profiling, Equipment Monitoring, and equipment naming inside the QC Hub.
  - Drafted initial layout and structures for Equipment Mapping.

### Refactored
- **Equipment Registration**: Set monitoring toggle to `true` by default upon registering new equipment.
- **Compliance Visualizations**: Updated compliance run charts with distinct pass/fail color indicators for quick inspection.

---

## [0.10.0] - 2026-07-06

### Added
- **Database Utilities**: Introduced a Database Factory Reset tool for clearing local persistent state during testing and maintenance.

### Fixed
- **Datalogging & Units**:
  - Fixed hardware SD card data logging reliability.
  - Corrected VOC sensor unit conversion from `ppm` to `ppb`.
  - Merged overlapping multi-channel sensor data logs created during concurrent compliance task runs.
- **UI & Stability**:
  - Resolved a UI scrolling crash inside the Compliance Wizard checklist view.
  - Redesigned and upgraded graph renderings and results cards in Compliance Runs.

---

## [0.9.0] - 2026-07-06

### Fixed
- Resolved a critical issue preventing database configuration backups from restoring properly.

---

## [0.8.0] - 2026-07-06

### Added
- Emergency configuration restore point specifically tailored for ESHRE deployment datasets.

---

## [0.7.0] - 2026-07-06

### Added
- **Zone Management**: Introduced dedicated Zone Cards to the "My Lab" dashboard for improved spatial organization.
- **Offline Sensor Registration**: Enabled registration capability for offline or disconnected hardware modules.

### Refactored
- Increased the sensor offline detection threshold timer to **5 minutes** to prevent transient disconnection alerts.

---

## [0.6.0] - 2026-07-05

### Added
- Emergency ESHRE release featuring automated **Configuration Restore** functionality.
- Initial release of Compliance Tasks and Runs modules within the platform.

### Refactored
- Overhauled the **QC Hub** dashboard to display live compliance tasks and ongoing runs.

---

## [0.5.0] - 2026-07-02

### Added
- QC wizard UI for 'Equipment Calibration' according to the new design and business requirement with a multi-step form wizard view.
- Functionality to parse data from MGLAB1 modules by fixing an existing parsing issue.


### Refactored
- Data logging architecture to save a single data frame for multi channel sensors and link to multiple parameter data logs.
- Sensor selection modals to display suitable sensors in the format <`sensorName`>-<`channelName`> for selection while preventing selection of sensors that do not contain channels with suitable parametric type.
- BLE parser related to MGLAB1 modules to match device firmware.


### CleanUp
- Removed code and files related to live meter concept which is not in the business requirement now.
- Removed description, location and parametric type from sensor model.

---

## [0.4.0] - 2026-06-27

### Added
- Multi channel data ingestion for MG-TM, MG-GASCO and MG-LAB1 modules
(Basic data path and history buffers implemented. Further logic updates may be required)

### Refactored
- The sensor card to implement multi channel data display
- Sensor profile to show correct sensor icon for the selected sensor.

---

## [0.3.0] - 2026-06-24

### Added
- Forced app updates feature to push updates to devices.

### Refactored
- Bottom Navigation menu to have Dashboard, My Lab, Run QC and Reports (Dashboard will be functional in the next release)
- My lab tab to represent a digital twin of the lab. All Equipments and sensors registered to the lab are visible in this tab.
- BLE whitelisting of sensors to an automatic whitelisting method instead of manually whitelisting for different tasks : QC, Live Meter, Lab Monitor, etc.

---

## [0.2.0] - 2026-04-01

### Added
- **Architectural Blueprints**: Initialized `knowledge/RELEASE_GUIDE.md` and `knowledge/VERSIONING.md` to define company release standards.
- **Portable Keystore System**: Successfully migrated from absolute local paths to project-relative paths for signing, enabling seamless multi-developer collaboration.
- **Keystore Generation Utility**: Added official `keytool` instructions for creating and verifying signing keys within the repository.

### Fixed
- **JVM Memory Crash**: Resolved the `Gradle build daemon disappeared unexpectedly` error by optimizing `org.gradle.jvmargs` for systems with 7GB RAM.
- **Cross-Drive Build Failure**: Fixed the `this and base files have different roots` error by relocating the `PUB_CACHE` to the same physical drive as the project.
- **Security Hardening**: Standardized `.gitignore` to recursively exclude all `build/` directories and protect sensitive signing files (`*.jks`, `key.properties`).
- **Signature Verification**: Implemented and verified the `apksigner` formal check for release builds.

---

## [0.1.0] - Prior to 2026-04-01

### Added
- **Core Laboratory Management**:
  - Full lab and equipment setup/configuration modules.
  - Advanced Quality Control (QC) task execution and monitoring.
  - Real-time data logging and event tracking engine.
  - Automated report generation and email distribution system.
- **Hardware & Communication**:
  - BLE Sensor Integration (`flutter_blue_plus`) for real-time device monitoring.
  - QR Code scanning capability for rapid equipment/sensor identification.
  - Local WiFi and network configuration modules.
- **Data & Security**:
  - High-performance local persistence using **Isar Database**.
  - Secure data backup and restoration system.
  - Centralized state management architecture using **Riverpod**.
- **Authentication & Onboarding**:
  - Firebase Authentication with Google Sign-In integration.
  - Comprehensive first-time setup wizard and interactive tutorials.
  - Splash screen and Lottie-based micro-animations for enhanced UX.
