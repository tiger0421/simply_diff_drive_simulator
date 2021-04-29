# ORNE_NeoNavigation
Run navigation on a real robot or on simulator, ignition gazebo.

## Video
In this video, we use amcl, neonavigation, and octomap_mapping.
[![](https://img.youtube.com/vi/n9oqzNH6MQM/0.jpg)](https://www.youtube.com/watch?v=n9oqzNH6MQM)


## Usage
### Simulation + Navigation + Mapping

In the video above, we do the following.

terminal 1: ignition gazebo(background) + neonavigation
```Shell
roslaunch simply_diff_drive_simulator run_simulation.launch with_navigation:=true
```

terminal 2: octomap_mapping
```Shell
roslaunch simply_diff_drive_simulator octomapping.launch disable_stf:=true
```

### Simulation only

```Shell
roslaunch simply_diff_drive_simulator run_simulation.launch no_ign_gui:=false
```

After clicking ignitoin gazebo gui, you can do the following
+ W: forward
+ A: turn left
+ S: turn right
+ D: backward
+ R: stop


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
catkin_make -DCMAKE_BUILD_TYPE=Release
```
※ Build failed  
Change package version like below, when you failed buildig package, ros_ign.
```Shell
cd ~/sim_ws/src/ros_ign
git reset --hard 269ed5d81eff385bb6b9fa25531b58bbc4adc4bf
```
and build again.
</details>