# LRW
The little Red Wagon Project

# Version 0.5

The working topic for this project is Little Red Wagon.  But this name has a copyright attached, so we call it LRW.  The latest suggestion is "Sidecar"

This is the fifth attempt to organize what was discussed from the first design meeting through subsequent emails, further design meetings, and up to the present date of February 27, 2019

Please chime in with opinions, improvements, or discussion points!

# The basics:

## 1 - The LRW will generically have 4 wheels although more can be added, in pairs.  

To begin with, this is a simplification for the steering software.

## 2 - Each wheel CAN be driven by a motor, and each wheel CAN be steered.  

The software will be set up to do that, but it will be flexible enough to steer the wheels in pairs as well.  The wheels can also be non-steered.  Driven wheels that have pivots may swing themselves by skid-steer type steering or have a steering motor adjust the direction.  Fixed driven wheels CAN be steering with skid type steering, but there is a bunch of slip that needs to be compensated for.  This option is supported but will only be developed if there is interest.

## 3 - Suspension is an option but not a requirement. 

Any type of suspension is fine, as long as it fits into the module (or the two modules if the wheels are paired up).  

## 4 - The LRW will generically fit through a standard doorway in a home or apartment.  

24 inches wide fits well through 28 inch doors with enough spare room that you don't scuff up the door frame with the door open.  It can be any width you wish, but 24 inches is 'default', if there is such a thing on a completely configurable vehicle

## 5 - The length of the LRW is whatever you need it to be.  

A reasonable minimum would be the width.  A generic proportion would be about twice as long as wide.  If it gets up above 3 times as long as it is wide, it becomes difficult to move through an apartment.  Again, completely configurable

## 6 - Depth, completely configurable from dragging the base on the ground through unstable heights.  

The motor connection to the driven wheels is somewhere around half the height of the wheel.  The axles on non-driven wheels are at about half the height of the wheel if axles are used.  The vehicle may have higher clearance between, or may keep the clearance low to lower the center of gravity.

 

  

# Modularity and contracts

In order to determine if a module fulfills the requirements for it's use, there needs to be a contract that it must meet.  It is a bit cumbersome, but it allows parallel development on different portions of the design, or on different designs for the same function, at the same time.

An update to allow a single CPU as master and slaves with software objects separated

## 1 - The wheels are added in pairs.  

While a module per wheel would be most flexible, a module for a pair of wheels may be less costly and offer most of the benefits.  This is a complication for the software, but it should not be onerous.  

1. The wheel pair will have a connection (assumed to be electrical) for each driven wheel and a connection (assumed to be electrical) for the feedback on each driven wheel, if feedback is used.  
2. The wheel pair will mount to the frame at two corners.  This makes the mount the same for 2 single wheels as well as for a pair of wheels.
3. Drive motors for the wheels modules can span a pair of wheels, with a single motor and controller.  The Slave module can be mounted onboard the motor module or mounted with the Master Module.
4. The wheel modules, or rather the individual wheels, are intended to be individually steerable.  If the wheels are added as a pair, a method of steering that does not need to tie the pair of wheels together is the goal.  Mechanical linkage can be accommodated in the software.  A single steering mechanism spanning two wheels will be ‘tied’ to the first of the wheels, whichever is numbered first.

## 2 - The frame of LRW is what every other module is attached to.  

Tentatively a simple box with wheel modules secured to the sides or beneath.  Wood, aluminum, bamboo, paper mache .. whatever you like.

1. The frame has mounting available for 2 or 4 wheels, depending on the design.
2. The frame has a mount for the master board
3. The frame has a mount for the battery or batteries used to power the vehicle, and wiring to support connecting the battery(s) to the master module and the master module to the motor module(s)

## 3 - Master module.  

The frame will have a computer that is referred to as the Master module.  It will contain the basic functions for steering and driving.

1. Multiple Slave modules can be used if each wheel has it's own steering and motor drive. 
2. The selections for communicating between modules - so far - include USB, Bluetooth and wifi.  
3. An app for bluetooth and a smart phone will eventually be required to configure the software - number of wheels, which are steerable, which are driven, length and width and height, ground clearance, size of wheels, etc.  
4. The master module is the basic brains and the way that interfaces connect to the system.  So it has compact flash storage, USB connectivity, bluetooth, wifi, and any other interface that is required to the LRW
5. It has been suggested that this entire project can fit into an Arduino Mega, and that Master and Slave, with all of the overhead associated with command and control between different CPUs ... is simply not required.  I’m willing to be convinced, but I see implementation issues with this approach.  This is intended to be covered by item 7

## 4 - Slave Motor Module. 

The Motor module is intended to 'steer' 1 wheel separately, with feedback for direction, and drive the wheel at a setpoint speed, with speed feedback.  

1. The module has a 2 pin power connector, a 3 pin speed feedback, a 2 pin steering connector, and a 3 pin steering feeedback connector for the motor.  
2. 4 individually steerable and driveable wheels would require 4 slave motor modules.  
3. If a communication interface is required for steering or speed/distance feedback, like I2C or Canbus, the interface will be built onto this module.  This is one solution.  
4. Other feedback suggested has been a USB mouse that tracks a disc coupled to each wheel and makes use of the ubiquity of the mouse and the USB interface.  We hope that access to these common computer peripherals enables easy access for all.  Servo motors do not strictly require rotational feedback, and so the interface to the Slave module is simplified.

## 5 - Slave Guidance module.  

This slave would support an interface to a 'handle' for manual guidance of the vehicle, to guide the LRW forward and back, left and right, but have the LRW follow the handle instead of the user dragging the LRW.  The guidance modules could also implement a joystick control, or interfaces to apps on smart phones, or remote control via a cloud connection. 

## 6 - Slave Path module.  

This module allows for GPS tracking, path planning, sonar, lidar, vision, and any number of other advances detection of surroundings.  It could attempt more challenging routing paths, do dead reckoning for position in the absense of GPS connection, log the path that is taken so that it can be repeated, log the positions of objects that are encountered via vision or lidar, and any number of interesting tasks.

## 7 – All-in-one.  

A large Master module (sufficient memory, bluetooth, wifi, enough I/O pins, etc) with a set of defined motors and steering may be able to make use of separate software modules, but have them all running on the Master Module.  This avoids having communication defined between master and slave modules.  Other software timing issues may arise.   

 As of version 0.5, item 7 will be used for the minimum viable product - MVP



  

# Parts

## Off-the-shelf parts, accessible in most places, are the goal.  

Anyone, anywhere should be able to build a version of this LRW with parts that are recycled, upcycled, purchased, or built.

## Wheelchair motors, electric bicycle hub motors, windshield wiper motors, cordless drills, used Hot Wheels type electric cars, servo motors and gearboxes from ebay. 

These are the drive motors envisioned to start with.  Small variable speed controllers for DC motors, from amazon or ebay, remote control vehicles, etc are envisioned to drive the motors with batteries of 6V - 30V, lead acid or rechargable batteries of some sort.  Remote control cars, drill batteries, electric scooter or bicycle batteries, wheelchair batteries.  Items that are available wherever you are and that you can afford.

Feedback for the wheels, where the computer can see how many times the wheel has turned, are a bit more of a challenge to source sturdy, proven and reliable designs.  

Encoders and resolvers work well, but they are expensive and you need to figure out how to mount them on the motor, or between the motor and the wheel.  USB Computer mice have been suggested.  It is hoped that some testing can prove this as a viable option or not.

## Regenerative braking, and braking in general, must be addressed.  

DC motors can have their positive and negative shorted together to give a parking type of brake.  Servos ... I think they need power to maintain their position.  As do brushless DC motors and AC motors.  Friction brakes, parking brakes ... are important for when there is no power available for braking.  But recovering energy from regenerative braking is likely an important part, an essential part, of the system design.  I’d like to have it included ... but I am uncomfortable making it optional ... and I’m uncomfortable making it mandatory.

## The design decision was to purchase a hoverboard and use it as the front pair of wheels for the MVP.  

Interfacing to the drive electronics via the gyro sensors is simple, direct, and should be fairly standard across the multiple brands.  This will save a lot of time and development if it works.  These hoverboards are available in a lot of places, and should be available used or surplus since the safety issues have been well publicized.

 As of version 0.5, the latest of the design decisions is to use a small remote control truck available inexpensively from Amazon.  A bit of research into which signals on the radio remote control which pins on the controller has been done.  So far, the signals are from the radio are available on the microprocessor.  The signals follow through the driver chips to the motors.  The radio does forward/reverse with no throttle percentage.  It is full forward, stopped, or full reverse.  The steering is full left, center, or full right.  Again, no percentage .. just left or right signals or no signal.

I expect that those 3.3V inputs will be put into the arduino as control and the output of the arduino will be 3.3V signals to the driver chips, which put out 5V from the battery pack to the 3 motors.  No further parts are needed to move or steer the truck.  An Arduino Uno is expected to handle the software and interface requirements beginning with a simple sketch.

  

# Software

## Software is key in the system.  

A flexible and simple user interface is something that all devices require.  It is also helpful to have a user interface to walk the user through troubleshooting, gather data on sensors or controllers that are not performing as required.

## Python 

Python is a powerful and popular language that can be implemented on computers from the desktop to tiny computer chips that can only deal with one sensor.  

Using Python will not tie the design to any particular brand of computer, although I expect that we will start with a Raspberry PI and a couple of arduinos.  Any computer that interfaces to what is required and can communicate to the system can be used.  Cloud based or stand-alone.

The implementation of the software will be done with objects, in the python language.  

## Objects 

Object-oriented programming, and using objects to encapsulate the program and the data required for controlling the details of driving the motors and tracking their progress.  This is the goal.  And it splits the software between over-all direction, path selection, and the details of timing and implementing things.

Separate objects can all be run on the same master to begin with, and have the objects split out onto other CPUs as they are added.  This also skips the complexity of getting a network between dissimilar CPUs up and running as a first step.

 

  

# Minimum Viable Product (MVP)

 All projects should have a MVP targeted.  This has changed quite a bit.  My interpretation of an MVP that I can build locally, for a reasonable cost, is:

 \- A small Remote control truck, complete with NiCd batteries, remote control, and charger

\- An arduino Uno.  The signals are mostly figured out, the board appears to be simple and I think I can modifiy it to disconnect the microcontroller from the driver chips.  I can then solder the signals from the Microcontroller/radio system and solder the outputs from the arduino through a resistor divider for each output to signal the driver chips instead.   

\- An inexpensive PWM controller, perhaps 2, from ebay, no longer appears to be required.



# Use cases that have been mentioned:

 \- follow me during a marathon run, holding clothing, food and water supplies, and generally causing a buzz in the watching crowd

 \- a gardening wheelbarrow to transport plants, flowers, mulch, etc  This may require a trailer dragged behind for cargo and the user sitting on the LRW to give it enough weight to pull the load

 \- a 'go-cart' for kids to play around with, that does not go fast enough to really hurt them.  Like a DIY Barbie corvette that looks more like a HUMMER.



# Youtube playlist

https://www.youtube.com/playlist?list=PLlBdSZoO29ytspA1yN-0S8WM5ofmJUtT2
