---
title: Joystick Navigation
layout: default

grand_parent: Users
parent: Navigation
nav_order: 2
---

# Joystick Navigation
In addition to the normal navigation in OpenSpace, using the keyboard and mouse, it is also possible to navigate using a game controller, such as an Xbox controller, PS4 controller or a SpaceMouse. If you want to use any of these supported controllers you need to include their corresponding asset file in a profile. This can be done in the profile editor in the launcher by editing the profile to include one of the joystick assets. All of the joystick assets are located in the sub-folder <code>data/assets/util/joysticks</code> inside the OpenSpace folder. It is important to include the right asset file for the type of game controller you are using. For example, the wireless Xbox asset will not work with a non-wireless Xbox controller and vice versa.

## Xbox Controller
The image below shows a map over the buttons and joysticks on a Xbox controller.

<img src="images/xbox.png" style="text-align:center; width:70%;"/>

Navigation using a Xbox controller in OpenSpace is defined in the Xbox asset file (<code>xbox.asset</code>) or the Xbox wireless asset file (<code>xbox-wireless.asset</code>). The table below gives an overview of what each button or joystick on the Xbox controller does in OpenSpace. NA in the table specifies that this button or joystick has no functionality in the default version of OpenSpace.

| Button or joystick | Description |
|--------------------|-------------|
| A | Toggle zoom friction |
| B | Toggle rotation friction |
| X | Switch focus to Earth |
| Y | Switch focus to Mars |
| LB | Pressed: Switch to local roll mode <br/>Released: Switch back to normal mode |
| LT | Zoom out |
| RB | Pressed: Switch to global roll mode <br/>Released: Switch back to normal mode |
| RT | Zoom in |
| Up | NA |
| Right | NA |
| Left | Toggle roll friction |
| Down | NA |
| Left Joystick up/down | Orbit around focus up/down |
| Left Joystick left/right | Orbit around focus left/right |
| Left Joystick Press | NA |
| Right Joystick up/down | Pan camera up/down |
| Right Joystick left/right | Pan camera left/right <br/>If LB or RB is pressed: Roll camera |
| Right Joystick Press | NA |
| Select | NA |
| Start | NA |

The LB and RB buttons switch the roll mode to local or global respectively. The difference between these two is that the local roll mode rolls the camera around the center of the screen, while the global roll mode rolls the camera around the current focus.

## PS4 Controller
The navigation using an Xbox or PS4 controller are very similar, the only difference is the layout of the controllers. Otherwise the functionality is the same. The image below shows a map over the buttons and joysticks on a PS4 controller.

<img src="images/ps4.png" style="text-align:center; width:75%;"/>

Navigation using a PS4 controller in OpenSpace is defined in the PS4 asset file (<code>ps4.asset</code>). The table below gives an overview of what each button or joystick on the PS4 controller does in OpenSpace. NA in the table specifies that this button or joystick has no functionality in the default version of OpenSpace.

| Button or joystick | Description |
|--------------------|-------------|
| Cross | Toggle zoom friction |
| Circle | Toggle rotation friction |
| Square | Switch focus to Earth |
| Triangle | Switch focus to Mars |
| L1 | Pressed: Switch to local roll mode <br/>Released: Switch back to normal mode |
| L2 | Zoom out |
| R1 | Pressed: Switch to global roll mode <br/>Released: Switch back to normal mode |
| R2 | Zoom in |
| Up | NA |
| Right | NA |
| Left | Toggle roll friction |
| Down | NA |
| Left Joystick up/down | Orbit around focus up/down |
| Left Joystick left/right | Orbit around focus left/right |
| Left Joystick Press | NA |
| Right Joystick up/down | Pan camera up/down |
| Right Joystick left/right | Pan camera left/right <br/>If L1 or R1 is pressed: Roll camera |
| Right Joystick Press | NA |
| Share | NA |
| Options | NA |
| Touch Pad | NA |
| PS | NA |

The L1 and R1 buttons switch the roll mode to local or global respectively. The difference between these two is that the local roll mode rolls the camera around the center of the screen, while the global roll mode rolls the camera around the current focus.

## SpaceMouse
The SpaceMouse is a joystick with 6 degrees of freedom that is sold by the company [3Dconnexion](https://3dconnexion.com/uk/spacemouse/). There are a few different versions of it and therefore there are a few different versions of the asset files that specify the navigation. The versions that are currently supported (since release 0.18.0) is the SpaceMouse Compact (<code>space-mouse-compact.asset</code>) and the SpaceMouse Enterprise (<code>space-mouse-enterprise.asset</code>). Both of these can be in wireless mode <code>space-mouse-compact-wireless.asset</code> and <code>space-mouse-enterprise-wireless.asset</code> respectively. The image below is a map of the different movements of the SpaceMouse and a translation of the terminology used by 3Dconnexion (3D) and the terminology used by OpenSpace (OS).

<img src="images/spacemouse-map.png" style="text-align:center;"/>

The table below gives an overview of what each button or joystick on the SpaceMouse does in OpenSpace. The Left and Right buttons are only supported for the Compact version of the SpaceMouse. However, if you are using the Enterprise version you can bind some of the buttons to a regular key on the keyboard and bind actions to them, read more about this [here](basic-navigation) and [here](../../builders/profile_syntax).

| Button or joystick | Description |
|--------------------|-------------|
| Push left/right | Orbit around focus left/right |
| Push back/forth | Orbit around focus up/down |
| Push up/down | Zoom in/out |
| Twist left/right | Pan camera left/right |
| Tilt left/right | Roll camera |
| Tilt up/down | Pan camera up/down |
| Left button | Switch to local roll mode (Default) |
| Right button | Switch to global roll mode |

The Left and Right buttons switch the roll mode to local or global respectively. The difference between these two is that the local roll mode rolls the camera around the center of the screen, while the global roll mode rolls the camera around the current focus.


# Issues and Solutions
Here is a list of some issues you can encounter related to the joysticks and some tips on how to fix them.

## Openspace Does Not React to the Controller Input
First thing to check here is that the controller is properly connected to the computer and that the correct asset file has been included to the profile and that the correct profile is run. If OpenSpace still does not react to the controller then it is possible that your controller has a different name than what OpenSpace expects. You can check the name of your controller when OpenSpace is running in any profile. Press the *F1* button on the keyboard and you will see the old GUI interface of OpenSpace pop up. In the window called **OpenSpace GUI**, press the empty checkbox next to **Joysticks Information**. This will open a new window and here all the connected joysticks will be listed. In this list you can search for your joystick and note down what name it has in the list, ignoring the number in the end. The items in the list called *3Dconnexion KMJ Emulator* or *Summed contributions* can be ignored. The next step is to change the name of the controller in the asset file. Start by opening the asset file corresponding to your controller in a text editor. You will need to change one line of code that specifies the controller name, below you can see an example for the Xbox controller (all other joystick assets look similar as well).

```
  asset.onInitialize(function()
    local controller = XBoxController;
    local name = "Xbox Controller"; -- Change this to the name of your controller

    local deadzoneJoysticks = 0.15
    local deadzoneTriggers = 0.05

    ...
```

## Openspace Keeps Spinning Even When the Joysticks Are Not Touched
This issue is caused by the deadzone being too small for the joysticks or the triggers on the controller. To fix it you can increase the size of the deadzone by editing one or two lines in the asset file. Start by opening the asset file corresponding to your controller in a text editor. You will need to change one or two lines of code that specify the deadzone size, below you can see an example for the PS4 controller (all other joystick assets look similar as well).

```
  asset.onInitialize(function()
    local controller = PS4Controller;
    local name = "Wireless Controller";

    local deadzoneJoysticks = 0.15 -- Increase this number to increase the deadzone for the joysticks
    local deadzoneTriggers = 0.05 -- Increase this number to increase the deadzone for the triggers

    ...
```

Adjust these values until the spinning stops and the feel of the navigation is good. Every time you change the values you need to restart OpenSpace. If the value is too small then the spinning might still occur at some occasions, if the value is too large then OpenSpace reaction to the input might feel delayed.
