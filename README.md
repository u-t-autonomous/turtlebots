# turtlebots
# Network Configuration:
1. On your remote PC, run the following command:
  ifconfig
Copy and make note of the remote PC's IP Address
2. Open the remote PC's .bashrc file:
  nano .bashrc
3.Add the following lines to the end of the .bashrc file if they are not already there:

  export ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
  
  export ROS_HOSTNAME=IP_OF_REMOTE_PC
  
4. Turn on turtlebot and connect it to a monitor via HDMI.
5. Repeat steps 1-3, this time on the turtlebot, and add these lines to the .bashrc instead:

  export ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
  
  export ROS_HOSTNAME=IP_OF_TURTLEBOT
  
# Date and Time:

Any time the turtlebot is turned off, it's date and time will become out of sync, since we are using a local network, we have to manually set it's date and time each time it's turned on. To do so, run this command on the turtlebot:

  sudo date MMDDhhmmyyyy.ss

Currently working on a better way to do this.

# SLAM:
1. ssh into turtlebot with the following command:

  ssh pi@IP_OF_TURTLEBOT 
 
2. On a new terminal, run the turtlebot bringup node:

  roslaunch turtlebot3_bringup turtlebot3_robot.launch
 
3. On a new terminal, launch SLAM:

  export TURTLEBOT3_MODEL=waffle
  roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping

4. On a new terminal, run the teleoperation node:

  export TURTLEBOT3_MODEL=waffle
  roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
  
This will allow you to control the robot with the WASD and X keys

5. Move the robot around and a map of it's surroundings will automatically be generated

6. To Save Map:

  rosrun map_server map_saver -f ~/map

This last argument can be changed to whatever name/save location you desire.

# Navigation:

1. ssh into turtlebot with the following command:

  ssh pi@IP_OF_TURTLEBOT 
  For the current setup(3/3/20): 192.168.0.150
2. On a new terminal, run the turtlebot bringup node:

  roslaunch turtlebot3_bringup turtlebot3_robot.launch
  
3. On a new terminal, launch navigation node:

  roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
  
This last argument is the path to your map file, if you saved it somewhere else or with a different name you will need to adjust the command accordingly.

4. Click the 2D Pose Estimate button.

5. Click on the approxtimate point in the map where the TurtleBot is located and drag the cursor to indicate the direction the turtlebot is facing.

6. Optionally, you can move the robot back and forth with tools like the turtlebot3_teleop_keyboard node to give the robot a better sense of it's position on the map.

7. You should now be able to send the turtlebot navigation goals with the 2d Nav goal button at the top.
