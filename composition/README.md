# Composition demo
This package features a demo of how to use composition in combination with a launch and header file, in order to create a turtle-spawning client.

## How to run
1. Open terminal
2. Source ROS2; `source /opt/ros/foxy/setup.bash`
3. Navigate to the "ros2playground" folder
4. `colcon build --symlink-install`
5. In a new terminal, navigate to the "composition" folder inside the ros2playground folder.
6. `. install/setup.bash` to source the ROS2 overlay
7. `ros2 launch composition turtlelaunch.py`

TODO: fix "Publisher already registered for provided node name." warning

