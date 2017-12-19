ROS2 FreeRTPS
=============

## Install & Build

```
mkdir -p ~/ros2_embedded_ws/src

cd ~/ros2_embedded_ws
wget https://gist.githubusercontent.com/elehuitouze/faf63830f02cabee1f2ab133a3b253e1/raw/ros2_embedded.repos
vcs import ~/ros2_embedded_ws/src < ros2_embedded.repos
cd ~/ros2_embedded_ws/src/ros2/rosidl_typesupport && patch -p1 < ../../ros2_freertps/ros2_freertps/rosidl_typesupport.diff

cd ~/ros2_embedded_ws
touch src/ros2/rosidl_typesupport/rosidl_typesupport_c/AMENT_IGNORE
touch src/ros2/rosidl_typesupport/rosidl_typesupport_cpp/AMENT_IGNORE
touch src/ros2/rosidl/rosidl_generator_c/AMENT_IGNORE

. ~/ament_ws/install_isolated/local_setup.sh
ament build --symlink-install --isolated --cmake-args \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_SHARED_LIBS=OFF \
    -DCMAKE_TOOLCHAIN_FILE=~/ros2_embedded_ws/src/ros2_freertps/freertps/cm4.toolchain
