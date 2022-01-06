# OpenLeo's IVI system (Come discuss about it on our [Discord](https://discord.gg/evxp5ahPAS)!)

## Intro

This is the main repository for the OpenLeo's In Vehicle Infotainment system. This contain the hardware and main software design for the ECU that hosts the head unit and trip computer UIs (and may host a digital cluster as well in the future)

## Hardware

We plan to use an ARM SoC that has good linux support (including good drivers), for example an i.mx SoC. The IVI itself should have a good enough DAC, but will probably not contain a integrated amp (this may change). The requirements for now:

* ARM SoC with good linux compatibility
* Has multiple display outputs, each with it's own framebuffer
* May have video inputs (eg. for reverse camera or dashcam)
* May have an integrated 4g modem (eg. for telematics/phone)
* May have integrated FM/DAB interface
* Will probably not include a CD drive, but will probably include an USB and uSD/TF card interface
* One, ideally two CAN interfaces, maybe provisioning for other (eg. VAN, MOST...) interfaces
* Being able to extend it (for example a 433mhz receiver for TPMS systems)


## Software/OS

This is designed to use a embedded linux (eg. kernel + busybox, using only the framebuffers), with these software running on it:

* The watchdog, that monitor the health of the daemon and manages them if they crash
* The car daemon, which connects to the CAN/VAN/etc interfaces and provide a socket file for the UIs to use
* The bluetooth deaemon, which manages the A2DP, HFP, AVRCP, PBAP, SAP, LAP profiles
* The audio daemon (pulseaudio), that manages the mixer and audio output with auto level management (eg. music being turned down when a notification rings)
* The music/radio daemon (mopidy), that manages the music and radio playback, ideally with FM/DAB and spotify/deezer/etc support
* The navigation daemon, that manages the turn-by-turn navigation instructions, route informations and alerts
* The head unit UI, which is the main UI of the device
* The trip computer UI, as a secondary interface, optional
