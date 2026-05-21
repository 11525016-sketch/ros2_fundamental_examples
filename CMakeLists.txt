cmake_minimum_required(VERSION 3.8)
project(ros2_fundamental_examples)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclpy REQUIRED)
find_package(std_msgs REQUIRED)

include_directories(include)

# --- INSTALLATION SECTION ---

# 1. Install the scripts directory to share
install(
  DIRECTORY ros2_fundamental_examples/scripts
  DESTINATION share/${PROJECT_NAME}
)

# 2. Install the include directory
install(DIRECTORY include/
  DESTINATION include
)

# 3. Install the Python executables
# This tells ROS where to find your nodes when you run 'ros2 run'
install(PROGRAMS
  ros2_fundamental_examples/py_minimal_publisher.py
  ros2_fundamental_examples/py_minimal_subscriber.py
  DESTINATION lib/${PROJECT_NAME}
)

# 4. Install Python modules for import
ament_python_install_package(${PROJECT_NAME})

# --- TESTING AND EXPORT ---

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  set(ament_cmake_copyright_FOUND TRUE)
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_export_include_directories(include)

ament_package()