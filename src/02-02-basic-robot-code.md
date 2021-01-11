# Anatomy of a Basic Robot Program

For those of you who made one of the VEX ProtoBots, this code will look familiar.

> Lines that start with // are comments and are used to explain, but have no impact on how the robot actually works.

```c
////////////////////////////////////////////////////////////////////
// Protobot.c                                                     //
////////////////////////////////////////////////////////////////////
//                                                                //
// This code is the end code for a fully functional VEX protobot. //
//                                                                //
// It demonstrates many of the basic concepts of a robot program. //
////////////////////////////////////////////////////////////////////


///////////////////////////////////////////////////////////////////////////////////////////////
// Configuring Your Robot                                                                    //
///////////////////////////////////////////////////////////////////////////////////////////////
// In RobotC, lines that start with #pragma tell RobotC how your robot is set up.            //
//                                                                                           //
// It has information about where motors are sensors are plugged in, as well as their names. //
///////////////////////////////////////////////////////////////////////////////////////////////
#pragma config(Motor,  port2,           RightDrive,    tmotorServoContinuousRotation, openLoop)
#pragma config(Motor,  port4,           LeftDrive,     tmotorServoContinuousRotation, openLoop)
#pragma config(Motor,  port5,           IntakeWheel,   tmotorServoContinuousRotation, openLoop)
#pragma config(Motor,  port7,           Arm,           tmotorServoContinuousRotation, openLoop)
#pragma config(Sensor, dgtl5,  					ArmUp,         sensorTouch)
#pragma config(Sensor, dgtl6,  					ArmDown,       sensorTouch)

/////////////////////////////////////////////////////////////////////////////////////////////////
// task main()                                                                                 //
/////////////////////////////////////////////////////////////////////////////////////////////////
// When you start running your code, your robot will need to know where to start reading from. //
//                                                                                             //
// In VEX, wherever you see task main is the place where                                       //
// the code starts reading from                                                                //
/////////////////////////////////////////////////////////////////////////////////////////////////
task main()
{
    //////////////////////////////////////////////////////////////////////////////
    // Variables                                                                //
    //////////////////////////////////////////////////////////////////////////////
    // Variable keep track of information. They act like a bucket.              //
    //                                                                          //
    // The word int means that the information in the bucket is a whole number. //
    //                                                                          //
    // For JoystickValues, the values range from -127 to 127.                   //
    // For Buttons and LimitSwitches, the value is either 0 or 1.               //
    //////////////////////////////////////////////////////////////////////////////
    int rightJoystickValue = 0;
    int leftJoystickValue = 0;
    int leftButtonUp = 0;
    int leftButtonDown = 0;
    int rightButtonUp = 0;
    int rightButtonDown = 0;
    int armUpLimitSwitch = 0;
    int armDownLimitSwitch = 0;

    //////////////////////////////////////////////////////////////////////////////////////////////////
    // This code here means that your program will run forever.                                     //
    //                                                                                              //
    // Just like when you read an instruction manual, you start at the beginning and go to the end. //
    // However, if you aren't specifically told to repeat something, you wouldn't know to do so.    //
    // By telling our robot to repeat, it will run our code forever.                                //
    //////////////////////////////////////////////////////////////////////////////////////////////////
    while(1==1)
    {
        ///////////////////////////////////////////////////////////////////////////////////
        // Get joystick and sensor values                                                //
        ///////////////////////////////////////////////////////////////////////////////////
        // This code gets values from the joystick and puts those values into variables. //
        // Once the values are in a variable, we can easily process them.                //
        //                                                                               //
        // The vexRT word tells our robot to look at the joystick.                       //
        // Calls to SensorValue tell our robot to look at the value from an sensor.      //
        ///////////////////////////////////////////////////////////////////////////////////
        rightJoystickValue = vexRT[Ch2];
        leftJoystickValue = vexRT[Ch3];
        leftButtonUp = vexRT[Btn5U];
        leftButtonDown = vexRT[Btn5D];
        rightButtonUp = vexRT[Btn6U];
        rightButtonDown = vexRT[Btn6D];

        armUpLimitSwitch = SensorValue[ArmUp];
        armDownLimitSwitch = SensorValue[ArmDown];


        ////////////////////////////////////////////////////////////////////
        // Interpret and Act                                              //
        ////////////////////////////////////////////////////////////////////
        // This big block of code tells our robot to process our inputs   //
        // (sensors and joystick values) and identify an output (motors). //
        //                                                                //
        // The if statements work to identify the driver's intention.     //
        // Does the driver want to move the arm up? Is it safe to move    //
        // the arm up? All of that is evaluated within the parentheses    //
        // next to the word if.                                           //
        //                                                                //
        // The calls, such as motor[Arm] = 127; tell the robot to move    //
        // a motor at a certain power, ranging from -127 to 127.          //
        //                                                                //
        // Else acts as an aditional way to program logic, where the      //
        // robot will look and see if that logic is valid if and only     //
        // if the if statement above it was not true.                     //
        ////////////////////////////////////////////////////////////////////
        motor[RightDrive] = rightJoystickValue;
        motor[LeftDrive] = leftJoystickValue * -1;

        if((leftButtonUp == 1) && (armUpLimitSwitch == 0))
            {
                motor[Arm] = 127;
            }
        else if ((leftButtonDown == 1) && (armDownLimitSwitch == 0))
            {
                motor[Arm] = -127;
            }
        else
            {
                motor[Arm] = 0;  // if you don't set the motors to 0, they will keep running forever
            }

        if(rightButtonUp == 1)
            {
                motor[IntakeWheel] = 127;
            }
        else if (rightButtonDown == 1)
            {
                motor[IntakeWheel] = -127;
            }
        else
            {
                motor[IntakeWheel] = 0;
            }
        }
  }

```