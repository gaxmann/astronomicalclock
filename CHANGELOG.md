# Changelog

Detailed changelog of [Astronomical Clock](https://AstronomicalClock.eu/). You'll find a [short summary](./WHATSNEW.md) of the latest changes here.

*This browser/PWA edition prioritises speed and low resource usage. It uses a lightweight astronomy engine instead of Skyfield/DE440, resulting in minute-level precision instead of the sub-second precision of the Android version.*

---

> ## Known issues
> 
> - The mobile back button is currently not supported correctly in the PWA and may leave a black screen

---

## [1.1.1.22] - 2026-08-07 (Weather View)

### Added
- New Weather View, bringing the 2016 "Weather Clock" concept into Astronomical Clock #1.1.1.1
- Shortcut to weather page: https://sky12.de/?pg=1
- Brightnesses of planets are now shown (missing APK feature) #1.1.1.14
- In Fullscreen mode reset of the clock after 5 min: back to dial, zoom off, time control off
- Code optimised

### Fixed
- Some years didn't have solar data (e.g. 1971) #1.1.1.4
- New weather diagramm now stays visible even when location has changed but no new data were loaded; of course the "fresh sign" disappears #1.1.1.22

## [1.0.5.98] - 2026-08-02 (9d weather)

### Added
- Code optimised #1.0.5.83
- 7d weather now shows separate snowfall
- 9d(+2d) weather instead of 10d. Now with sunshine duration, precipitation bars, a revised temperature grid, and improved week and edge rendering. Dry and windstill icons added. Day-1 and day+9 are now additionally drawn, so half of the line is still shown #1.0.5.74
- Last missing element for telescope design: unobtrusive circle as representation of meteor radiants instead of square symbol #1.0.5.90
- Improved visual detection of shooting stars (considering meteor strength and moon position and illumination)
- Português, Italiano and हिन्दी added (because autotr isn't working too well)

### Fixed
- Openmet: precip now correctly is precip instead of rain
- Star cores are now 10% smaller (too big on Tablets) 

## [1.0.5.23] - 2026-07-31

### Added
- 10-day weather forecast with minimum and maximum temperature graph
- Snow support for weather forecasts

### Fixed
- "rain" value was without snow, changed to precipation

## [1.0.5.7] - 2026-07-29 (7d weather)

### Added
- Weather 7-day trend preview with temperature ranges and rain and wind indicators in one line #1.0.5.1
- In timecontrol time on data page now stops correctly, no Agni-fresh sign during timecontrol #1.0.5.7

## [1.0.4.12] - 2026-07-26 (Improved zoom)

### Added
- Improved zoom: more efficient dial creation, sharper rendering, and higher maximum zoom #1.0.4.1
- Star height markers optimised (for zoom) #1.0.4.7
- Network timeout 5s #1.0.4.12
- Bug fixes (solc memory leak)

## [1.0.3.78] - 2026-07-24

### Changed
- Weather diagram now uses continuous scaling and better min/max handling #1.0.3.67
- Js built now with esbuild instead of Terser

## [1.0.3.53] - 2026-07-19

### Added
- Persistent location and altitude cache added 

## [1.0.3.46] - 2026-07-18

### Added
- Link to rain radar displayed when it rains
- Only stars that are sometimes visible will be displayed

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
- Bug fixes #1.0.1.70
- Favicon as png
- A lot of small bug fixes regarding the translation from py to js

## [1.0.1.62] - 2026-07-04 (Compacted files)

### Changed
- Code compacted from 480kB to 220kB
- Images compacted from 1MB to 130kB

## [1.0.1.48] - 2026-07-03 (Weather overview)

### Added
- Weather functionality added (on dial #1.0.1.15) and on data page #1.0.1.37
- Autotranslation languages added
- Functionality now mainly matches the APK

## [1.0.0.5] - 2026-06-30 (First published)

### Added
- Time control added to move the clock forward and backward in time
- Code optimised
- /info/ pages added

### Fixed
- Images lost alpha channel

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
> - Dial and pages now match the APK
> - Some features are still missing, e.g. Time control, Design selection, Weather, Alarms
> 
> ## [0.0.1.40] - 2026-06-24
> 
> ### Added
> - The dial is working

---

> *All notable changes to this project will be documented in this file (tags: Added, Changed, Deprecated, Removed, Fixed, Security). The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html) plus a revision number. - Risk-based categorisation applies: **Added** introduces the highest risk of new errors, **Changed** usually stabilises behaviour, **Fixed** improves stability.*

---
