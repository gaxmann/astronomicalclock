# Astronomical Clock ☀️

<img src="design/icon.png" width="48" height="48" align="left">***Browser/PWA version of Gordon's Sun Clock* – A single-hand clock with a dial that changes daily, based on the rhythms of nature and the stars. A new way of displaying time in harmony with the seasons**

This repository contains the web implementation of the natural-time sun clock, including local astronomical calculations, offline support, and the canvas-based dial. It is the ongoing web port of the original Android/Python app.

The web version performs all astronomical calculations locally in JavaScript (including VSOP87 and IAU 2000B), and does **not** provide the full Skyfield precision of the Android/Python version (JPL DE440 ephemerides). Some app features are still missing or incomplete, such as sun-based alarms and multiple designs.

## Features

- **Accurate solar positioning**: Within VSOP87 & IAU 2000B limitations (see [Android app](https://github.com/gaxmann/gordonssunclock) for JPL precision)
- **Single-hand design**: Simple, clear, intuitive
- **Location-based**: Adjusts to your coordinates (manual input or location detection)
- **Real-time rise/set**: Sun and Moon rise and set according to their apparent size
- **Installable**: As a progressive web app
- **Offline capable**: No internet required after first setup (PWA)
- **Optional weather overview**: Clear icon-based, drama-free daily outlook
- **Temporal hours clock**: Display of ancient unequal hours (12 day hours & 4 night watches) – e.g. for historians or anyone seeking a deeper connection to historical timekeeping
- **Time travel:** Explore past and future skies, including the sky at your birth
- **Meteor showers:** the eight major streams with search area and radiant  
- **Agnihotra support**: Display precise Agnihotra times with countdown
- **Tablet mode**: Turn a tablet into a permanent wall clock (the Android app may be better suited for this)
- **Languages**: Deutsch, English, Español, Français, Русский, 中文 plus some autotranslated languages
- **Free & private**: Free of charge, no ads, privacy-friendly

Link to Astronomical Clock: https://astronomicalclock.eu/  
**Short link:** https://sky12.de/

Main Android repository: https://github.com/gaxmann/gordonssunclock

---

<p float="left">
  <img src="https://github.com/gaxmann/gordonssunclock/raw/master/_gitdesign/sunclock2604.png" width="250" />
  <img src="https://github.com/gaxmann/gordonssunclock/raw/master/_gitdesign/tablet.jpg" width="250" />
</p>

---

## Like it?

If you enjoy Sun Clock, please consider:
- Share it with others – Short link: **sky12.de**
- Leaving a positive review on [Play Store](https://play.google.com/store/apps/details?id=de.ax12.zunclock) 
- Reading what others say on the [Voices on Sun Clock](https://github.com/gaxmann/gordonssunclock/wiki/Voices-on-Sun-Clock) wiki page

Enjoy using Sun Clock ☀️

