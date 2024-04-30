## Installation Steps

This guide assumes that you are using Ubuntu 22.04.

### Install Dependencies

```
sudo apt install git cmake build-essential libboost-dev libssl-dev libboost-serialization-dev libboost-python-dev libeigen3-dev libgl1-mesa-dev libglew-dev libgtk-3-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev openexr libatlas-base-dev libopenexr-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev python3-dev python3-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-dev gfortran
```

### Install OpenCV4

```
mkdir ~/opencv_build && cd ~/opencv_build
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
mkdir -p ~/opencv_build/opencv/build && cd ~/opencv_build/opencv/build
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_GENERATE_PKGCONFIG=ON -D BUILD_EXAMPLES=ON -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules ..
make -j6
sudo make install
```

### Build Pangolin

```
cd ~
git clone --recursive https://github.com/stevenlovegrove/Pangolin.git
cd Pangolin/
sudo ./scripts/install_prerequisites.sh recommended
cmake -B build
cmake --build build
cd build
sudo make install
```

### Build and Install ORB_SLAM3

```
cd ~
git clone https://github.com/hello-atharva/ORB_SLAM3.git
cd ORB_SLAM3/
./build.sh
cd build
sudo make install
cd ../Thirdparty/Sophus/build
sudo make install
```

### Build and Install Python bindings

```
cd ~
git clone https://github.com/hello-atharva/ORB_SLAM3-PythonBindings.git
mkdir build
cd build
cmake ..
make -j4
sudo make install
```

### Update LD_LIBRARY_PATH

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
```

### Test with your Arducam

```
cd ~
git clone git@github.com:hello-atharva/stretch_py_benchmark_tools.git -b orbslam3
cd stretch_py_benchmark_tools
python3 slam.py /home/hello-robot/ORB_SLAM3/Vocabulary/ORBvoc.txt config/arducam.yaml 6
```

Pan the head to detect features and initialize a reference frame.
