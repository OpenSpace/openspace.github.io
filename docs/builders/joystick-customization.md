---
title: Joystick Customization
layout: default

parent: Builders
nav_order: 4
---

# Customizing the joystick navigation
This page will go in-depth into how you can customize the joystick navigation to your own liknig. If you want to read more about how the default joystick navigation works in OpenSpace see [Joystick Navigation](../../users/navigation/joysticks).

To start you need an asset file to edit. If you are using a game controller that matches one of the assets that OpenSpace already provides (Xbox, PS4, SpaceMouse), it is recomended that you start with a copy of that matching asset and place it in your <code>user\data\assets</code> folder. However, if the game controller you will use does not match an already provided asset, it is still recommended to start with one of the assets that are provided, such as the <code>space-mouse-compact</code> asset. The steps would be that same in both of these cases with the exception that the new game controller would need some initial setup, see [Setup new joystick type](#Setup-new-joystick-type).

## Bind a camera movement to a joystick axis
To bind a camera navigation movement to an axis of the joystick you will need the function <code>openspace.navigation.bindJoystickAxis</code> that takes in eight arguments. Below is a list that describes each argument in detail.

1. The name of the controller you want to use (for more info see [Joystick Navigation](../../users/navigation/joysticks)). It is important that this name matches the name that OpenSpace detects as the name for the gmae controller you want to use.

2. The index of which axis of the game controller you want to bind the camera movement to. This is distinct for the type of game controller you will use and to find these values for a new joystick type see [Setup new joystick type](#Setup-new-joystick-type).

3. What type of camera movement you want to bind to the axis. This must be one of the identifiers in the following list:

| Identifier   | Description                                                             |
|--------------|-------------------------------------------------------------------------|
| "None"       | Unbind the axis. Defulat value when no camera movement type is used.    |
| "Orbit X"    | Move the camera in the left/right direction in relation to the focus, while still keping the same distance. The camera will move as if it was orbiting the focus. |
| "Orbit Y"    | Move the camera in the up/down direction in relation to the focus, while still keping the same distance. The camera will move as if it was orbiting the focus. |
| "Zoom"       | Move the camera closer or further away from the focus                   |
| "Zoom In"    | Move the camera closer to the focus                                     |
| "Zoom Out"   | Move the camera further away from the focus                             |
| "LocalRoll"  | Roll the camera (clockwise) in relation to the middle of the view       |
| "GlobalRoll" | Roll the camera (clockwise) in relation to the focus                    |
| "Pan X"      | Tilt the camera left/right in relation to the view                      |
| "Pan Y"      | Tilt the camera up/down in relation to the view                         |

4. (Optional) Whether or not this axis should be inverted. This is a common setting in video games. Defualts to <code>false</code>.

5. (Optional) The type of joystick that this axis represents on the game controller. The options are either <code>"JoystickLike"</code> or <code>"TriggerLike"</code>. A joystick is <code>"TriggerLike"</code> if it can only be pressed or pushed in one direction. A <code>"JoystickLike"</code> axis can be pushed in two directions for example, left and right, or up and down. Defualts to <code>"JoystickLike"</code>.

6. (Optional) Whether or not this axis is "sticky". In most cases this should be set to <code>false</code>. An axis is "sticky" if, when you let go of it, the values it represent in the software does not go back to the defualt. Another sign is that the longer you push it, the value and therfore the movemennt gets more and more extreme over time and does not stop or slow down when you let go. Defualts to <code>false</code>.

7. (Optional) Whether or not the movement for this axis should be reversed. In the case of a <code>"JoystickLike"</code> axis this is the same as inverting the axis. However, in the case of a <code>"TriggerLike"</code> axis this can reverse the movement of the camera that pushing the trigger makes. For example, if the <code>"LocalRoll"</code> movement type is bound to a trigger, you can only roll OpenSpace clockwise when you press the trigger, to make it go counter-clockwise you would need to reverse the movement. Defualts to <code>false</code>.

8. (Optional) Sensitivity value for this axis. Can be used to fine tune the sensitivity for all axes individually. Defualts to <code>1.0</code>.

Here is an example with the SpaceMouse:
~~~lua
  local SpaceMouse = {
    Push = {0, 1, 2}, -- left/right, back/forth, up/down
    Twist = {5}, -- left/right
    Tilt = {4, 3}, -- left/right, back/forth

    LeftButton = 0,
    RightButton = 1
  }

  asset.onInitialize(function()
    local controller = SpaceMouse;
    local name = "SpaceNavigator";

    openspace.navigation.bindJoystickAxis(name, controller.Push[1], "Orbit X", false, "JoystickLike", true, false, 40.0);
    openspace.navigation.bindJoystickAxis(name, controller.Push[2], "Orbit Y", false, "JoystickLike", true, false, 40.0);
    openspace.navigation.bindJoystickAxis(name, controller.Twist[1], "Pan X", true, "JoystickLike", true, false, 40.0);
    openspace.navigation.bindJoystickAxis(name, controller.Tilt[2], "Pan Y", false, "JoystickLike", true, false, 35.0);
    openspace.navigation.bindJoystickAxis(name, controller.Push[3], "Zoom", false, "JoystickLike", true, false, 40.0);
    openspace.navigation.bindJoystickAxis(name, controller.Tilt[1], "LocalRoll", false, "JoystickLike", true, false, 35.0);
  end)
~~~

## Bind a property to a joystick axis
It is possible to controll an OpenSpace property using a joystick on a game controller, to do that you will need the function <code>openspace.navigation.bindJoystickAxisProperty</code> that takes in seven arguments. Below is a list that describes each argument in detail.

1. The name of the controller you want to use (for more info see [Joystick Navigation](../../users/navigation/joysticks)). It is important that this name matches the name that OpenSpace detects as the name for the controller.

2. The index of which axis you want to bind. This is distinct for the type of controller you use and to find these values for a new controller see [Setup new joystick type](#Setup-new-joystick-type).

3. The full identifer of the property you want to bind to the axis.

4. (Optional) The minimum value you want to allow to set this property to with the axis. Defualts to <code>0.0</code>.

5. (Optional) The maximum value you want to allow to set this property to with the axis. Defualts to <code>100.0</code>.

6. (Optional) Whether or not this axis should be inverted. This is a common setting in video games. Defualts to <code>false</code>.

7. (Optional) Whether or not the property change should be forwareded to other connected nodes or sessions. This is similar to the <code>"isLocal"</code> parameter for actions. Defualts to <code>true</code>.

Here is an example with the Earth scale:
~~~lua
  local XBoxController = {
    LeftThumbStick = { 0 , 1 },
    RightThumbStick = { 2, 3 },
    LeftTrigger = 4,
    RightTrigger = 5,
    A = 0,
    B = 1,
    X = 2,
    Y = 3,
    LB = 4,
    RB = 5,
    Select = 6,
    Start = 7,
    LeftStickButton = 8,
    RightStickButton = 9,
    DPad = {
      Up = 10,
      Right = 11,
      Down = 12,
      Left = 13
    }
  }

  asset.onInitialize(function()
    local controller = XBoxController;
    local name = "Xbox Controller";

    -- Bind Right trigger to Earth Scale
    openspace.navigation.bindJoystickAxisProperty(name, controller.RightTrigger, "Scene.Earth.Scale.Scale", 0.1, 100, false, true);
  end)
~~~

## Bind a script to a joystick button
Binding a custom script to a joystick button is done with the function <code>openspace.navigation.bindJoystickButton</code> that takes 6 arguments. Below is a list that describes each argument in detail.

1. The name of the controller oyu want to use (for more info see [Joystick Navigation](../../users/navigation/joysticks)). It is important that this name matches the name that OpenSpace detects as the name for the controller.

2. The index of which button you want to bind. This is distinct for the type of controller you use and to find these values for a new controller see [Setup new joystick type](#Setup-new-joystick-type).

3. The script that should be executed when the button is activated.

4. Description of the script that the button will execute when the button is activated.

5. (Optional) When the button should be interpreted as activated, defualts to <code>"Press"</code>. This must be one of the identifiers in the following list:

| Identifier | Description                                     |
| ---------- | ----------------------------------------------- |
| "Idle"     | When the button is **not** pressed              |
| "Press"    | When the button is pressed                      |
| "Repeat"   | When the button is held pressed                 |
| "Release"  | When the button was pressed and is not released |

6. (Optional) Whether or not the script should be forwareded to other connected nodes or sessions. This is similar to the <code>"isLocal"</code> parameter for actions. Defualts to <code>true</code>.

# Setup new joystick type
When connecting a new game controller or joystick to OpenSpace the first step is to get a good mapping of what buttons and axis the controller have and what indicies each button and axis have. The easiest way to get a good overview of this is with the connected joysticks list in OpenSpace. You can access this list by pressing the *F1* button on the keyboard and you will see the old GUI interface of OpenSpace pop up. In the window called **OpenSpace GUI**, press the empty checkbox next to **Joysticks Information**. This will open a new window and here all the connected joysticks will be listed. In this list you can search for your joystick. The items in the list called *3Dconnexion KMJ Emulator* or *Summed contributions* can be ignored. Once you have found your game controller you will see two numbered lists of axes and buttons with a slider and button respectivly. See image below:

**IMAGE**

Now we can begin to explore the game controller. What we want to have in the end is a list of all the axes and buttons and which index in the list they correspond to. To start it can be good to have descriptive names for each button and axis you can find on the game controller, or atleast the ones that you are interested in.

Now that we have a clear image of what the game contorller is capable of, we need to figure out how is is connected to OpenSpace. Lets start with the axes, we want to identify which index in the list cooresponds to each axes on the game controller. Choose one axis and move it around a little bit on the game controller, you should see one or more sliders reacting to your movement in the list in OpenSpace. If you see several sliders reacting to your movement, try to isolate your movement to only one direction such as up/down or left/right. When you are cetain of which index reacted to your input to the axis you can note that down and move on to the next axis.

For the buttons we will use the same strategy, puch one button a few times and see which of the buttosn in OpenSpace reacts, note down that number and move on to the next. Now that we have a clear image of how each button ans axis relate to the list in OpenSpace we could build a map in our asset.

In each joystick asset file that OpenSpace provide there will be a section at the top that looks similar to this:

~~~lua
-- Name of the controller
local XBoxController = {
  -- Axes
  LeftThumbStick = { 0 , 1 }, -- left/right, up/down
  RightThumbStick = { 2, 3 }, -- left/right, up/down
  LeftTrigger = 4,
  RightTrigger = 5,

  -- Buttons
  A = 0,
  B = 1,
  X = 2,
  Y = 3,
  LB = 4,
  RB = 5,
  Back = 6,
  Start = 7,
  LeftStickButton = 8,
  RightStickButton = 9,
  DPad = {
    Up = 10,
    Right = 11,
    Down = 12,
    Left = 13
  }
}
~~~

This is the map of the game controller that tells OpenSpace how each axis and button relate to the indicies in the the list that OpenSpace sees. Now with all the information you now have about your game controller you can make your own map. Start with a name for your contrrolelr, in the example above it is called <code>XBoxController</code>. Then you can start with the axes, in the example above there are four joysticks that each have one to two axes. There is the two joystick that can move both left/right, and up/down, then there are the two trigger that only have one axis each. To add an axis to the list you add its name (no spaces or special characters) and set that equal to the index it coresopnded to in the OpenSpace list. So it would look like:

~~~lua
local NameOfController = {
  -- Axes
  NameOfAxis1 = { 0, 1 }, -- This joystick on the game controller has two axes, one for left/right and one for up/down
  NameOfAxis2 = 2, -- This axis is a trigger
  ...

  -- Buttons
  NameOfButton1 = 0,
  NameOfButtons2 = 1,
  ...

  -- Collection of buttons
  NameOfButtonCollection1 = {
    NameOfButton1InCollection1 = 5,
    NameOfButton2InCollection1 = 6,
    ...
  },
  NameOfButtonCollection2 = {
    NameOfButton1InCollection2 = 8,
    NameOfButton2InCollection2 = 9,
    ...
  }

  ...
}
~~~

Now that you have defined your map over your game controller you can start customizing it and bind camera movemtns to the axes and scripts to the buttons, as the guide above decribes.

If you have created a new asset file for a game controller thay OpenSpace does not already have, consider contributing it to the repository so other users can use it too. Just open a new pull request or contact us on our slack and we can help you get it into the program.
