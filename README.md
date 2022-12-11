## find-object (standalone) 

Find-Object project, visit the [home page](http://introlab.github.io/find-object/) for more information.

## find_object_2d (ROS1 package)

### Install

Binaries:
```bash
# ROS Kinetic:
 $ sudo apt-get install ros-kinetic-find-object-2d
# ROS Jade:
 $ sudo apt-get install ros-jade-find-object-2d
# ROS Indigo:
 $ sudo apt-get install ros-indigo-find-object-2d
# ROS Hydro:
 $ sudo apt-get install ros-hydro-find-object-2d
```

Source:

 * If you want SURF/SIFT on Indigo/Jade/Kinetic (Hydro has already SIFT/SURF), you have to build [OpenCV](http://opencv.org/) from source to have access to *nonfree* module. Install it in `/usr/local` (default) and the Find-Object should link with it instead of the one installed in ROS.

     * On Indigo/Jade, I recommend to use latest 2.4 version ([2.4.11](https://github.com/Itseez/opencv/archive/2.4.11.zip)) and build it from source following these [instructions](http://docs.opencv.org/doc/tutorials/introduction/linux_install/linux_install.html#building-opencv-from-source-using-cmake-using-the-command-line). Find-Object can build with OpenCV3+[xfeatures2d](https://github.com/Itseez/opencv_contrib/tree/master/modules/xfeatures2d) module, but find_object_2d package will have libraries conflict as cv-bridge is depending on OpenCV2. If you want OpenCV3, you should build ros [vision-opencv](https://github.com/ros-perception/vision_opencv) package yourself (and all ros packages depending on it) so it can link on OpenCV3.

     * On Kinetic, I recommend to use OpenCV3+[xfeatures2d](https://github.com/Itseez/opencv_contrib/tree/master/modules/xfeatures2d) module (*to confirm* OpenCV3 installed with ROS already includes SIFT/SURF, so no need to rebuild OpenCV). You can also install OpenCV2, but find_object_2d package will have libraries conflict as cv-bridge is depending on OpenCV3. Thus if you want OpenCV2 on Kinetic, you should build ros [vision-opencv](https://github.com/ros-perception/vision_opencv) package yourself (and all ros packages depending on it) so it can link on OpenCV2.

```bash
# Install ROS Groovy/Hydro/Indigo/Jade/Kinetic (catkin build):
 $ cd ~/catkin_ws
 $ git clone https://github.com/introlab/find-object.git src/find_object_2d
 $ catkin_make

# Install ROS Fuerte (in a directory of your "ROS_PACKAGE_PATH"):
 $ svn checkout -r176 http://find-object.googlecode.com/svn/trunk/ros-pkg/find_object_2d
 $ rosmake find_object_2d
```

### Run
```bash
 $ roscore &
 # Launch your preferred usb camera driver
 $ rosrun uvc_camera uvc_camera_node &
 $ rosrun find_object_2d find_object_2d image:=image_raw
```
See [find_object_2d](http://wiki.ros.org/find_object_2d) for more information.

## find_object_2d (ROS2 package)

### Install

Binaries:
```bash
To come...
```

Source:

```bash
# Install ROS Foxy/Galactic/Humble (colcon build):
 $ cd ~/ros2_ws
 $ git clone https://github.com/introlab/find-object.git src/find_object_2d
 $ colcon build
```

### Run
```bash
 # Launch your preferred usb camera driver
 [...]
 
 # Launch find_object_2d node:
 $ ros2 launch find_object_2d find_object_2d.launch.py image:=/camera/color/image_raw
 
 # Draw objects detected on an image:
 $ ros2 run find_object_2d print_objects_detected --ros-args -r image:=/camera/color/image_raw
```
#### 3D Pose (TF)
A RGB-D camera is required. Example with Realsense D400 camera:
```bash
 # Launch your preferred usb camera driver
 ros2 launch realsense2_camera rs_launch.py align_depth.enable:=true
 
 # Launch find_object_2d node:
 $ ros2 launch find_object_2d find_object_3d.launch.py \
     rgb_topic:=/camera/color/image_raw \
     depth_topic:=/camera/aligned_depth_to_color/image_raw \
     camera_info_topic:=/camera/color/camera_info
 
 # Show 3D pose in camera frame:
 $ ros2 run find_object_2d tf_example
```

## CI Latest

  <table>
    <tbody>
        <tr>
           <td>Linux</td>
           <td><a href="https://github.com/introlab/find-object/actions/workflows/cmake.yml"><img src="https://github.com/introlab/find-object/actions/workflows/cmake.yml/badge.svg" alt="Build Status"/> <br> <a href="https://github.com/introlab/find-object/actions/workflows/ros1.yml"><img src="https://github.com/introlab/find-object/actions/workflows/ros1.yml/badge.svg" alt="Build Status"/> <br> <a href="https://github.com/introlab/find-object/actions/workflows/ros2.yml"><img src="https://github.com/introlab/find-object/actions/workflows/ros2.yml/badge.svg" alt="Build Status"/>
           </td>
        </tr>
        <tr>
           <td>Windows</td>
           <td><a href="https://ci.appveyor.com/project/matlabbe/find-object/branch/master"><img src="https://ci.appveyor.com/api/projects/status/hn51r6p5c0peqctb/branch/master?svg=true" alt="Build Status"/>
           </td>
        </tr>
     </tbody>
  </table>

