cmake_minimum_required(VERSION 3.5)
project(composition)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(turtlesim REQUIRED)
find_package(rclcpp_components REQUIRED)
find_package(std_msgs REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

#include the 'include' directory
include_directories(include)

#create resource which references the libraries in the binary bin
set(node_plugins "")

#add spawn_turtle_nodelets as plugin
add_library(turtle_spawn SHARED
	src/spawn_turtle_nodelet.cpp)
target_compile_definitions(turtle_spawn
	PRIVATE "COMPOSITION_BUILDING_DLL")
ament_target_dependencies(turtle_spawn
	"rclcpp"
	"rclcpp_components"
	"turtlesim"
	"std_msgs")
rclcpp_components_register_nodes(turtle_spawn "composition::spawn_turtle_nodelet")
set(node_plugins "${node_plugins}composition::spawn_turtle_nodelet;$<TARGET_FILE:turtle_spawn\n>")



#tell where to put binaries
install(TARGETS
	turtle_spawn

	ARCHIVE DESTINATION lib
	LIBRARY DESTINATION lib 
	RUNTIME DESTINATION bin)

#install launch file
install(DIRECTORY launch
	DESTINATION share/${PROJECT_NAME}
	)

ament_package()