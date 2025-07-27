OH SINT is challenge is Type of information gathering CTF Challenge.

difficultly level - EASY
Challenge- https://tryhackme.com/room/ohsint
the task file was in OH SINT folder Name - WindowsXP....

### Tools i used 

1.i used ExifTool online site for this 
https://exif.tools/upload.0php
2.Wigle website for check BSSID
https://wigle.net/

# STEPS-

i used exiftool online site for to scan the Image i that Challenge gave and outputs are interesting

|                                                                                                                            |                                      |
| :------------------------------------------------------------------------------------------------------------------------- | :----------------------------------- |
| **ExifTool Version Number[![](https://exif.tools/external.svg)](https://exif.tools/meta/ExifTool-Version-Number)**         | **12.25**                            |
| **File Name[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Name)**                                     | **phpPQVMgq**                        |
| **Directory[![](https://exif.tools/external.svg)](https://exif.tools/meta/Directory)**                                     | **/tmp**                             |
| **File Size[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Size)**                                     | **229 KiB**                          |
| **File Modification Date/Time[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Modification-Date/Time)** | **2025:07:19 18:10:38+00:00**        |
| **File Access Date/Time[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Access-Date/Time)**             | **2025:07:19 18:10:37+00:00**        |
| **File Inode Change Date/Time[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Inode-Change-Date/Time)** | **2025:07:19 18:10:38+00:00**        |
| **File Permissions[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Permissions)**                       | **-rw-------**                       |
| **File Type[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Type)**                                     | **JPEG**                             |
| **File Type Extension[![](https://exif.tools/external.svg)](https://exif.tools/meta/File-Type-Extension)**                 | **jpg**                              |
| **MIME Type[![](https://exif.tools/external.svg)](https://exif.tools/meta/MIME-Type)**                                     | **image/jpeg**                       |
| **XMP Toolkit[![](https://exif.tools/external.svg)](https://exif.tools/meta/XMP-Toolkit)**                                 | **Image::ExifTool 11.27**            |
| **GPS Latitude[![](https://exif.tools/external.svg)](https://exif.tools/meta/GPS-Latitude)**                               | **54º 17' 41.27" N**                 |
| **GPS Longitude[![](https://exif.tools/external.svg)](https://exif.tools/meta/GPS-Longitude)**                             | **2º 15' 1.33" W**                   |
| **Copyright[![](https://exif.tools/external.svg)](https://exif.tools/meta/Copyright)**                                     | **OWoodflint**                       |
| **Image Width[![](https://exif.tools/external.svg)](https://exif.tools/meta/Image-Width)**                                 | **1920**                             |
| **Image Height[![](https://exif.tools/external.svg)](https://exif.tools/meta/Image-Height)**                               | **1080**                             |
| **Encoding Process[![](https://exif.tools/external.svg)](https://exif.tools/meta/Encoding-Process)**                       | **Baseline DCT, Huffman coding**     |
| **Bits Per Sample[![](https://exif.tools/external.svg)](https://exif.tools/meta/Bits-Per-Sample)**                         | **8**                                |
| **Color Components[![](https://exif.tools/external.svg)](https://exif.tools/meta/Color-Components)**                       | **3**                                |
| **Y Cb Cr Sub Sampling[![](https://exif.tools/external.svg)](https://exif.tools/meta/Y-Cb-Cr-Sub-Sampling)**               | **YCbCr4:2:0 (2 2)**                 |
| **Image Size                                                                                                               | **1920x1080**                        |
| **Megapixels[![](https://exif.tools/external.svg)](https://exif.tools/meta/Megapixels)**                                   | **2.1**                              |
| **GPS Latitude Ref[![](https://exif.tools/external.svg)](https://exif.tools/meta/GPS-Latitude-Ref)**                       | **North**                            |
| **GPS Longitude Ref[![](https://exif.tools/external.svg)](https://exif.tools/meta/GPS-Longitude-Ref)**                     | **West**                             |
| **GPS Position[![](https://exif.tools/external.svg)](https://exif.tools/meta/GPS-Position)**                               | **54º 17' 41.27" N, 2º 15' 1.33" W** |
yeah even location..

and this line got my attention.

```
|Copyright                     |OWoodflint|
```

so use this to search in google.i found a X account in exact same name and i look at it..there is profile pic cute cat.

```
https://x.com/owoodflint?lang=gu
```

Answer For Our first Question 

1.What is this user's avatar of?

```
cat
```

and then i thought to search in github for find anything helpful

and for 2,4,5 Questions solved by it..

**==2.What city is this person in?**==
==**4.What is his personal email address?**==
==**5.What site did you find his email address on?==**

THIS IS WHAT I FOUND ON GITHUB

##### **people finder**

##### **Hi all, I am from London, I like taking photos and open source projects.** 

##### **Follow me on twitter: @OWoodflint**

##### **This project is a new social network for taking photos in your home town.**

##### **Project starting soon! Email me if you want to help out: OWoodflint@gmail.com**

```
https://oliverwoodflint.wordpress.com/
```



Our target have leaked their wifi BSSID on Twitter page, from that inforamtion we can use [https://wigle.net/](https://wigle.net/) . Now once you have BSSID you need to go to Wigle.net and do an advanced search using BSSID . In the Network Characteristics section enter the BSSID value and click on Query.


and found this for 
**Q3. What is the SSID of the WAP he connected to?  
```
Ans: UnileverWifi
```

and also from his that GITHUB page his site link

```
https://oliverwoodflint.wordpress.com/
```

i found answer for question nb 6
**6.Where has he gone on holiday?**
```

ans: New York

```

so there last one to finish

**Q7. What is the person’s password?  
```
Ans: pennYDr0pper.!
```
i found it in source code in his page.



## try hackme OHSINT is completed

what i learned,

in here i learned how to use exiftool to extract hidden details and also wginle how to search bssid..and i learned i need to be patien and explore more than visual things normal i could..