# VHDLref

The purpose of this website is to provide a usable language reference for writing VHDL (VHSIC Hardware Description Language) in a way that is concise, direct, and easy to understand for as many people as possible.

This website was written with Jekyll and can be hosted on Github Pages. The design of this website is intended to be as simple and accessible to as many people as possible, so there are very few colors (only exception being code highlighting) and no JavaScript. The interface should be able to scale and be readable at most resolutions. If it does not work on your device, please submit an issue at the git repository listed below.

This website is distributed under the terms of the MIT license, except for the archives of the original reference, which remain property of the original author(s). More information about those can be found [here](history.md).

---

There has been some work put into turning this website into a webapp using Cordova. Currently only the Android build has been tested. Running `make android` will build the website and application and put it in the cordova folder. While webapps are not ideal, the website is light enough that any performance loss is made up in being able to seamlessly change the website all at once, instead of having multiple sources.

---

Design Goals:
* Accessible
* Simple
* Useful

Meaning:
- [x] Open source - anyone can take and use for their own purposes without restriction
- [x] None or limited use of images and colors
- [x] Works on a variety of devices and web browsers
- [ ] Up to date with currently used standards (need to support VHDL-08)
- [x] One major focus or topic per page
- [x] No JavaScript - static HTML and CSS only
- [ ] Search engine optimized
- [x] Meaningful example code that is easy to follow
- [x] Relative links to/from every page
- [ ] Easy for visually impaired to use (need people to test)

Pull requests and forks are welcome.
