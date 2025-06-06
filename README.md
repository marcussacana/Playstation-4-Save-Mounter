# Playstation 4 Save Mounter 1.3
This is an older version of the save mounter since its much easier to get working because it doesnt do any patching, but this has some drawbacks, read the original readme below.

Supports PS5 FWs:
- 2.50, 3.20, 4.03, 4.50, 5.xx, 6.xx
	- 5.10 and 5.50 have the same offsets so i just assume its the same for all of 5.xx
	- Its possible some other firmwares with the same major version has the same offsets
 - Currently can Mount only PS4 game saves, PS5 support to be added later

Requires ps5debug, here is a build of [Dizz's version](https://github.com/DizzRL/ps5debug), which supports 1.xx-5.xx, uses john-tornblom's elf loader: https://github.com/idlesauce/ps5debug

To get required offsets for unsupported firmwares send this to john-tornbloms elf loader, and add the results to offsets.cs (the sdk, and this build currently only supports 1.xx-5.xx, once support is added for higher fws you'll need to re-build): https://github.com/idlesauce/ps5-get-save-mounter-1.3-offsets

---

## Summary
This program allows you to mount save data as READ/WRITE
### You can
* Make decrypted copies of your saves
* Replace saves with modified ones
* Replace save files with someonelse's save files (share saves)
* Create new saves


### You can't
* Replace save files with an encrypted save
* Use this on unexploited consoles

### You need
* To make sure you're using a recent ps4debug version, bin of the latest ps4debug (as of 11/14) is included in the download
* To be able to run .net framework 2.0 executables (even windows 98 is able to do this)
## Prerequisites
* PS4 5.05
* FTP Client (eg filezilla, ...)
## Instructions (mouting existing saves)
1) Load [ps4debug](https://github.com/xemio/ps4debug)
2) Start a game
3) Load [FTP](https://github.com/xvortex/ps4-ftp-vtx)
4) Open the tool
5) Enter the ip of your ps4 and click 'Connect'
6) Click 'Get Processes' and select your game in the combobox
7) Click 'Setup'
8) Click 'Search'
9) Select the save you want to mount in the combobox
10) Select the mount permission in the combobox (default is READ ONLY)
11) Click 'Mount'
12) Your save is now mounted and accessible from ftp in /mnt/pfs/ & in /mnt/sandbox/{title}/savedataX (it's the same just a different dir)
13) After you're done copying/replacing files click 'Unmount'

**don't replace files in sce_sys directory, it is unnecessary and will probably corrupt your save**



**Some games use another save format, they have an sce_ prefix in their name (saves can be found in /user/home/{userid}/savedata/{titleid} check the name there). they won't show up as search results**  
**This can probably be patched but I was too lazy** 



Here's a workaround
1) go to /user/home/{userid}/savedata/{titleid}
2) make a copy of the sce save: 2 files, the bin file(96KB), the sdimg file
3) rename them  
	"sce_sdmemory.bin" -> "temp.bin"  
    "sdimg_sce_sdmemory" -> "sdimg_temp"
4) go to /system_data/savedata/{userid}/db/user and download the database.db file
5) open it with an [sqlite editor](https://sqlitebrowser.org/)  
6) add a new record in the savedata table
7) fill in the data and you're done
8) replace the original database with the newer one
9) Click 'Search' again, it should now add a temp entry to the combobox
10) proceed as usual
11) go to /user/home/{userid}/savedata/{titleid}
	* delete the original sce_sdmemory.bin and sdimg_sce_sdmemory
	* rename temp.bin to sce_sdmemory.bin and temp to sdimg_sce_sdmemory
12) replace the modified database with the original one
13) you're done

## Authors
- Aida
- [ChendoChap](https://github.com/ChendoChap)
## Acknowledgments
* [golden](https://github.com/xemio)
