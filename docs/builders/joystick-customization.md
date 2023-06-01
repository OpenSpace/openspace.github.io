---
title: Joystick Customization
layout: default

parent: Builders
nav_order: 4
---

# Customizing the joystick navigation
This page will go in-depth into how to customize the joystick navigation to your own liknig. If you want to learn more about the default joystick navigation in OpenSpace, see [Joystick Navigation](../../users/navigation/joysticks).

To start, you will need an asset file to edit. If you are using a controller that matches one of the assets that OpenSpace already provides (Xbox, PS4, SpaceMouse, etc.) it is recomended that you start with a copy of that matching asset and place it in your `user\data\assets` folder. However, if the controller you will use does not match any provided asset, it is still recommended to start with one of the assets that are provided, such as the `space-mouse-compact` asset. The steps will be that same in both cases with the exception that the new controller will need some additional setup, see [Setup new joystick type](#Setup-new-joystick-type) before moving on to the customization.

## Bind camera navigation to a joystick axis
To bind a camera movement to an axis of the joystick you will need the function `openspace.navigation.bindJoystickAxis` that takes eight arguments. Below is a list that describes each argument in detail. If you are customizing an already existing asset then you probably do not want to add a new camera movement binding, insteda you might want to alter the pre-existing ones. To customize a camera movement it is most likely only nececary to change a few of the input value in the pre-existing function call to the function `openspace.navigation.bindJoystickAxis`.

1. The name of the controller you want to use (for more info on how to find this name, see [Joystick Navigation](../../users/navigation/joysticks)). It is important that this name matches the name that OpenSpace detects for the controller.

2. The index of which axis on the controller you want to bind the camera movement to. This is distinct for the type of controller you will use and to find these values for a new controller see [Setup new joystick type](#Setup-new-joystick-type). If you are using an already supported controller, you can use the "map" at the top of the asset to find the indices. Either you can put in the incicies directly or you can use the map with the descriptive name such as `controller.RightTrigger` or `controller.LeftThumbStick.LeftRight`.

3. What type of camera movement you want to this axis to do. This defines how the camera will move in OpenSpace, when you move the specified axis of the controller. Must be one of the identifiers in the following list:

| Identifier   | Description                                                             |
|--------------|-------------------------------------------------------------------------|
| "None"       | Unbind the axis, no camera movement is applied. Defulat value from the start. |
| "Orbit X"    | Move the camera in the left/right direction in relation to the focus, while still keping the same distance. The camera will move as if it was orbiting the focus. |
| "Orbit Y"    | Move the camera in the up/down direction in relation to the focus, while still keping the same distance. The camera will move as if it was orbiting the focus. |
| "Zoom"       | Move the camera closer or further away from the focus                   |
| "Zoom In"    | Move the camera closer to the focus                                     |
| "Zoom Out"   | Move the camera further away from the focus                             |
| "LocalRoll"  | Roll the camera (clockwise) in relation to the middle of the view       |
| "GlobalRoll" | Roll the camera (clockwise) in relation to the focus                    |
| "Pan X"      | Turn the camera left/right in relation to the view                      |
| "Pan Y"      | Turn the camera up/down in relation to the view                         |

4. (Optional) Whether or not this axis should be inverted. This is a common setting in video games. Defualts to `false`.

5. (Optional) The type of joystick that this axis represents on the controller. The options are either `"JoystickLike"` or `"TriggerLike"`. A joystick is `"TriggerLike"` if it can only be pressed or pushed in one direction. A `"JoystickLike"` axis can be pushed in two directions for example, left **and** right, or up **and** down. Defualts to `"JoystickLike"`.

6. (Optional) Whether or not this axis is "sticky". In most cases this should be set to `false`. An axis is "sticky" if, when you let go of it, the values it represent in the software does not go back to the defualt. Another sign is that the longer you push it, the value and therfore the movemennt gets more and more extreme over time and does not stop or slow down when you let go. Defualts to `false`.

7. (Optional) Whether or not the movement for this axis should be reversed. In the case of a `"JoystickLike"` axis this is the same as inverting the axis (which was argument number 4). However, in the case of a `"TriggerLike"` axis this can reverse the camera movement for the trigger. For example, if the `"LocalRoll"` movement type is bound to a trigger, you can only roll OpenSpace clockwise when you press the trigger, since the trigger can only go in one direction. To make the camera roll counter-clockwise instead, you would need to reverse the movement with this argument. Defualts to `false`.

8. (Optional) Sensitivity value for this axis. Can be used to fine-tune the sensitivity for all axes individually. Defualts to `1.0`. A value larger that `1.0` would lead to the axis becomes more sensitive and a value that is smaller than `1.0` would lead to the axis beaing less sensitive to input. There is also a global sensitivity property that can be adjusted in the GUI, under *Settings*, *Navigation Handler*, *Orbital Navigator* and then *Joystick Sensitivity* (identifier `NavigationHandler.OrbitalNavigator.JoystickSensitivity`). Note that this will affect all connected controllers and all of their axes.

Here is an example asset with the SpaceMouse:
~~~lua
  local SpaceMouse = {
    -- Axes
    Push = {
      LeftRight = 0,
      BackForth = 1,
      UpDown = 2
    },
    Twist = 5,
    Tilt = {
      LeftRight = 4,
      BackForth = 3
    },

    -- Buttons
    LeftButton = 0,
    RightButton = 1
  }

  asset.onInitialize(function()
    local controller = SpaceMouse;
    local name = "SpaceNavigator";

    openspace.navigation.bindJoystickAxis(name, controller.Push.LeftRight, "Orbit X", false, "JoystickLike", true, false, 40.0)
    openspace.navigation.bindJoystickAxis(name, controller.Push.BackForth, "Orbit Y", false, "JoystickLike", true, false, 40.0)
    openspace.navigation.bindJoystickAxis(name, controller.Twist, "Pan X", true, "JoystickLike", true, false, 40.0)
    openspace.navigation.bindJoystickAxis(name, controller.Tilt.BackForth, "Pan Y", false, "JoystickLike", true, false, 35.0)
    openspace.navigation.bindJoystickAxis(name, controller.Push.UpDown, "Zoom", false, "JoystickLike", true, false, 40.0)
    openspace.navigation.bindJoystickAxis(name, controller.Tilt.LeftRight, "LocalRoll", false, "JoystickLike", true, false, 35.0)
  end)
~~~

## Bind a property to a joystick axis
To controll an OpenSpace property using an axis on a controller you will need the function `openspace.navigation.bindJoystickAxisProperty` that takes seven arguments. Below is a list that describes each argument in detail.

1. The name of the controller you want to use (for more info on how to find this name, see [Joystick Navigation](../../users/navigation/joysticks)). It is important that this name matches the name that OpenSpace detects for the controller.

2. The index of which axis on the controller you want to bind the property to. This is distinct for the type of controller you are using and to find these values for a new controller see [Setup new joystick type](#Setup-new-joystick-type). If you are using an already supported controller, you can use the "map" at the top of the asset to find the indices. Either you can put in the incicies directly or you can use the map with the descriptive name such as `controller.RightTrigger` or `controller.LeftThumbStick.LeftRight`.

3. The full identifer for the property you want to controll to this axis on the controller.

4. (Optional) The minimum value allowed to be set for this property using theis axis. Defualts to `0.0`.

5. (Optional) The maximum value allowed to be set for this property using theis axis. Defualts to `100.0`.

6. (Optional) Whether or not this axis should be inverted. This is a common setting in video games. Defualts to `false`.

7. (Optional) Whether or not the property change should be forwareded to other connected nodes or sessions. This is similar to the `"isLocal"` parameter for actions. Defualts to `true`.

Here is an example asset with the Earth scale bound to the right trigger on an Xbox controller:
~~~lua
  local XBoxController = {
    -- Axes
    LeftThumbStick = {
      LeftRight = 0,
      UpDown = 1
    },
    RightThumbStick = {
      LeftRight = 2,
      UpDown = 3
    },
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

  asset.onInitialize(function()
    local controller = XBoxController;
    local name = "Xbox Controller";

    -- Bind Right trigger to Earth Scale
    openspace.navigation.bindJoystickAxisProperty(name, controller.RightTrigger, "Scene.Earth.Scale.Scale", 0.1, 100, false, true);
  end)
~~~

## Bind a script to a joystick button
Binding a custom script to a joystick button is done with the function `openspace.navigation.bindJoystickButton` that takes 6 arguments. Below is a list that describes each argument in detail.

1. The name of the controller you want to use (for more info on how to find this name, see [Joystick Navigation](../../users/navigation/joysticks)). It is important that this name matches the name that OpenSpace detects for the controller.

2. The index of which button on the controller you want to bind the script to. This is distinct for the type of controller you are using and to find these values for a new controller see [Setup new joystick type](#Setup-new-joystick-type). If you are using an already supported controller, you can use the "map" at the top of the asset to find the indices. Either you can put in the incicies directly or you can use the map with the descriptive name such as `controller.A` or `controller.DPan.Left`.

3. The script that should be executed when the button is activated.

4. Description of the script that the button will execute when the button is activated.

5. (Optional) When the button should be interpreted as activated, defualts to `"Press"`. This must be one of the identifiers in the following list:

| Identifier | Description                                     |
| ---------- | ----------------------------------------------- |
| "Idle"     | When the button is **not** pressed              |
| "Press"    | When the button is pressed                      |
| "Repeat"   | When the button is held pressed                 |
| "Release"  | When the button was pressed and is not released |

6. (Optional) Whether or not the script should be forwareded to other connected nodes or sessions. This is similar to the `"isLocal"` parameter for actions. Defualts to `true`.

# Setup new joystick type
When connecting a new controller or joystick to OpenSpace the first step is to get a good mapping of what buttons and axes the controller have and what indicies they are connected to. To get an overview of the joysticks and its axes and buttons you can use the connected joysticks list in OpenSpace. You can access this list by pressing the *F1* button on the keyboard and you will see the old GUI interface of OpenSpace pop up. In the window called **OpenSpace GUI**, press the empty checkbox next to **Joysticks Information**. This will open a new window and here all the connected joysticks will be listed. In this list you can search for your joystick. The items in the list called *3Dconnexion KMJ Emulator* or *Summed contributions* can be ignored. Once you have found your controller you will see two numbered lists of axes and buttons with a slider and button respectivly. See image below:

![](images/joysticks-list.png)

Now we can begin to explore the game controller. What we want to have in the end is a list of all the axes and buttons and which index in the list they correspond to. To start it can be good to have descriptive names for each button and axis you can find on the game controller, or atleast the ones that you are interested in.

Now that we have a clear image of what the game contorller is capable of, we need to figure out how is is connected to OpenSpace. Lets start with the axes, we want to identify which index in the list cooresponds to each axes on the game controller. Choose one axis and move it around a little bit on the game controller, you should see one or more sliders reacting to your movement in the list in OpenSpace. If you see several sliders reacting to your movement, try to isolate your movement to only one direction such as up/down or left/right. When you are cetain of which index reacted to your input to the axis you can note that down and move on to the next axis. Below is an image to show how it can look like when one of the axes have been moved:

![](images/joysticks-axis.png)

For the buttons we will use the same strategy, puch one button a few times and see which of the buttosn in OpenSpace reacts, note down that number and move on to the next. Now that we have a clear image of how each button ans axis relate to the list in OpenSpace we could build a map in our asset. Below is an image to show how it can look like when one of the buttons are pressed:

![](images/joysticks-button.png)

In each joystick asset file that OpenSpace provide there will be a section at the top that looks similar to this:

~~~lua
-- Name of the controller
local XBoxController = {
  -- Axes
  LeftThumbStick = {
    LeftRight = 0,
    UpDown = 1
  },
  RightThumbStick = {
    LeftRight = 2,
    UpDown = 3
  },
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

This is the map of the game controller that tells OpenSpace how each axis and button relate to the indicies in the the list that OpenSpace sees. Now with all the information you now have about your game controller you can make your own map. Start with a name for your contrrolelr, in the example above it is called `XBoxController`. Then you can start with the axes, in the example above there are four joysticks that each have one to two axes. There is the two joystick that can move both left/right, and up/down, then there are the two trigger that only have one axis each. To add an axis to the list you add its name (no spaces or special characters) and set that equal to the index it coresopnded to in the OpenSpace list. So it would look like:

~~~lua
local NameOfController = {
  -- Axes
  NameOfJoystick1 = { -- This joystick on the controller has two axes, one for left/right and one for up/down
    LeftRight = 0,
    UpDown = 1
  },
  NameOfTrigger1 = 2, -- This axis is a trigger
  ...

  -- Buttons
  NameOfButton1 = 0,
  NameOfButtons2 = 1,
  ...

  -- Collection of buttons
  NameOfButtonCollection = {
    NameOfButton1InCollection = 5,
    NameOfButton2InCollection = 6,
    ...
  }

  ...
}
~~~

Now that you have defined your map over your game controller you can start customizing it and bind camera movemtns to the axes and scripts to the buttons, as the guide above decribes.

If you have created a new asset file for a game controller thay OpenSpace does not already have, consider contributing it to the repository so other users can use it too. Just open a new pull request or contact us on our slack and we can help you get it into the program.
