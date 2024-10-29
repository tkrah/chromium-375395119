# PDF Font Embedding issue 

Link: https://issues.chromium.org/issues/375395119

Reproducer:

* Open chromium and open the test.html file
* Strg+P => Choose no borders => Choose no header + footer
* Print the Page to a PDF file

## Environment
Versions used while observing this issue with Puppeteer are:

* https://storage.googleapis.com/chrome-for-testing-public/129.0.6668.100/linux64/chrome-linux64.zip
* https://storage.googleapis.com/chrome-for-testing-public/130.0.6723.58/linux64/chrome-linux64.zip

Versions used while observing it with user interactive print to pdf dialog:

* chromium_129.0.6668.100~linuxmint1+virginia_amd64.deb
* chromium_130.0.6723.58~linuxmint1+virginia_amd64.deb

from the Linux-Mint repositories.

### Desktop Environment

````
             ...-:::::-...                  tkrah@box
          .-MMMMMMMMMMMMMMM-.               ------------------
      .-MMMM`..-:::::::-..`MMMM-.           OS: Linux Mint virginia 21.3 x86_64
    .:MMMM.:MMMMMMMMMMMMMMM:.MMMM:.         Host: 21CFCTO1WW (ThinkPad T14 Gen 3)
   -MMM-M---MMMMMMMMMMMMMMMMMMM.MMM-        Kernel: 6.8.0-47-generic
 `:MMM:MM`  :MMMM:....::-...-MMMM:MMM:`     Uptime: 11 hours, 5 mins
 :MMM:MMM`  :MM:`  ``    ``  `:MMM:MMM:     Packages: 3450 (dpkg)
.MMM.MMMM`  :MM.  -MM.  .MM-  `MMMM.MMM.    Shell: bash 5.1.16
:MMM:MMMM`  :MM.  -MM-  .MM:  `MMMM-MMM:    Display (FS2333): 1920x1080 @ 60Hz *
:MMM:MMMM`  :MM.  -MM-  .MM:  `MMMM:MMM:    Display (2490W1): 1920x1080 @ 60Hz
:MMM:MMMM`  :MM.  -MM-  .MM:  `MMMM-MMM:    DE: Cinnamon 6.0.4
.MMM.MMMM`  :MM:--:MM:--:MM:  `MMMM.MMM.    WM: Muffin (X11)
 :MMM:MMM-  `-MMMMMMMMMMMM-`  -MMM-MMM:     WM Theme: Mint-L-Dark-Purple (Mint-Y)
  :MMM:MMM:`                `:MMM:MMM:      Theme: Mint-L-Blue [GTK2/3/4]
   .MMM.MMMM:--------------:MMMM.MMM.       Icons: candy-icons [GTK2/3/4]
     '-MMMM.-MMMMMMMMMMMMMMM-.MMMM-'        Font: Ubuntu (10pt) [GTK2/3/4]
       '.-MMMM``--:::::--``MMMM-.'          Cursor: Bibata-Modern-Classic (24px)
            '-MMMMMMMMMMMMM-'               Terminal: GNOME Terminal 3.44.0
               ``-:::::-``                  Terminal Font: DejaVu Sans Mono (10pt)
                                            CPU: AMD Ryzen 7 PRO 6850U (16) @ 4,77 GHz
                                            GPU: AMD Rembrandt @ 0,53 GHz [Integrated]
                                            Memory: 21,87 GiB / 30,13 GiB (73%)
                                            Swap: 2,11 GiB / 8,00 GiB (26%)
                                            Locale: de_DE.UTF-8
````

## Chromium 129.0.6668.100


````
$ pdffonts ISSUE-375395119-129.pdf
name                                 type              encoding         emb sub uni object ID
------------------------------------ ----------------- ---------------- --- --- --- ---------
AAAAAA+TimesNewRomanPSMT             CID TrueType      Identity-H       yes yes yes      4  0
BAAAAA+PatrickHand-Regular           CID TrueType      Identity-H       yes yes yes      6  0
````

````
$ pdfinfo ISSUE-375395119-129.pdf 
Title:           ISSUE-375395119
Creator:         Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Producer:        Skia/PDF m129
CreationDate:    Mon Oct 28 19:10:40 2024 CET
ModDate:         Mon Oct 28 19:10:40 2024 CET
Custom Metadata: no
Metadata Stream: no
Tagged:          yes
UserProperties:  no
Suspects:        no
Form:            none
JavaScript:      no
Pages:           1
Encrypted:       no
Page size:       594.96 x 841.92 pts (A4)
Page rot:        0
File size:       21943 bytes
Optimized:       no
PDF version:     1.4
````

## Chromium 130.0.6723.58

````
$ pdffonts ISSUE-375395119-130.pdf 
name                                 type              encoding         emb sub uni object ID
------------------------------------ ----------------- ---------------- --- --- --- ---------
AAAAAA+TimesNewRomanPSMT             CID TrueType      Identity-H       yes yes yes      4  0
[none]                               Type 3            Custom           yes no  yes      5  0
````

````
$ pdfinfo ISSUE-375395119-130.pdf 
Title:           ISSUE-375395119
Creator:         Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Producer:        Skia/PDF m130
CreationDate:    Mon Oct 28 19:10:00 2024 CET
ModDate:         Mon Oct 28 19:10:00 2024 CET
Custom Metadata: no
Metadata Stream: no
Tagged:          yes
UserProperties:  no
Suspects:        no
Form:            none
JavaScript:      no
Pages:           1
Encrypted:       no
Page size:       594.96 x 841.92 pts (A4)
Page rot:        0
File size:       19350 bytes
Optimized:       no
PDF version:     1.4
````

# Inkscape Postprocessing

Using Inkscape 1.4:

````
$ inkscape -l ISSUE-375395119-129.pdf -n 1 -o ISSUE-375395119-129.svg
````

````
$ inkscape -l ISSUE-375395119-130.pdf -n 1 -o ISSUE-375395119-130.svg

** (org.inkscape.Inkscape:10772): WARNING **: 08:49:10.187: PDF fontType3 information ignored.

** (org.inkscape.Inkscape:10772): WARNING **: 08:49:10.189: PDF fontType3 information ignored.

** (org.inkscape.Inkscape:10772): WARNING **: 08:49:10.191: PDF fontType3 information ignored.

** (org.inkscape.Inkscape:10772): WARNING **: 08:49:10.193: PDF fontType3 information ignored.

** (org.inkscape.Inkscape:10772): WARNING **: 08:49:10.196: PDF fontType3 information ignored.

** (org.inkscape.Inkscape:10772): WARNING **: 08:49:10.198: PDF fontType3 information ignored.
````

Will reproduce the SVG files - where the `ISSUE-375395119-129.svg` still does have the "MUSTER" text and the `ISSUE-375395119-130.svg` does not.
