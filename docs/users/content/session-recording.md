---
title: Session Recording
layout: default
grand_parent: Users
parent: Content
nav_order: 2
---

The Session Recording feature provides a way to record all views, renderables, and time control to a file which can be played-back at a later time. OpenSpace is interactive software, meant to be used in real time. However, it can be difficult and time-consuming to recreate all of the camera movements and content settings when presenting content that is complex and/or prolonged. Session Recording can be used to automate some or all parts of a particular presentation.

## Recording a Session
Clicking the camera icon at the bottom menu bar will display the Session Recording menu. If using linux (which currently does not support the on-screen menu), a separate browser can be used to show the menu (http://localhost:4680/) or console commands can be used (see the advanced wiki page which is linked at the bottom of this page).
The top half of the menu has controls for starting a recording. Leave the "Text file format" option unchecked unless advanced features are being used (see section below if interested). Enter a filename (without extension) for the recording, and press the Record button when ready to start. The file will be saved in user/recordings/ directory.
Upon recording, the sub-menu disappears and the program can be used normally, with all actions & settings being recorded. Click the red "Stop recording" button when done, and a file of the specified name will be saved to user/recordings/ in the OpenSpace directory.

## Playback of a Recorded Session
There are two ways to handle the simulation time when playing back a session.  The most common method is to allow OpenSpace to set the simulation time (the current time visible in the menu) to exactly what it was when recorded ("Force time change to recorded time" checkbox). If the "Loop playback" option is checked, then the recording will continually repeat itself until manually stopped. The drop-down menu contains a list of files in the user/recordings/ directory that can be played.
Mouse camera control is disabled during playback.  The bottom menu (as well as log messages) will indicate when playback is finished.  You can abort the playback by clicking the 'Stop Recording' button, or entering: `openspace.sessionRecording.stopPlayback()` in the console. It is also possible to simply pause playback by clicking the menu button.

This [wiki page]({{ site.url }}/docs/components/session-recording) contains more advanced information about the session recording feature.
