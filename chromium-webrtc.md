# Instructions

## Required materials
* spencer-gen2 board
* meta-spencer

## Prerequisite
* Logged into a shell console
* Connect to wifi(see qvts/wifi.md)
* Append the following line to the /etc/resolve.conf => nameserver 8.8.8.8
* Unmute the speaker and enable the capture from the microphone (see qvts/audio.md) 
  to check audio related things

## Start the simple browser application
```
root@spencer-gen2:~#
root@spencer-gen2:~# echo nameserver 8.8.8.8 >> /etc/resolv.conf
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
# Testing instructions
## Query the Video and Audio devices

* A screen similar to the one shown below will appear on the display.
* Click on the highlighted link, similar to the one shown in the image, to query the video and audio devices from the 
  browser

<img width="576" alt="query" src="https://github.com/Rajeshvce/Testing/assets/94607772/7de74c08-16ab-4632-bd01-19806ab94df7">


* Afterwards, a new tab resembling the one displayed below will open on the screen.
* Within this tab, one can view the various audio and video devices available on the board.
* The selected camera from the **video source** dropdown will provide a preview on the screen.

<img width="623" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/07ddcadf-b60a-4609-b6df-3e9fedb4daab">

## Camera Testing

* A screen similar to the one shown below will appear on the display.
* Click on the highlighted link, similar to the one shown in the image, to test the camera streaming in browser


<img width="709" alt="camera" src="https://github.com/Rajeshvce/Testing/assets/94607772/2b7079b5-660f-4e25-9923-e58684cd8a96">


* Afterwards, a new tab resembling the one displayed below will open on the screen.
* Within this tab, click the button **open camera** and give the access to camera 
* Then a preview of the camera will be displayed on the screen

<img width="373" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/63b3d16d-2ddc-467b-8c4b-5a8df4be7e8c">

## Choosing different camera resolutions

* A screen similar to the one shown below will appear on the display.
* Click on the highlighted link, similar to the one shown in the image, to check the different camera resolutions 


<img width="730" alt="resolution" src="https://github.com/Rajeshvce/Testing/assets/94607772/3736d34c-92fc-40c5-9b8e-4cc65ae5641f">


* Afterwards, a new tab resembling the one displayed below will open on the screen.
* Within this tab, one can select for various camera resolutions—such as QVGA, VGA, HD, and Full HD and preview them accordingly.
  
<img width="663" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/bb34bd24-dddb-4c00-a10d-99be8954a899">

## Taking the snapshot from the browser

* A screen similar to the one shown below will appear on the display.
* Click on the highlighted link, similar to the one shown in the image, to take a snapshot from the camera


<img width="495" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/fdc881a2-82b2-4d61-ab69-f1569cf65100">


* Afterwards,a new tab resembling the one displayed below will open on the screen.
* Within this tab, One can take a snapshot by clicking the **Take snapshot** button there


<img width="271" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/3667614c-ba0c-462b-9399-e9f3dbaaeb3f">

## Testing Audio output

* A screen similar to the one shown below will appear on the display.
* Click on the highlighted link, similar to the one shown in the image, to test the audio output from the browser


<img width="394" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/dba596a6-7e0d-4be4-ad00-18607fe516f9">


* Afterwards, new tab resembling the one displayed below will open on the screen.
* Within this tab, users can play the second video and listen to the audio through the speakers.


<img width="587" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/52470fee-0dc8-4ead-b4f4-969cb65cf3f2">

## Testing basic peer to peer connection


* A screen similar to the one shown below will appear on the display.
* Click on the highlighted link, similar to the one shown in the image, to test the peer to peer connection


<img width="334" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/1cafec8b-1d35-4ae3-af49-576ba824c93a">

* Afterwards, new tab resembling the one displayed below will open on the screen.
* Open two separate tabs using the same highlighted link and proceed to click **Start** in both tabs.
* This action will display side-by-side camera previews from both tabs.

<img width="711" alt="image" src="https://github.com/Rajeshvce/Testing/assets/94607772/d49f3ba5-3a18-4759-881b-aa45c4dbf589">

&nbsp;
* **NOTE** : export the flag QT_QPA_EGLFS_ROTATION=90 to rotate the screen by an angle of 90 degrees
