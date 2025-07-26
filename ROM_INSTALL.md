#### How to use
```
make distclean
git submodule update --init --recursive
cd Tools/simulation
rm -rf gz
git clone git@github.com:ROM-robotics/PX4-gazebo-models.git -b rom_release/1.15 gz
cp Tools/simulation/gz/4014_gz_x500_mono_cam_down ROMFS/px4fmu_common/init.d-posix/airframes/
make px4_sitl gz_x500_mono_cam_down
```
###### only experts လားလို့မေးလာလိမ့်မယ်။ ဟုတ်တယ်လို့ဖြေဖို့ y ကို နှိပ်လိုက်။
###### compile ok ပြီး run ရင် fail လိမ့်မယ် အဲ့ဒီအခါ အောက်က cp တစ်ကြောင်း run လိုက်ရင်ရပါပြီ။
```
cp Tools/simulation/gz/4014_gz_x500_mono_cam_down build/px4_sitl_default/rootfs/etc/init.d-posix/airframes/

cp ROMFS/px4fmu_common/init.d-posix/airframes/4014_gz_x500_mono_cam_down /home/mr_robot/PX4-Autopilot/build/px4_sitl_default/rootfs/etc/init.d-posix/airframes/
cp ROMFS/px4fmu_common/init.d-posix/airframes/4014_gz_x500_mono_cam_down build/px4_sitl_default/src/modules/simulation/gz_bridge/CMakeFiles/

# it will OK
make px4_sitl gz_x500_mono_cam_down
```


#### to check camera
```
gz topic -et /camera
ros2 run ros_gz_bridge parameter_bridge /camera@sensor_msgs/msg/Image@gz.msgs.Image
ros2 topic echo /camera

# or rviz2 image view with /camera topic, not /camera/image topic


```
## gzgarden bridge နဲ့ ပါက်သက်လို့ 

#### ROS2 HUMBLE 
က Default အားဖြင့် Gazebo Fortress ဖြစ်ပြီး packages တွေက ros-humble-ign-* ဖြစ်တယ်။

#### ROS2 Iron 
က Gazebo Fortress, Gazebo Garden ( experimental ) ဖြစ်ပါတယ်။

#### ROS2 Jazzy 
က Gazebo Harmonic ဖြစ်ပြီး သူ့ရဲ့ packages တွေက ros2-jazzy-gz-* ဖြစ်ပါတယ်။


#### PX4-Autopilot release/1.14
က Gazebo Fortress ပါတဲ့။ chatgpt က ပြောတာ။ Gemini ကပြောတာကတော့ Gazebo Graden ပါတဲ့။

#### PX4-Autopilot release/1.15
က Gazebo Fortress ပါတဲ့။ chatgpt က ပြောတာ။ Gemini ကပြောတာကတော့ သေချာမပြောထားပေမဲ့ Experimental အရ Gazebo Graden ပါတဲ့။

#### PX4-Autopilot release/1.16
က Gazebo Garden ပါတဲ့။ chatgpt က ပြောတာ။ Gemini ကပြောတာကတော့ Gazebo Harmonic ပါတဲ့။

#### how to fix ကြည့်ရတာ Harmonic နဲ့ Garden driver တို့ အလုပ်တွဲလုပ်နေပုံရတယ်။

sudo apt remove ros-humble-ros-gz-* ros-iron-ros-gz-*
sudo apt install ros-humble-ros-gzgarden-*
