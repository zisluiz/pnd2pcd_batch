# png2pcd_batch

#### Simple command line utility to convert depth and rgb frames from PNG format to PCL pointcloud

There are 2 execution modes:

1. using file with association information i.e. containing rgb-depth PNG files correspondence
2. just providing folders that contain depth and rgb frames

In the 1st case you should anyhow [associate the files](https://vision.in.tum.de/data/datasets/rgbd-dataset/tools#associating_color_and_depth_images) by yourself (for further details check description of parse_freiburg function).
In the 2nd case - correspondence strictly depends on file names, and you should check it twice, to avoid situation when selected depth frame is not appropriate for rgb frame. (add sorting to filenames vector using custom predicate)

All dataset related parameters are incapsulated in Intr structure (intrinsics).
There are: width, height, fx, fy, cx, cy, scale_factor.
Usually depth data is saved from Kinect as unsigned short 16 bit, but in pcl::PointXYZ you have to re-scale it to float - metric measurment.

**Appropriate intrinsics should be written to file cam_params.cfg otherwise
default values will be used (which may lead to invalid output data).**

## Compiling

Install dependencies (this will take a while, especially for `vtk`, dependency of `pcl`):
```
brew tap homebrew/science
brew update
brew install pcl --without-apps
brew install opencv
```

CMake:
```
mkdir build; cd build
cmake ..
make
```
