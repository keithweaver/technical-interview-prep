# Explain the android architecture?

- Application Framework: developer layer, utilizes android.media APIs
- Binder IPC: Facilitates communication over process boundaries
- Native Multimedia Framework: Provides framework that utilizes the Stagefright engine for audio and video recording and playback.
- OpenMAX (OMX) Integration Layer (IL): C Library, Standardized way for Stagefright to recognize and use custom hardware based codecs called components.


Source: https://source.android.com/devices/media/#Architecture


# Explain the code flow for audio playback scenario and video playback scenario?


# Explain the state diagram of media player object?

*Capitals are states and func() are functions. ... means continue to next line. [#] means go to line that starts with [#] (probably to options)*

```
-> reset() -> IDLE -> setDataSource() -> ...
... INITIALIZE -> prepare() -> PREPARED -> [1]
               -> prepareAsync() -> PREPARING -> [2]
[2] -> PREPARED -> seekTo() -> PREPARED -> [1]
[1] -> start() -> STARTED -> pause() -> PAUSE -> ...
... -> start() -> STARTED -> stop() -> STOPPED -> ...
... -> PREPARING ->
```

`STARTED` can also go to `PLAYBACK COMPLETE` which can lead to `STARTED` or `STOPPED.`


Source: http://ccppcoding.blogspot.ca/2012/10/android-multimedia-media-player-states.html

# Explain about open core and stage fright?

Stagefright: an open source media player used by 95 percent of Android devices.

OpenCore: Media player that was replaced by Stagefright.


Source: https://blog.lookout.com/stagefright-detector
Source: https://stackoverflow.com/questions/22988446/difference-of-opencore-and-stagefright

# Diff b/w Open core and Stage fright?



# Explain Stage fright architecture?



# What is OpenMax IL?

- The OpenMAX IL (Integration Layer) API defines a standardized media component interface to enable developers and platform providers to integrate and communicate with multimedia codecs implemented in hardware or software.


Source: https://www.khronos.org/openmaxil


# What are the call back functions in OpenMax IL?

# What is role of OMX_Component?


# How will you implement an OMX Component?


# What is the use of OpenMax IL?

- Standardize the interface to allow developers to integrate with multimedia hardware and software codecs.


# When "setparam" and "setconfig" functions will be used?


# When "AllocateBuffer" and "Usebuffer" functions will be called?


# What is the role of awesome player in Stage fright?

Awesome Player: handles playing, pausing, stopping, and restarting media playback, while doing so in a different manner depending on the type of media. For audio, AwesomePlayer instantiates and invokes an AudioPlayer component that is used as a wrapper for any audio content. For video, AwesomePlayer invokes AwesomeRenderer‘s video rendering capabilities, while also directly communicating with the OMX subsystem through MediaSource/OMXCodec object (there is no proxy such as AudioPlayer in the case of video playback).

Source: https://stackoverflow.com/questions/24154326/what-is-awesomeplayer-in-android-stagefright-mutlimedia-framework


# How will you integrate an software codec or hardware codec with stage fright?


# How the player type is decided for playback of particular file format?




# What is Meta data and how will it be extracted?


# Will stage fright support all media file formats?


# How the thumbnail image will be created?


# What is role media scanner?

The media scanner service will read metadata from the file and add the file to the media content provider.

Source: https://developer.android.com/reference/android/media/MediaScannerConnection.html
https://stackoverflow.com/questions/13270789/how-to-run-media-scanner-in-android

# What is the role of media extractor?

MediaExtractor facilitates extraction of demuxed, typically encoded, media data from a data source.

Source: https://developer.android.com/reference/android/media/MediaExtractor.html

# What is the role of metadata retriever?

To retrieve meta data from a file... to grab information that isn't the actual file contents. Information like title, bitrate, etc.


Source: https://developer.android.com/reference/android/media/MediaMetadataRetriever.html

# What is the functionality of Audio flinger?

Audio flinger is the system component which manages the audio from Android user before handing it off to the kernel driver.


Source: https://stackoverflow.com/questions/11218923/what-is-audioflinger-and-why-does-it-fail-tone-prop-ack

# What is the functionality of surface flinger?

SurfaceFlinger's role is to accept buffers of data from multiple sources, composite them, and send them to the display.

When an app comes to the foreground, the WindowManager service asks SurfaceFlinger for a drawing surface. SurfaceFlinger creates a layer (the primary component of which is a BufferQueue) for which SurfaceFlinger acts as the consumer. A Binder object for the producer side is passed through the WindowManager to the app, which can then start sending frames directly to SurfaceFlinger.


Source: https://source.android.com/devices/graphics/arch-sf-hwc


# What is the role of Audio policy Service and Audio Policy Manger?



# Explain the State diagram of Phone state?


# How Application Processor and Communication Processor will be communicated?


# What are the native services that will start from media server?


# How player app and media player service will be communicated?


# What is Binder?


# What are the IPC methods used in android?


# How AV sync is managed during video playback?


# How the buffer management will be done for playback and recording?


# What is PMEM and ashmem?


# What is audio track and audio sink in the context of playback?


# What is mutex, and when it is used?


# What is parser and renderer, will these be OMX Components?


# How would you know whether s/w codec or h/w codec is used?


# What is frame buffer?


# What is egl swapbuffers?


# What is parser?


# What is recogniser?


# What is Payload?


# Explain Power Saving Machanisam in Audio/Video Playback?


# Explain Interrupts handling in Audio Playback?


# Why up sampling and down sampling is required while routing different audio streams data?


# Which is the flag we set when playback complete in OMX Component?


# What a mp4 file header have in it?


# What does Media Scanner do?


# Where is thumbnail stored in a picture?


# How AV sync is achieved in RTSP streaming?


# In RTSP streaming, what RTCP Packets comprise of ?


# What happens in JNI if many media player instances are created?


# Who selects the codecs for encoding for Author Engine


# What is the control path in RTP?

RTP is the protocol used for the actual transport and delivery of the real-time audio and video data. As the delivery of the actual data for audio and video is typically delay sensitive, the lighter weight UDP protocol is used as the Layer 4 delivery mechanism, although TCP might also be used in environments that suffer higher packet loss.

Source: http://www.informit.com/articles/article.aspx?p=169578&seqNum=3


# Which transport protocol is used in RTSP?

RTP

Source: http://www.informit.com/articles/article.aspx?p=169578&seqNum=3

# Which is preferred for streaming...? RTSP or HTTP?

RTSP

# Which is more preferred H263 or H264?


# What is container and codec?


# Can seek and pause operations be done in while streaming through rtsp?

Yes, RTSP pass very simple commands in addition to portions of the file.

Source: http://www.informit.com/articles/article.aspx?p=169578&seqNum=3

# What is interlaced and progressive streaming?


# How do you synchronize between the audio and video streamed data?


# Why RTSP is called real time?

It's in the name.

# Difference between HTTP n RTSP?

- RTSP stands for Real Time Streaming Protocol. One of the main uses for RTSP is to receive streaming video (e.g video on demand). A client establishes a connection with a media server and obtains data from the server and displays it.

- HTTP, on the other hand, is a stateless protocol. HTTP provides mechanism to download a media file over the internet. It would not be wrong to think of accessing media over HTTP as accessing a file over a network and playing it.


Source: https://stackoverflow.com/questions/6742010/how-to-understand-the-difference-between-the-two-online-video-rtsp-and-http
http://www.garymcgath.com/streamingprotocols.html

# What is RTSP protocol?

The Real Time Streaming Protocol (RTSP) is a network control protocol designed for use in entertainment and communications systems to control streaming media servers. The protocol is used for establishing and controlling media sessions between end points.


Source: https://en.wikipedia.org/wiki/Real_Time_Streaming_Protocol


# Source for questions
http://ccppcoding.blogspot.ca/2012/08/android-multimedia-interview-questions.html
