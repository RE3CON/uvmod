# [CLICK HERE TO OPEN UVMOD RX-TX](http://uvmod.ddns.net/) *feature work in development* WIP
## [中文版 Open Chinese Version (maintained independently)](https://uvmod.xanyi.eu.org/)
# [UVMOD in Russian Language Version](https://uvmod.valek.net.ru/) by [Valek rus](https://github.com/valekrus/uvmod-russian)
# [UVMOD in Portugese by Matoz @spm81](https://meshtastic.pt/QuanSheng/)

[Discussion forum 4PDA](https://4pda.to/forum/index.php?showtopic=1071343&st=0) | [Telegram Group](https://t.me/uv_k5/34434) | [Chinese Mod collection](https://www.zhihu.com/people/troilusxi) | [Japanese Mod collection](https://www.nazononiku.com/uncategorized/uv-k5%E3%81%AE%E3%83%95%E3%82%A1%E3%83%BC%E3%83%A0%E3%82%A6%E3%82%A7%E3%82%A2%E3%82%92%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA/686/)

## Introduction

Web-based client-side Quansheng firmware patcher written in Javascript and HTML.
It is based on the discoveries by the many contributors in the [uvmod-kitchen](https://github.com/amnemonic/Quansheng_UV-K5_Firmware/tree/main/uvmod_kitchen) by writing Python in Java code and analyzing modded firmware binaries for my enhanced UVMOD RX-TX patcher by making diffs from unpacked binaries to get the results for changing/replacing the propper offsets bit strings in heximal for example based on [Tunas1337 UV-K5 Modded Firmwares](https://github.com/Tunas1337/UV-K5-Modded-Firmwares). This patcher implements the **same functionality** not limited to RX only but also TX in a modular and flexible javascript structure. This is an enhanced RX-TX UVMOD based on [whosmatt UVMOD src](https://github.com/whosmatt/uvmod). The first TX features were much earlier written and released here thats why the name UVMOD RX-TX.

## How it works
On the [website](https://recon.ddns.net/) you can generate a patched firmware image by selecting the patches of your choice. The patcher encode, apply the patches to modify and then decode the firmware on a binary level and can accept user input to customize variables. A custom base image can be supplied (uploaded) to allow support for mods that are compiled and linked directly into the firmware. The mods (patches) will be applied in the range from the first mod on top to the last mod on button. The later mods on the webpage can overwrite the mods function standing on the top of the online patcher and run in the direction down of the mods collection. eg. Mod TX and RX from 18-1300MHz will get overwritten if you select it together with Disable TX Lock from 50-600 MHz, Enable TX everywhere except Air Band, ...and so forth... because this functions are in contrast to each other. 
**Do not select Mods (patches) with contraindicated features and functions!**
Use it wisely and choose your selected mods carefully before apply, download (save) and flash the firmware into your transceiver.

## Copy and Host it, upload it on your own Webspace

Simply download the [latest files in a zip file](https://github.com/RE3CON/uvmod/archive/refs/heads/main.zip) and extract it, upload it to your own webspace hosting.

## Unpack/Pack and Encoding Firmware binaries

Firmware version spoofing on modded firmware v2 for v3, v4 uv-5r plus<br>
You must have [Python](https://www.python.org/downloads/) installed.
1. Download file [qsfirm.py](https://github.com/RE3CON/Quansheng_UV-K5_Firmware/blob/main/firmware/qsfirm.py) and place it into the same folder with [yourfirmware.bin](https://github.com/RE3CON/Quansheng_UV-K5_Firmware/tree/main/firmware)
3. Run command: qsfirm.py unpack yourfirmware.bin fw.dec.bin fw.ver.bin
4. *Optional:* At this point you can use [binary compersation](https://en.m.wikipedia.org/wiki/Comparison_of_file_comparison_tools) diff and merge tools [Binary diff Tool](https://www.guiffy.com/Binary-Diff-Tool.html), WinMerge, hexcompare, [HEXCMP](https://hexcmp.en.lo4d.com/windows).<br> For search replace pattern, they are likely firmware version independend, you may use patch creater w/o installed Python dist. requirements to unpack/pack. Applying even on a packed firmware bin such as [diabolo 2oo2 universal patch engine](https://github.com/RE3CON/diablo2oo2-s-Universal-Patcher-dUP-Windows) or others see eXe stuff forums. They may produce false positives alerts like unwanted Patch Tool risk once compiled as an exe patcher file. PE packer, crypter like PEcompact and co. can eliminate these wrong alerts. See unpacking and hacking forums about this topic. Completely Disabling AV software such as windows defender with all protection features and levels will be a temporary solution or run it in a virtual machine enviroment (VM) isolated if you afraid. Someone with good Python skills could just make these patches on search and replace pattern instead fixed address offsets which are different by every fw version but not the bytes pattern strings. Adding for precission a few (2 o 4) neighbor bits before and after the targets to replace.
5. Edit file fw.ver.bin in a hex editor like [HXD](https://mh-nexus.de/en/hxd/) to change the fw version where it should be flashed over. For example for v4, replace it with 4.00.01. With a * instead of a number makes it universal for all fw versions flashable.
6. Run command: qsfirm.py pack fw.dec.bin fw.ver.bin yourfirmware_mod_v4.bin

## Mod development

Clone this repository and execute `python3 -m http.server` or `python -m http.server` in the root directory for an instant local web server, allowing easy testing.  
Mods are defined in [mods.js](mods.js), with an example mod to outline the pattern.  
Also __refer to the helper functions and documentation in__ [modframework.js](js/modframework.js).  

The supported format for binary data is in the format of a hex string __without separators__. You can use find and replace to remove all `\x` from a regular hex string or directly export the correct format from a bytes object in python using `print(''.join('%02x'%i for i in BYTES_OBJECT))`.

You may try one of these Java to exe convertors, compiling a java program into an executable. AutoIt and other scripting tools etc.. Most patches are also in [Python](https://github.com/amnemonic/Quansheng_UV-K5_Firmware/tree/main/uvmod_kitchen) available  to create an offline application.

## **Disclaimer** 
This project was created for research and amateur radio use only, we are not responsible for improper use of this code which might lead to unauthorized transmission, reception or any patent infringments.

The firmware produced with this website is released WITHOUT ANY WARRANTY: Anyone flashing a modified binary image obtained from the sources made available through this repository and website configurator does so at their own risk. We always test all the code on our devices before publishing it on the repository, however we cannot guarantee the absolute absence of bugs nor of potential side effects. Mods flagged with Experimental are not fully tested.

## Credits, rules and trouble, whats all about...
"Threaten me with reference to DMCA is a taboo that's absolutely frowned upon among open source coding communities. A No-Go by doing shared code works. However he's desided later to implement my TX unlock code and add TX related features afterwards." Thats great to push the initial uvmod further with TX features since that."

## About warnings...
However warnings about TX freq related features have been together with the FIRST UVMOD equipped with a TX Mod released by me and clearly to understand warnings written to the function description at the same time as published. This was a while <i>before</i> whosmatt's first time implemented my and any TX mod/patch. See the code time line changes around August, 3th 2023. 
<strong><i>It is absolutely wrong to say and write public that I have removed any warnings, I just did not implement it.</i></strong> Later on he added even more tx features (Yah thats really great!). All TX freq mods surrounding with a hugh bunch of fancy red colors, red flags and fancy css attributes to show warnings – in a good believing it could preventing more non authorized usage in the wrong hands of a HF transmitter. 

There are no danger TX freq differences between custom created fw using a UVMOD website or download one of these already modded fw file or modding firmware offline customized with python patches and apply to the firmware. One or the other way, it is to think about the secret menu functions where you can w/o any modded firmware flashing, just switch to unlock extended rx/tx ranges on/off and set country restrictions. All modded fw makes this hidden original freq feature partwise redundant and broken instead of extending or changing it – addressing the hidden menu settings. 
You know where I'm coming from, these are just different views how to express these visual warnings/danger/attention/hints, call it how you want in meaning – use it wisely. Every HAM OP, commercial or legal user should know and learned about the QTH countries regulations mostly required before a legal purchase and use of HAM radio transmitters and HF Amps.  
Not only Air Band but also Millitary, emergency services and so forth could be affected when you use it wrong. TX below 136 MHz produce a lot Harmonics on other frequencies with higher transmitting power than on the wanted transmitting  frequency shown on LCD.


*Credits and thanks to whosmatt!*
