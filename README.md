# TurtleBot3
<img src="https://raw.githubusercontent.com/ROBOTIS-GIT/emanual/master/assets/images/platform/turtlebot3/logo_turtlebot3.png" width="300">

- Active Branches: noetic, humble, jazzy, main(rolling)
- Legacy Branches: *-devel

## Open Source Projects Related to TurtleBot3
- [turtlebot3](https://github.com/ROBOTIS-GIT/turtlebot3)
- [turtlebot3_msgs](https://github.com/ROBOTIS-GIT/turtlebot3_msgs)
- [turtlebot3_simulations](https://github.com/ROBOTIS-GIT/turtlebot3_simulations)
- [turtlebot3_manipulation](https://github.com/ROBOTIS-GIT/turtlebot3_manipulation)
- [turtlebot3_manipulation_simulations](https://github.com/ROBOTIS-GIT/turtlebot3_manipulation_simulations)
- [turtlebot3_applications](https://github.com/ROBOTIS-GIT/turtlebot3_applications)
- [turtlebot3_applications_msgs](https://github.com/ROBOTIS-GIT/turtlebot3_applications_msgs)
- [turtlebot3_machine_learning](https://github.com/ROBOTIS-GIT/turtlebot3_machine_learning)
- [turtlebot3_autorace](https://github.com/ROBOTIS-GIT/turtlebot3_autorace)
- [turtlebot3_home_service_challenge](https://github.com/ROBOTIS-GIT/turtlebot3_home_service_challenge)
- [hls_lfcd_lds_driver](https://github.com/ROBOTIS-GIT/hls_lfcd_lds_driver)
- [ld08_driver](https://github.com/ROBOTIS-GIT/ld08_driver)
- [open_manipulator](https://github.com/ROBOTIS-GIT/open_manipulator)
- [dynamixel_sdk](https://github.com/ROBOTIS-GIT/DynamixelSDK)
- [OpenCR-Hardware](https://github.com/ROBOTIS-GIT/OpenCR-Hardware)
- [OpenCR](https://github.com/ROBOTIS-GIT/OpenCR)

## Documentation, Videos, and Community

### Official Documentation
- ⚙️ **[ROBOTIS DYNAMIXEL](https://dynamixel.com/)**
- 📚 **[ROBOTIS e-Manual for Dynamixel SDK](http://emanual.robotis.com/docs/en/software/dynamixel/dynamixel_sdk/overview/)**
- 📚 **[ROBOTIS e-Manual for TurtleBot3](http://turtlebot3.robotis.com/)**
- 📚 **[ROBOTIS e-Manual for OpenMANIPULATOR-X](https://emanual.robotis.com/docs/en/platform/openmanipulator_x/overview/)**

### Learning Resources
- 🎥 **[ROBOTIS YouTube Channel](https://www.youtube.com/@ROBOTISCHANNEL)**
- 🎥 **[ROBOTIS Open Source YouTube Channel](https://www.youtube.com/@ROBOTISOpenSourceTeam)**
- 🎥 **[ROBOTIS TurtleBot3 YouTube Playlist](https://www.youtube.com/playlist?list=PLRG6WP3c31_XI3wlvHlx2Mp8BYqgqDURU)**
- 🎥 **[ROBOTIS OpenMANIPULATOR YouTube Playlist](https://www.youtube.com/playlist?list=PLRG6WP3c31_WpEsB6_Rdt3KhiopXQlUkb)**

### Community & Support
- 💬 **[ROBOTIS Community Forum](https://forum.robotis.com/)**
- 💬 **[TurtleBot category from ROS Community](https://discourse.ros.org/c/turtlebot/)**

# COMMAND FOR NAVIGAE
เปิด slam(เก็บ map)

	ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
	
เปิด keyboard

	ros2 run turtlebot3_teleop teleop_keyboard
	
save map

	ros2 run nav2_map_server map_saver_cli -f ~/map_folder/map_name
	
Run nav

	ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=$HOME/map.yaml
	
	ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=/home/phubet2547/map/map_world.yaml


Gazebo
	ros2 launch turtlebot3_gazebo empty_world.launch.py
	
	ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
	
	ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
	
	ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
	
bringup in sbc

	ros2 launch turtlebot3_bringup robot.launch.py
	
check position

	ros2 run tf2_ros tf2_echo odom base_link
	
watch waypoints

	ros2 topic echo /waypoints

## COMMAND FOR ROS
colcon build แบบ select package

	colcon build --packages-select my_pkg_py
	
create python pkg ทำที่ (ros2/ws/src)

	ros2 pkg create my_pkg_py --build type ament_python --dependencies rclpy
	
แก้เวลา colcon build ผิดที่

	rm -r build/ install/ log/
	
rename node at runtime สามารถ run node เดียวกันได้หลายครั้งโดยไม่ชึ้น  warning

	ros2 run my_pkg_py excecutable_name --ros-args -r __node:=new_node_name
	
colcon build แบบ symlink ทำให้เมื่อแก้ code จะไม่ต้อง colcon build ใหม่ทุกครั้ง only python_pkg

	colcon build --packages-select my_pkg_py --symlink-install
 
	rm -rf build/ install/ log/ #เวลา ล้าง CACHE
	
Rqt and rqt_graph (ดู node ที่กำลังทำงาน)

	rqt_graph
	
Turtlesim

	sudo apt install ros-humble-turtlesim #(install turtle)
 
	ros2 run turtlesim turtle_teleop_key #(บังคับเต่า)
 
	ros2 run turtlesim turtlesim_node  #(แสดงเต่า)

ดู msg

	#ros2 interface show example_interfaces/msg/[กด tab ดู]
	
Pub_sub

สร้างไฟล์

	touch filename
 
ทำให้ไฟล์ excecutable

	chmod +x file_name
	
ดู topic info #จะบอกว่า node ไหนเป็น pub อันไหนเป็น sub และ type ของ msg ที่ส่ง

	#phubet@phubet-Victus-by-HP-Gaming-Laptop-15-fa1xxx:~$ ros2 topic info /data
	#Type: example_interfaces/msg/String
	#Publisher count: 1 
	#Subscription count: 1

ดู msg ที่ pub ส่งใน topic นั้นๆ

	ros2 topic echo /data
	
ดู rate ของ msg

	ros2 topic hz /data

ดู size msg ที่ส่งใน msg
	#phubet@phubet-Victus-by-HP-Gaming-Laptop-15-fa1xxx:~$ ros2 topic bw /data
	#Subscribed to [/data]
	#30 B/s from 2 messages
	#Message size mean: 16 B min: 16 B max: 16 B

ลอง publish ใน command ใช้ร่วมกับ ros2 topic echo [topic_name] ได้จะขึ้นเป็น msg ของอีกอันแล้วก็ของอันนี้

	ros2 topic pub -r 1 /data example_interfaces/msg/String "{data : 'Hello'}"

ดู node ที่ทำงานอยู่

	ros2 node list

ดู info ของ node นั้น

	ros2 node info /[node_name]

เปลี่ยนชื่อ node ที่จะ run เป็นการ overwrite ที่ runtime ไม่ได้เปลี่ยนที่ตัว code

	ros2 run my_package Pub_node --ros-args -r __node:=pub_node
 
เปลี่ยน topic name ด้วย
 
		ros2 run my_package Pub_node --ros-args -r __node:=pub_node -r [ชื่อเก่า]:=[ชื่อใหม่]
		
การ record data ใน topic นั้นๆ

	สร้าง directory นึงมา
	mkdir ...
	cd เข้าไปที่ dir นั้น
	ros2 bag record /[topic ที่สนใจ]
	ros2 bag record -o [ชื่อ folder ที่จะตั้ง] /number_count
	ดู info ของ folder ที่ record
		ros2 bag info [ชื่อ folder]
	เล่นข้อมูลที่ record 
		ros2 bag play [ชื่อไฟล์]# จะทำให้ topic น้นเกิดการส่งของ msg ในนั้นสามารถใช้ ros2 topic echo ดูได้
	record หลาย topic ได้
		ros2 bag record /[topic ที่สนใจ 1] /[topic ที่สนใจ 2]
	record ทุก topic # ซึ่งมันจะ record ทุก topic จริง ๆ
		ros2 bag record -a


