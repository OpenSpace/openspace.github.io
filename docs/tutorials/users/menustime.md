---
title: Using the Menus - Time
layout: default
parent: User Tutorials
grand_parent: Tutorials

has_children: false
has_toc: false
nav_order: 4
---


# Using the Menus - Time
{: .no_toc }

This section will cover using the menus to manipulate time in OpenSpace.

1. TOC
{:toc}

## Time Menu
 - Clicking on the date at the bottom of the screen will open the Time menu.
 - The Time menu can be popped out using the button in the upper right next to x
 - The Time menu is separated into sections for changing the date, the rate of time, and two helper buttons.
 - The different sections will be described below. The realtime and now helper buttons set the rate of time to one second per seconds and set the date to the computers current date respectively.

## Changing the Date/Time
 - There are different ways to change the date/time using the Time menu.
 - Clicking the arrow above or below any of the components of the date will increment that part of the date. 
    - For instance, to advance time one month, click the arrow above the month. 
    - To advance time one day, click the arrow above the day of the month.
    - Holding shift while clicking the arrow will change the time instantly rather then interpolate the change.
 - Typing values into the components of the date is another way to change the date.
    - Type the value you want and hit enter, time will change instantly.
    - You must enter valid values for time and date, invalid values (such as 55 for day, or 75 for minutes) will result in unexpected behavior.
 - The next way to change the date is to use the calendar function of the Time menu.
    - To show the calendar, click the expand icon on the right next to the seconds component of the date.
    - Clicking on a date in the calendar will interpolate the date.
    - Hold shift while clicking to instantly set the date.
 - The most flexible way to change the date is to use the lock icon on the left, next to the year component of the date.
    - Clicking the lock icon will expand the menu with three new buttons.
    - Once activated, you can now change the components of the date without the simulation updating.
    - Once you have changed all the components to the exact date/time you want to use, then press the 'Interpolate' or 'Set' buttons to change the date in the simulation.

## Changing the Rate of Time
 - There are four components of the Time menu under "Simulation Speed"
 - The main two components are the "Display Unit" dropdown, and the "Unit/second" sliders
    - To change the rate of time, adjust the dropdown to your desired unit, and then use the slider to specify the value you want. For time to go in reverse, use thhe "Negative Unit/second" slider.
    - The third component is the "Quick Adjust" Slider. 
 - Once you have chosen your desired rate, you can use the "Quick Adjust" knob to make a momentary change to the rate.
    - When you release the mouse the rate will return to your chosen value.
 - The fourth component is are the arrow and play/pause buttons.
    - The arrow will cycle through predetermined rates of time specified by the profile.
    - The play/pause button will toggle the rate of time between zero and your specified value. 
    - Just like using the space bar, holding shift while clicking the play/pause button will make an instant change to the rate instead of an interpolated change.

## Time Options in the Settings Menu
 - The TimeManager section of the Settings Menu contains four values relevant to the Time menu. Lower values will make things happen faster, higher values will make things happen slower.
  - '_Default Time Interpolation Duration_' affects how long the interpolation will take when changing the date.
  - '_Default Delta Time Interpolation Duration_' affects how long the interpolation will take when changing the rate of time.
  - '_Default Pause Interpolation Duration_' affects how long the interpolation will take when pausing, which is changing the rate of time from your chosen value to zero.
  - '_Default Unpause Interpolation Duration_' affects how long the interpolation will take when unpausing, which is changing the rate of time from zero to your chosen value.

## Video

<iframe width="740" height="530" src="https://www.youtube.com/embed/z0daNU4OFFA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

| Video time | Description |
|:-------------|:------------------|
| 0:00 | Open and popout the Time menu. |
| 0:11 | Changing the date by typing. |
| 0:31 | Changing the date with arrows. |
| 1:11 | Changing the date with calendar. |
| 1:41 | Setting the date with the lock icon. |
| 2:20 | Changing the rate of time |
| 0:35 | Using the quick adjust slider |
| 3:02 | Pausing time. |
| 3:30 | Rate of time arrows. |
| 4:08 | Realtime/Now buttons. |
| 4:35 | Changing Time Manager settings. |

---
<span class="v-align-middle">
[Time in OpenSpace](/docs/tutorials/users/time){: .btn .btn-purple }
</span>
<span class="fs-6"><-- Previous |</span>
<span class="fs-6">Next -->  </span>
<span class="v-align-middle">
[Using the Menus - Datasets](/docs/tutorials/users/menusdatasets){: .btn .btn-purple }
</span>

