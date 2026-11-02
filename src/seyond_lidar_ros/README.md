# About the package
  This is the primary package of the Seyond LiDAR ROS driver.

  **directory structure**

```
├── config                              // lidar config file
├── launch                              // ros1 & ros2 launch file
├── msg                                 // msg file
├── node                                // main file
│   ├── seyond_node.cc
│   └── seyond_test.cc
├── rviz                                // rviz config file
├── src
│   ├── driver
│   │   ├── driver_lidar.cc
│   │   ├── driver_lidar.h
│   │   ├── point_types.h
│   │   ├── ros1_driver_adapter.hpp
│   │   ├── ros2_driver_adapter.hpp
│   │   └── yaml_tools.hpp
│   ├── multi_fusion                    // for multiple lidars fusion
│   │   ├── ros1_multi_fusion.hpp
│   │   └── ros2_multi_fusion.hpp
│   ├── test                            // test node code
│   │   ├── ros1_test.hpp
│   │   └── ros2_test.hpp
│   └── seyond_sdk                      // seyond sdk
├── package.xml
├── CMakeLists.txt
├── LICENSE
└── README.md

```

# Compile

 1. **Copy**
  copy /seyond_lidar_ros/ directory to your ROS/ROS2 workspace
 
 2. **Build Seyond SDK**
  ```bash
  cd seyond_lidar_ros/src/seyond_sdk/build
  ./build_unix.sh
  cd -
  ```
  if not success, please refer to the latest Seyond SDK documentation

 3. **Build ros package**
  ```bash
  source /opt/ros/<ROS_DISTRO>/setup.sh
  // for ROS
  catkin_make install

  // for ROS2
  colcon build
  ```

# ROS2 실행과 RViz

워크스페이스에서 ROS 환경과 `install/setup.bash`를 source한 뒤 실행합니다. 기본 실행은 LiDAR 드라이버만 시작합니다.

```bash
ros2 launch seyond start.py
# RViz도 실행할 때
ros2 launch seyond start.py rviz:=true
```

소스 파일을 직접 실행할 때는 `--rviz` 옵션을 사용할 수 있습니다. 워크스페이스 루트 기준:

```bash
python3 src/seyond_lidar_ros/launch/start.py
python3 src/seyond_lidar_ros/launch/start.py --rviz
# 다른 launch 인자도 함께 전달 가능
python3 src/seyond_lidar_ros/launch/start.py --rviz lidar_ip:=172.168.1.10
```

`--rviz`는 직접 실행용 옵션입니다. `ros2 launch`에서는 `rviz:=true`를 사용합니다. 설치된 launch 파일에 변경을 반영하려면 패키지를 다시 빌드합니다.
