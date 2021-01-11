# Sense, Interpret Act

The Control Systems team has one high level job: take inputs, process them, then produce outputs.

## The Control Systems Cycle

All development revolves around the *Control Systems Cycle*, which are the actions that your robot does tens of times per second.

### Sense

Sensing is about having your robot understand its surroundings. If a robot can’t understand its surroundings, it wouldn’t know what to do! In its most basic form, a robot can sense inputs from a joystick. A handheld joystick can send a decimal value between -1 and 1 on the vertical and horizontal axis for both sticks. It also can send whether a button is pressed or not.

However, the real power comes through sensors. As the name suggests, a sensor’s job is to sense things about the robot. With that data, the robot can make decisions without needing a driver to tell it so. But why would I want the robot to make decisions on its own? If a robot can make decisions on its own, then it means that the driver or operator has to spend less time worrying about the details of movement.

Let’s take an elevator in a skyscraper to understand the power of sensors. When you are in an elevator, you press a button and the elevator goes where you want it to. That is because an encoder, a sensor that can tell position, knows where the elevator is at all times. If it didn’t, you would have to manually control the velocity of the elevator at all times, which would be more work for you and be more likely to fail.

### Interpret

Once you can sense data, it is time to process it. In robotics, we use software to process our input data and turn it into an actionable plan. If the elevator in the previous section knows where it is, that doesn’t mean anything if it can’t establish a plan for its next action.

Interpreting data once again is simple and can grow to be very complex. In a typical drive-train robot, interpreting is a matter of taking joystick inputs, scaling them if necessary, and passing them to the drive-train motors. However, if you have an encoder, you may want to have a mechanism go to a specific position or velocity, and in your interpret step, you would do math to control the output to achieve your end goal.

### Act

Acting is where your robot actually moves. After all, the entire purpose of a robot is to move. Usually, you will control motors. Motors turn in a circle, and can spin super quickly, slowly, or somewhere in the middle. When you drive a car, the motors cause the wheels to turn, which propels the car forward.

The other kind of acting, which is more rare, is a solenoid. These are systems that can either be out or in. They do not have in-between states. The value of solenoids is that they are simpler to control (since they only have two values), and they can move quickly (explosive), but they are not designed for a lot of the tasks that we have in robotics.

## The Role of Software

As I mentioned earlier, software is responsible for the interpretation phase. All a robot program does is take inputs from sensors or joysticks, figure out the next step, and then tell the motors and solenoids to do their thing. While this is simple in theory, the difficulty and fun in the process comes from getting to figure out exactly what needs to happen in the interpretation phase. Do you remember those input output flow charts from elementary school math? Software is basically a input output flow chart for a robot.

The good thing is that for a getting started project, interpretation is very easy. As you learn, it gets more complex but you will still be able to handle it.

## The Role of Electronics

Now that we understand the role of software, we now need to understand the role of electronics.

Electronics is responsible for the infrastructure that allows this system to exist. All of the sensors are chosen in a collaboration between software, electronics, and mechanics interests.

They are also responsible for the micro-controller and power delivery. A micro-controller is a computer that is designed to run the robot program. As of the time of writing this post, it is called the RoboRIO. The RoboRIO, the sensors, and the motors all require power, so it is also the responsibility of Electronics students to provide power to the robot.

Wiring, however, is the most time-consuming part of the Electronics Process. Wires act like the nervous system of a robot. They allow the RoboRIO to talk to sensors and motors, and act as the bridge between the three steps of the Control Systems Cycle. During your time learning electronics, you will learn how to make many different types of wires and the purposes for each.


## Sources
- [https://alexbeaver.com/blog/control-systems-cycle](https://alexbeaver.com/blog/control-systems-cycle)