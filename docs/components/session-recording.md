---
title: Session Recording
layout: default

parent: Components
nav_order: 5
---

This feature provides a method for recording all views, renderables, and time control to a file which can be played-back at a later time.

# Getting Started With This Feature
This feature is not yet included in the master branch.  The **feature/sessionRecording** branch must be checked-out from github. All subsequent build & run steps are identical to the standard instructions for OpenSpace.  See [this page]({{ site.url }}/docs/developers/compiling/general) for more details about configuring & building OpenSpace.

# Notes About Controls and File Management
Currently things are done with lua commands in the console, but controls in the GUI have just been added and are being tested as of May 2019.  Also as of this date, all record/playback files are saved in the `recordings` directory in the base OpenSpace location.  In Lua commands as well as in the GUI, only a filename is used without a path (this replaces the old behavior where the files could be located anywhere on the filesystem).

# Recording a Session
To start a recording, open the console with the **\`** key and enter:
`openspace.sessionRecording.startRecording('filename.dat');`
Now use OpenSpace as you would normally, moving the camera around, adjusting layer visibility, time, whatever.  When you want to finish recording, open the console again and enter:
`openspace.sessionRecording.stopRecording();`
and you can go back to using OpenSpace.

# Playback of a Recorded Session
There are two ways to handle the simulation time when playing back a session.  The most common method is to allow OpenSpace to set the simulation time (the current time visible in the menu) to exactly what it was when recorded.

1. To play back a session in this manner, use the syntax:
`openspace.sessionRecording.startPlayback('filename.dat');`
This function is available in the GUI with the "Force time change to match recording" box is checked.

Playback can also be performed without changing the current simulation time, in which case there are three different time options that can be used:

2. Recorded Time - recorded actions will play back relative to the time that the recording started, or the time that the playback started.  For example, if a layer was turned on 3 seconds after starting recording, then in the playback it will turn on 3 seconds after playback started (regardless of what simulation time is).  Example:
`openspace.sessionRecording.startPlaybackRecordedTime('filename.dat');`
This function is available in the GUI with the "Force time change to match recording" box is *un*-checked.

3. Application Time - recorded actions will play back relative to the time that the OpenSpace application started.  Consider the example of a session file that, at the time it was recorded, OpenSpace had been running for 10 minutes.  In a later session, a user starts OpenSpace and then starts playback of that file 1 minute later.  In this case, the playback will begin 9 minutes after that point (regardless of what simulation time is). Example:
`openspace.sessionRecording.startPlaybackApplicationTime('filename.dat');`

4. Simulation Time - recorded actions will be locked to the simulated time in OpenSpace, and will not play back unless the time is set to the specific date & time.  With this mode, it is necessary to manually set the simulation time to before what it was when recorded.  Playback will begin when the current simulation time reaches the recorded simulation time. Example:
`openspace.sessionRecording.startPlaybackSimulationTime('filename.dat');`

Currently mouse camera control is disabled during playback.  Log messages will indicate when playback is finished.  You can abort the playback by entering:
`openspace.sessionRecording.stopPlayback();`

# Known Issues
Problems currently occur when playing back files that contain some types of time manipulation.  If playback gets in a strange state because of this, then the `openspace.sessionRecording.stopPlayback()` command can be used to end playback.  Camera positions are time dependent, so things can look different if you don't playback in simulation mode and the time is set far in the past/future.

# ASCII File Format
When saving the recording in ASCII format instead of binary, the file becomes editiable and will contain a series of rows like this:

`camera 35.6259 0.125842 624861769.816 14150159.7269534 1447711.8646562 22214479.4404503 -0.2036835 -0.1934829 -0.7594912 -0.5867287 4.0000052e-07 F Earth`

Below is an explination of the 14 columns in the example entry:
00 - "camera" this denotes that this row represents a camera keyframe.
01 - "35.6259" - a timestamp representing the number of seconds since openspace has been launched.
02 - "0.125842" - a timestamp representing the number of seconds since the recording has been started.
03 - "624861769.816" - a time stamp reprenting the simulation time in openspace represented as J2000 seconds.
04 - "14150159.7269534" - the x coordinate of the camera position.
05 - "1447711.8646562" - the y coordinate of the camera position.
06 - "22214479.4404503" - the z coordinate of the camera position.
07 - "-0.2036835" - the x value of the camera's rotation vector.
08 - "-0.1934829" - the y value of the camera's rotation vector
09 - "-0.7594912" - the z value of the camera's rotation vector
10 - "-0.5867287" - the w value of the camera's rotation vector
11 - "4.0000052e-07" - a scale value (current scaling of the focus node; in this example the small value means the camera is zoomed far out)
12 - "F" - a value representing (T)rue or (F)alse for whether or not the camera is following the rotation of the focus node (e.g. rotating along with a planet to stay fixed at a spot on its surface)
13 - "Earth" - the openspace identifier of the camera's focus node
