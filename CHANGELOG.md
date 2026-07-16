# Changelog

Detailed changelog of [Astronomical Clock](https://AstronomicalClock.eu/). You'll find a [short summary](./WHATSNEW.md) of the latest changes here.

*This browser/PWA edition prioritises speed and low resource usage. It uses a lightweight astronomy engine instead of Skyfield/DE440, resulting in minute-level precision instead of the sub-second precision of the Android version.*

---

> ## Known issues
> 
> - The mobile back button is currently not supported correctly in the PWA and may leave a black screen

---

## [1.0.3.38] - 2026-07-16 (Realistic stars)

### Added
- Stars in the Telescope design are now realistic instead of symbolic: B-V based colours, magnitude-scaled cores, dark/light mode differences
- Original greyscale design added, bug fixes
- 12 more stars added

## [1.0.2.20] - 2026-07-14 (Reduced complexity)

### Changed
- Reduced complexity: Removed unnecessary sky-position caches and global geometry state
- Bug fixes: Prevented a duplicate startup render when a saved automatic location has no valid fix. Simplified startup, background refresh handling. Weather hidden in time control mode
 
## [1.0.2.14] - 2026-07-12 (Performance update)

### Changed
- Speed optimisations ⚡: Solcal, orbit, refresh, startup, weather metadata, and resize

## [1.0.2.13] - 2026-07-12 (Bug fixes)

### Fixed
- Altitudes below the horizon were not correctly compensated by JS Astronomy library for using no refraction below -1° #1.0.1.79
- Favicon as png
- A lot of small bug fixes regarding the translation from py to js

## [1.0.1.70] - 2026-07-05

### Fixed
- Small bug fixes

## [1.0.1.62] - 2026-07-04 (Compacted files)

### Changed
- Code compacted from 480kB to 220kB
- Images compacted from 1MB to 130kB

## [1.0.1.48] - 2026-07-03 (Autotranslations added)

### Added
- Autotranslation languages added

## [1.0.1.15] - 2026-07-03 (Weather added)

### Added
- Weather functionality added (on dial #1.0.1.15) and on data page #1.0.1.37

## [1.0.0.5] - 2026-06-30 (First published)

### Added
- Time control added to move the clock forward and backward in time
- Code optimised
- /info/ pages added

### Fixed
- Images didn't have alpha any more

---

> ## [0.9.0.50] - 2026-06-29
> 
> ### Added
> - Restructured. File size reduced by half through increased use of system fonts and WOFF2 compression
> - CSS restructured
> 
> ## [0.9.0.3] - 2026-06-27
> 
> ### Added
> - Dial and pages now match the APK, some text have not been updated yet
> - Some features are still missing, including: Time control, Design selection, Weather, and Alarms
> 
> ## [0.0.1] - 2026-06-24
> 
> ### Added
> - The dial is working

---

> *All notable changes to this project will be documented in this file (tags: Added, Changed, Deprecated, Removed, Fixed, Security). The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html) plus a revision number. - Risk-based categorisation applies: **Added** introduces the highest risk of new errors, **Changed** usually stabilises behaviour, **Fixed** improves stability.*

---
