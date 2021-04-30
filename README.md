# ORNE_NeoNavigation
Run navigation on a real robot or on simulator, ignition gazebo.

## Video
In this video, we use amcl, neonavigation, and octomap_mapping.
[![](https://img.youtube.com/vi/n9oqzNH6MQM/0.jpg)](https://www.youtube.com/watch?v=n9oqzNH6MQM)


## Usage for simulation
### Simulation only

```Shell
roslaunch orne_neonavigation run_simulation.launch 
```

### Simulation only (use GUI)
You can extreamly save your CPU power NOT to show ignition GUI.

So, option, `no_ign_gui`, is `true` by default.

However, you can use GUI with `no_ign_gui:=false`.

```Shell
roslaunch orne_neonavigation run_simulation.launch no_ign_gui:=false
```

<details>
<summary>How to operate the robot ?</summary>
You can operate the robot with your keybord.
After clicking ignitoin gazebo gui, you can do the following
+ W: forward
+ A: turn left
+ S: turn right
+ D: backward
+ R: stop
</details>

---

### Simulation + Navigation

#### 2D AMCL (default) with GUI

```Shell
roslaunch orne_neonavigation run_simulation.launch no_ing_gui:=false with_navigation:=true
```

#### 3D AMCL without GUI

```Shell
roslaunch orne_neonavigation run_simulation.launch with_navigation:=true use_mcl_3dl:=true
```

---

### Simulation + Navigation + Mapping

In the video above, we do the following.

terminal 1: ignition gazebo(background) + neonavigation
```Shell
roslaunch orne_neonavigation run_simulation.launch with_navigation:=true
```

terminal 2: octomap_mapping
```Shell
roslaunch orne_neonavigation octomapping.launch disable_stf:=true
```

---

## Usage for running real robot
This is only valid for i-Cart.
<details>
<summary>runnning navigation</summary>

2D AMCL

```Shell
roslaunch orne_neonavigation run_navigation.launch
```

3D AMCL

```Shell
roslaunch orne_neonavigation run_navigation.launch use_mcl_3dl:=true
```

Option list related to real robot
```Shell
icart_controller_port:=/dev/sensors/icart-mini
joystick_port:=/dev/input/js0
use_2d_urg:=false
2d_urg_port:=/dev/sensors/hokuyo_H0803606
2d_urg_ang_min:=-1.047
2d_urg_ang_max:=1.047
```

</details>

---

### Other options list
You can use these option for navigation on simulator and on real robot respectively. 

<details>
<summary>use_path_with_velocity</summary>

```Shell
roslaunch orne_neonavigation run_simulation.launch no_ign_gui:=false with_navigation:=true use_path_with_velocity:=true
```

</details>

<details>
<summary>use_safety_limiter</summary>

```Shell
roslaunch orne_neonavigation run_navigation.launch use_safety_limiter:=true
```

</details>

<details>
<summary>map_file</summary>

```Shell
roslaunch orne_neonavigation run_simulation.launch with_navigation:=true map_file:=/FULL/PATH/TO/MAP.yaml
```

</details>

<details>
<summary>map_pcd</summary>

```Shell
roslaunch orne_neonavigation run_simulation.launch with_navigation:=true use_mcl_3dl:=true map_pcd:=/FULL/PATH/TO/MAP.pcd
```

</details>

<details>
<summary>robot speed settings</summary>

```Shell
roslaunch orne_neonavigation run_navigation.launch vel:=0.8 acc:=0.25 ang_vel:=1.0 ang_acc:=0.25
```

</details>

---

## Install
<details>
<summary>Build on host</summary>
The following environment is recommended.

+ Ubnuntu 18.04
+ ROS melodic
+ Ignition gazebo citadel

```Shell
mkdir -p ~/sim_ws/src
curl https://raw.githubusercontent.com/tiger0421/orne_neonavigation/melodic/docker/melodic/preinstall.repos.yaml > preinstall.repos.yaml
vcs import ~/sim_ws/src < preinstall.repos.yaml
cd ~/sim_ws
sudo rosdep init
rosdep update
rosdep install --from-paths src -i -r -y
catkin_make_isolated -DCMAKE_BUILD_TYPE=Release
```
※ Build failed  
Change package version like below, when you failed buildig package, ros_ign.
```Shell
cd ~/sim_ws/src/ros_ign
git reset --hard 269ed5d81eff385bb6b9fa25531b58bbc4adc4bf
```
and build again.
</details>

<details>
<summary>Use docker</summary>

```Shell
git clone -b melodic https://github.com/tiger0421/orne_neonavigation.git
cd orne_neonavigation/docker
sh scripts/generate_docker_xauth.sh

# non-GPU
cd melodic/intel
docker-compose up -d

# GPU
cd melodic/nvidia
docker-compose up -d

# You can run commands inside this container
docker exec -it ros-console /bin/bash
```

</details>