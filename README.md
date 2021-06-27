# Build Cartographer

**Test environment:**

- Ubuntu16.04 LTS
- ROS-Kinetic

## Before Install

```sh
sudo apt-get update
sudo apt-get install -y python-wstool python-rosdep ninja-build
```

## Step1. GooleTest

```sh
cd googletest
cmake -L CMakeLists.txt && make -j
sudo make install
```

## Step2. Abseil-cpp

```sh
cd abseil-cpp
cmake -L CMakeLists.txt && make -j
sudo make install
```

## Step3. Cartographer

```sh
cd cartographer
catkin_make_isolated --install --use-ninja
```

## Step4. Test & Start up

```sh
wget -P ~/Downloads https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/b2-2016-04-05-14-44-52.bag
wget -P ~/Downloads https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/b2-2016-04-27-12-31-41.bag
source install_isolated/setup.bash
roslaunch cartographer_ros offline_backpack_2d.launch bag_filenames:=${HOME}/Downloads/b2-2016-04-05-14-44-52.bag
roslaunch cartographer_ros demo_backpack_2d_localization.launch \
   load_state_filename:=${HOME}/Downloads/b2-2016-04-05-14-44-52.bag.pbstream \
   bag_filename:=${HOME}/Downloads/b2-2016-04-27-12-31-41.bag
```

