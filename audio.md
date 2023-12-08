# Instructions

## Required materials
* spencer-gen2 board
* meta-spencer

## Prerequisite
* Logged into a shell console
* Connect to wifi(see qvts/wifi.md)
* Append the following line to the /etc/resolve.conf => nameserver 8.8.8.8
* Unmute the speaker and enable the capture from the microphone (see qvts/audio.md)

# Start the simple browser application
```
root@spencer-gen2:~#
root@spencer-gen2:~# export QTWEBENGINE_DISABLE_SANDBOX=1
root@spencer-gen2:~# export QT_QPA_EGLFS_FORCE888=24
root@spencer-gen2:~# /usr/share/examples/webenginewidgets/simplebrowser/simplebrowser https://webrtc.github.io/samples/                                                    
QEglFSVivIntegration will set environment variable FB_MULTI_BUFFER=2 to enable double buffering and vsync.
 If this is not desired, you can override this via: export QT_EGLFS_IMX6_NO_FB_MULTI_BUFFER=1
Sandboxing disabled by user.
qt.webenginecontext: 

GL Type: egl
Surface Type: OpenGLES
Surface Profile: NoProfile
Surface Version: 3.1
QSG RHI Backend: OpenGL
Using Supported QSG Backend: yes
Using Software Dynamic GL: no
Using Multithreaded OpenGL: yes

Init Parameters:
  *  application-name simplebrowser 
  *  browser-subprocess-path /usr/libexec/QtWebEngineProcess 
  *  disable-features ConsolidatedMovementXY,InstalledApp,BackgroundFetch,WebOTP,WebPayments,WebUSB,PictureInPicture 
  *  disable-speech-api  
  *  enable-features NetworkServiceInProcess,TracingServiceInProcess 
  *  enable-threaded-compositing  
  *  enable-use-zoom-for-dsf false 
  *  in-process-gpu  
  *  no-sandbox  
  *  use-gl egl 

js: Error with Permissions-Policy header: Unrecognized feature: 'interest-cohort'.
 
```
* To test camera 
```
//On the display the following screen is displayed
root@spencer-gen2:~# amixer sset Lineout unmute
Simple mixer control 'Lineout',0
  Capabilities: pvolume pswitch pswitch-joined
  Playback channels: Front Left - Front Right
  Limits: Playback 0 - 31
  Mono:
  Front Left: Playback 18 [58%] [-6.50dB] [on]
  Front Right: Playback 18 [58%] [-6.50dB] [on]
root@spencer-gen2:~# 
```
* GP unmute audio and enable amplifier
```
root@spencer-gen2:~# gpioset 3 28=0
root@spencer-gen2:~# gpioset 3 29=1
root@spencer-gen2:~# 
```
* capture from Microphone:
```
root@spencer-gen2:~# amixer set 'PCM' 110
Simple mixer control 'PCM',0
  Capabilities: pvolume
  Playback channels: Front Left - Front Right
  Limits: Playback 0 - 192
  Mono:
  Front Left: Playback 110 [57%]
  Front Right: Playback 110 [57%]
root@spencer-gen2:~# 
root@spencer-gen2:~# 
root@spencer-gen2:~# 
root@spencer-gen2:~# amixer sset Mic 1
Simple mixer control 'Mic',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 3
  Mono: 1 [33%] [20.00dB]
root@spencer-gen2:~# amixer set 'Capture Mux' 'MIC_IN'
Simple mixer control 'Capture Mux',0
  Capabilities: enum
  Items: 'MIC_IN' 'LINE_IN'
  Item0: 'MIC_IN'
root@spencer-gen2:~# 
root@spencer-gen2:~# amixer set 'Capture' 12
Simple mixer control 'Capture',0
  Capabilities: cvolume cswitch cswitch-joined
  Capture channels: Front Left - Front Right
  Limits: Capture 0 - 15
  Front Left: Capture 12 [80%] [on]
  Front Right: Capture 12 [80%] [on]
root@spencer-gen2:~# 
root@spencer-gen2:~# arecord -D hw:0,0 -V mono -c 2 -f S16_LE -r 16000 -t wav mic.wav
Recording WAVE 'mic.wav' : Signed 16 bit Little Endian, Rate 16000 Hz, Stereo
#+                                                 | 00%^CAborted by signal Interrupt...
root@spencer-gen2:~# 
root@spencer-gen2:~# aplay mic.wav 
Playing WAVE 'mic.wav' : Signed 16 bit Little Endian, Rate 16000 Hz, Stereo
root@spencer-gen2:~# 
```
* Volume control:
```
root@spencer-gen2:~# amixer set 'PCM' 110
Simple mixer control 'PCM',0
  Capabilities: pvolume
  Playback channels: Front Left - Front Right
  Limits: Playback 0 - 192
  Mono:
  Front Left: Playback 110 [57%]
  Front Right: Playback 110 [57%]
root@spencer-gen2:~# aplay mic.wav 
Playing WAVE 'mic.wav' : Signed 16 bit Little Endian, Rate 16000 Hz, Stereo
root@spencer-gen2:~# 
root@spencer-gen2:~# amixer set 'PCM' 160
Simple mixer control 'PCM',0
  Capabilities: pvolume
  Playback channels: Front Left - Front Right
  Limits: Playback 0 - 192
  Mono:
  Front Left: Playback 160 [83%]
  Front Right: Playback 160 [83%]
root@spencer-gen2:~# 
root@spencer-gen2:~# 
```
* play a wav file:
```
root@spencer-gen2:~# aplay /unit_tests/ASRC/audio8k16S.wav
Playing WAVE '/unit_tests/ASRC/audio8k16S.wav' : Signed 16 bit Little Endian, Rate 8000 Hz, Stereo
root@spencer-gen2:~# 
root@spencer-gen2:~# 
root@spencer-gen2:~# 
```
* pulseaudio tests:
```
root@spencer-gen2:~# pulseaudio -k
root@spencer-gen2:~# pulseaudio --start
W: [pulseaudio] main.c: This program is not intended to be run as root (unless --system is specified).
root@spencer-gen2:~# 
root@spencer-gen2:~# 
root@spencer-gen2:~# 
root@spencer-gen2:~# 
root@spencer-gen2:~# pactl list cards
Card #0
  Name: alsa_card.platform-sound-bt-sco
  Driver: module-alsa-card.c
  Owner Module: 6
  Properties:
	alsa.card = "1"
	alsa.card_name = "bt-sco-audio"
	alsa.long_card_name = "bt-sco-audio"
	device.bus_path = "platform-sound-bt-sco"
	sysfs.path = "/devices/platform/sound-bt-sco/sound/card1"
	device.form_factor = "internal"
	device.string = "1"
	device.description = "Built-in Audio"
	module-udev-detect.discovered = "1"
	device.icon_name = "audio-card"
  Profiles:
	input:mono-fallback: Mono Input (sinks: 0, sources: 1, priority: 1, available: yes)
	output:mono-fallback: Mono Output (sinks: 1, sources: 0, priority: 100, available: yes)
	output:mono-fallback+input:mono-fallback: Mono Output + Mono Input (sinks: 1, sources: 1, priority: 101, available: yes)
	off: Off (sinks: 0, sources: 0, priority: 0, available: yes)
  Active Profile: output:mono-fallback+input:mono-fallback
  Ports:
	analog-input: Analog Input (type: Analog, priority: 10000, latency offset: 0 usec, availability unknown)
	  Part of profile(s): input:mono-fallback, output:mono-fallback+input:mono-fallback
	analog-output: Analog Output (type: Analog, priority: 9900, latency offset: 0 usec, availability unknown)
	  Part of profile(s): output:mono-fallback, output:mono-fallback+input:mono-fallback

Card #1
  Name: alsa_card.platform-sound
  Driver: module-alsa-card.c
  Owner Module: 7
  Properties:
	alsa.card = "0"
	alsa.card_name = "SpencerGen_2"
	alsa.long_card_name = "SpencerGen_2"
	device.bus_path = "platform-sound"
	sysfs.path = "/devices/platform/sound/sound/card0"
	device.form_factor = "internal"
	device.string = "0"
	device.description = "Built-in Audio"
	module-udev-detect.discovered = "1"
	device.icon_name = "audio-card"
  Profiles:
	input:stereo-fallback: Stereo Input (sinks: 0, sources: 1, priority: 51, available: yes)
	output:stereo-fallback: Stereo Output (sinks: 1, sources: 0, priority: 5100, available: yes)
	output:stereo-fallback+input:stereo-fallback: Stereo Output + Stereo Input (sinks: 1, sources: 1, priority: 5151, available: yes)
	off: Off (sinks: 0, sources: 0, priority: 0, available: yes)
  Active Profile: output:stereo-fallback+input:stereo-fallback
  Ports:
	analog-input-mic: Microphone (type: Mic, priority: 8700, latency offset: 0 usec, availability unknown)
	  Properties:
		device.icon_name = "audio-input-microphone"
	  Part of profile(s): input:stereo-fallback, output:stereo-fallback+input:stereo-fallback
	analog-output: Analog Output (type: Analog, priority: 9900, latency offset: 0 usec, availability unknown)
	  Part of profile(s): output:stereo-fallback, output:stereo-fallback+input:stereo-fallback
	analog-output-headphones: Headphones (type: Headphones, priority: 9900, latency offset: 0 usec, availability unknown)
	  Properties:
		device.icon_name = "audio-headphones"
	  Part of profile(s): output:stereo-fallback, output:stereo-fallback+input:stereo-fallback
root@spencer-gen2:~#
root@spencer-gen2:~#
root@spencer-gen2:~#
root@spencer-gen2:~#
root@spencer-gen2:~# pacmd list-sinks | grep "name:"
  name: <alsa_output.platform-sound-bt-sco.mono-fallback>
  name: <alsa_output.platform-sound.stereo-fallback>
root@spencer-gen2:~#
root@spencer-gen2:~#
root@spencer-gen2:~# paplay -p --device=alsa_output.platform-sound.stereo-fallback /unit_tests/ASRC/audio8k16S.wav 
root@spencer-gen2:~#
root@spencer-gen2:~#
```
