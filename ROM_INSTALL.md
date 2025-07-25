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
