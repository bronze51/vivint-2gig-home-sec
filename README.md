# vivint-2gig-home-sec
Repository for re-using vivint equipment
# Re-using vivint equipment
## Introduction
My recently bought house has a vivint doorbell (DBC2-43536D ), an IP camera (721W-46813F), and several 2Gig connected sensors. As the battery was failing of the vivint head-unit, and it complained about the lack of scubscription, I disconnected it for now.
I am pretty much an enthusiastic noob. I document below my successfull endeavours. Much of it will need further iterations and improvements overtime. Comments/tips are welcome.
### Doorbell
When you have a vivint doorbell and disconnect the vivint head-unit, you will no longer hear it "chime" when somebody presses the doorbell. This was a problem for me so I started exploring how to intercept the chime "event" at the doorbell in order to make a speaker inside "chime".
## Vivotek
### General
The vivint doorbell (DBC2-43536D), an IP camera (721W-46813F) are rebranded vivotek equipment.
The doorbell and the IP camera can be forced into WPS mode. Alternativelly, they can be forced into AP mode. Eother way, yuy can connect them to your own WLAN in case they weren't already.
Subsequently, you can enable "telnet" as follows: "http://<IP-address of vivotek device>/cgi-bin/admin/mod_inetd.cgi?telnet=on".
The password of the "root" user is available on the web: "adcvideo". You can not telnet into your vivotek device. Telnet is not a safe protocol, but it appear to be the only way a shell can be started on the vivotek device. 
### Doorbell
My doorbell runs linux with busybox. Busybox is a low resource, stripped-down implementation and its commands do not seem to support all the options. It is stripped down as I failed to find e.g. an ssh-deamon.
When the doorbell is pressed, the the script "play_sound" is invoked by "chronos", with the argunement "/etc/audio/bell.wav" (in my case).
The "play_sound" script is stored on a read-only portion of its storage (it might be possible to mount this storagte in "rw" mode, but I didnt explore this). 
The "play_sound" script invokes "nice". I managed to "override" "nice". I managed detect when "nice" is invoked for playing "/etc/audio/bell.wav" and when it is invoked for playing some other "audio" file. I managed to "ssh" into my Raspbery Pi (with speaker atatched) when "nice" was invoked for playing "/etc/audio/bell.wav".
  
Further details wil follow.
### IP camera
TBD
## 2Gig
TBD



