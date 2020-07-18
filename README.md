# CRTPi-Project Presents: CRTPi-VGA
*A Vanilla+ experience for 31Khz Analog Output over VGA!*
_____

Thank you very much to Mike V, Sakitoshi, Mike Chi, the guys at Arcadeforge, Artemio Urbina, Ruckage, ChipsnBlip, Gabriel, kitty666cats, and anyone I've missed! Thank you for the input, support, resources, and help along the way!

**Major Changelogs and Features can be viewed in the pinned posts here:**

    https://reddit.com/r/u_erantyint

**User Photo Galleries (Photos from Historical Versions):**

* VGA: https://photos.google.com/share/AF1QipNO6y2Vjt0jFrwY0kYbgsD-R2-KjNFuaDqKrFZQsCebWi6O1nZAF4ozajdksLw7KQ?key=WGVHbWMxLXd2ZlFqbFhGZ3BLRjZTSE42S1FNVFdB

**Required Hardware:**

    Raspberry Pi 3B or 3B+
    Gert VGA666 or other compatible VGA hat
    5v 2.5A Micro USB power supply (Element14 recommended)
    4GB+ SD Card
    
_____

**Optional Prerequisites: Install these prior to installing the CRTPi zips!** 

	Install the following theme: /ruckage/snes-mini/
	Install the following opt packages: scummvm, lr-beetle-wswan, lr-fbalpha2012, lr-mame2000, lr-mame2010, lr-nxengine, lr-ppsspp, lr-prboom, lr-snes9x2002, lr-tgbdual, lr-tyrquake, scraper, skyscraper
	Install the following experimental packages: lr-mame2003-plus
	Install libxpm-dev and libx11-dev: "sudo apt-get install libxpm-dev && sudo apt-get install libx11-dev"
	Install MUNT (MT-32 Emulation) using this guide: https://retropie.org.uk/forum/topic/12549/tutorial-installing-munt-mt-32-emulation-on-rpi-3 (Remove 'qtmobility-dev' from step 1) (mt32roms.zip in master is for step 10)

_____

**Instructions: This is recommended to be installed on a fresh Retropie install on a 3B or 3B+ using the 4.6 offical image (Or 4.5.1 updated to 4.6). Anything you overwrite is your own fault at this point!**

*VGA: For VGA666 to 31khz Display*

    Install Retropie and configure your desired content
    Connect to WiFi or Ethernet with internet access
    Download the CRTPi-VGA.zip into your root folder (cd /) with the command "sudo wget https://github.com/crtpi/CRTPi-VGA/raw/master/CRTPi-VGA.zip" 
    ***WARNING: THE NEXT STEP WILL OVERWRITE GAMELIST.XML FILES AS SHOWN IN THE REPRO! BACK UP ACCORDINGLY!!***
    Unzip and overwrite files with the command "sudo unzip -o -q CRTPi-VGA.zip"
    Remove the zip with the command "sudo rm CRTPi-VGA.zip"
    Power off the Pi with the command "sudo poweroff" and remove power once the green light stops blinking
    Install your VGA666 GPIO hat
    Put SD card back in Pi and power on while connected to your VGA monitor
    Drop to the command line or connect via SSH
    Restore read/write access to the files you have overwritten with the command  "sudo chmod a+rw -R /opt/retropie/configs/"
    Restore execute access to the runcommand scripts with the command "sudo chmod a+rwx /opt/retropie/configs/all/*.sh"
	Launch into RetroPie-Setup with the command "sudo ~/RetroPie-Setup/retropie_setup.sh"
	Go to "Configuration/Tools > resetromdirs" and run it
	Choose "Perform Reboot" from the menu to reboot your Pi.
	
_____

The VGA fork is now utilizing Snap-Shader, plus a newly-enhanced runcommand-onstart script, with provision for *user-specified per-game configuration*! 

**Here's the new script:**

    https://github.com/crtpi/CRTPi-VGA/blob/master/VGA-to_opt/retropie/configs/all/runcommand-onstart.sh

**Here's information about Snap-Shader:**

    https://github.com/ektgit/snap-shader-240p

**And here's a quick rundown on how it works:**

Not only does the new script carry forward the per-core scripting for 2048x / 1920x / and 1600x resolutions -- but adds per-game scripting by adding a text file to the system config and naming the rom(s) within the file. This allows you to force 2048x on a system that defaults to 1920x, or the other way around. This is especially useful for PSX, FDS, PCE/PCE-CD, and MAME for the few games that are 256 or 512 wide. Below are some example config files:

**/opt/retropie/conifgs/psx/256.txt**

    Brave Prove
    Castlevania - Symphony of the Night
    Crash Bandicoot
    Final Fantasy Origins
    Final Fantasy Tactics

**/opt/retropie/conifgs/megadrive/256.txt**

    Bubble And Squeak
    Bubsy in - Claws Encounters of the Furred Kind 
    Bugs Bunny in Double Trouble 
    Caesars Palace 
    Captain America and the Avengers 
    
 
**/opt/retropie/conifgs/fds/320.txt**

    Akumajou Dracula
    Donkey Kong
    Otocky
    Super Mario Brothers 2

You get the jist. It doesn't need an extension, but should match the rom name including punctuation. This forces them to launch in 2048x240p instead of the default 1920x240p, or vise versa. This gives the end user full control on a game-per-game basis over the horizontal integer. You'll still need to write a retroarch game config to override the defaults there, but this at least gets you the right field. For games with odd/shifting vertical resolutions (like Chrono Cross, Battle Arena Toshinden, Castlevania SotN, etc.), a single pass of snap-shader is applied (snap-basic, nearest neighbor filtering, and "don't care" scale).

_____

**Final Thoughts:**

If you have any questions, comments, concerns, or issues -- please PM me or DM me on Reddit or post on one of the threads. Chances are, it's a "feature" not a "bug." :)
_____
