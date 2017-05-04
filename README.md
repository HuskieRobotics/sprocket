Sprocket
========
A queue-based library for FRC robots, coded in LabVIEW 2015.

Part boilerplate, part library, **Sprocket** is intended to handle features
such as autonomous sequencing, manual / semi-auto controls and ... TODO.

Zero dependencies, but designed for interoperability with the LabVIEW WPI Robotics Library.

# Motivation
For seven years, Huskie Robotics has built its software from scratch for every
FRC build season.

For seven years, we have grappled with rising code complexity, and last-minute additions to our robot.

Last year, our behemoth three-tote autonomous for the 2015 Recycle Rush game hooked into every subsystem of our robot. We hacked it together with notifiers
and error-wire execution flow, and it was a sprawling mess.

(insert autonomous picture here)

**Sprocket** is an attempt to break the cycle of complexity. By condensing
complex event sequencing into queues, we hope to make autonomous,
semi-auto, and teleoperated actions more modular and more easily extensible.

# Getting Started

We have two versions of our library:
- **sprocket-r** - targeting the NI roboRIO
- **sprocket-c** - targeting the NI cRIO-FRC II (4-slot).

The NI cRIO-FRC (8-slot) controller is not supported.

Download the latest release from the [releases page](https://www.github.com/HuskieRobotics/sprocket/releases).

Unzip and you're ready to start building your swerve drive forklift.

Our library is organized into four main sections:

- Input - gather joystick input, transform into actions
- Sensor - gather sensor input
- Delegate - directing actions to separate subsystems
- Subsystem - calculate and perform subsystem actions

These three sections are organized into four VIs derived from the
auto-generated FRC robot project:
- Input -> Teleop.vi
- Sensor -> Sensor.vi (under Periodic Tasks.vi)
- Delegate -> Delegate.vi (under Periodic Tasks.vi)
- Subsystem logic -> Periodic Tasks.vi

With the following VIs intended for particular uses:
- Begin.vi - initializing motor controllers, actuators, sensors and queues
- Autonomous Independent.vi - sequencing autonomous actions
- Disabled.vi - stop all actuators / avert disaster

Vision processing is unsupported, but should be similar to Input.

# Documentation
API documentation hosted (hopefully) on [Github Pages](HuskieRobotics.github.io/sprocket).

Each VI has been (hopefully) painstakingly documented with context help and
comments for both users and contributors.

# Terminology

- Joystick - anything used to input human commands to the robot, be they
  gamepads or actual joysticks
- Driver - the human manning the joysticks

- Subsystem - portion of robot that can act independently

- Autonomous - fully independent robot actions without any driver input.
  Refers specifically to the autonomous period during FRC matches.
- Teleoperated (Teleop) - direct driver actions inputted through the joysticks.
- Semi-auto - sequenced actions occurring after a sequenced button input.
  Often used for automating complex tasks, or for things that depend on sensor
  checks.

# Contributors

Designed and built during the fall of 2015 by these people:

**FRC Team 3061 - Huskie Robotics**
- James Zhu (james.zhu.engineer@gmail.com)
- Dillon Hammond (dillonhammond@gmail.com)
- Ian Ren (Ian.Ren@navistar.com)
- Geoff Schmit (gcschmit@naperville203.org)

# License
Licensed under the MIT License (Expat). See LICENSE.md for the full text.

In short, you can do anything you want as long (commercial, free, private, etc.) as you include the original copyright (© Team 3061) and license notice (copy of LICENSE.md) in any copy of the source.
