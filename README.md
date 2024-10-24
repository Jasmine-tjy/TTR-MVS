# TTR-MVS
TTR-MVS is an MVS method that adopts textureless targeted refinement algorithm.
## Dependencies :hammer:
The code has been tested on Ubuntu 22.04 with i9 14900K/RTX4090, and you can modify the CMakeList.txt to compile on Windows.

* [Cuda](https://developer.nvidia.cn/cuda-toolkit) >= 6.0
* [OpenCV](https://opencv.org/) >= 2.4
* [cmake](https://cmake.org/) >= 2.8
* [Boost](https://www.boost.org/) >= 1.62.0

Besides make sure that your GPU Compute Capability matches the CMakeList.txt! Otherwise you can only get the empty result without any warnings. For example, according to GPU Compute Capability, RTX 4090's Compute Capability is 8.9. So you should set the cuda compilation parameter 'arch=compute_89,code=sm_89' or add a '-gencode arch=compute_89,code=sm_89'.

Due to version matching issues among cuda, opencv, and cmake, the construction environment is quite complex. For this purpose, we have uploaded a __Docker image__ for the three part, which allows users to create an environment. The available image can be found in [cmake_cuda_opencv](https://hub.docker.com/r/tangjas111/cmake_cuda_opencv/tags)

__!__ The provided image is mainly for the code executing which is not for Python, you can prepare the dataset first by using personal python environment.
### Tips of using docker :whale2:
* Login in your docker account first
* Pull the docker image from docker hub
  ```
  docker pull tangjas111/cmake_cuda_opencv:latest
  ```
* Run docker container
  ```
  docker run -itd --name TTR-test --runtime=nvidia --gpus all tangjas111/cmake_cuda_opencv:latest
  ```
* Copy the source code and preprocessed dataset into the container
  ```
  docker cp <dataset> <container id>:<work directory>
  docker cp <source code> <container id>:<work directory>
  ```
## Usage :rocket:
### Complie TTR-MVS
```
cmake .    
make
```
### Testing dataset :open_file_folder:
* ETH3D dataset
  
Download train and test dataset (style as xxx_dslr_undistorted.7z) from [ETH3D](https://www.eth3d.net/datasets), and use the script colmap2mvsnet.py to convert the dataset format(you may refer to MVSNet).
```
python colmap2mvsnet.py --dense_folder <ETH3D data path, such as ./ETH3D/office> --save_folder <The path to save>
```
* Tanks & Temples
  
We use the version provided by MVSNet. The dataset can be downloaded from [here](https://drive.google.com/file/d/1YArOJaX9WVLJh4757uE8AEREYkgszrCo/view), and the format is exactly what we need.
### Run :arrow_left:
After the code and dataset preparation, the code can be run as follows:
```
./TTR <ETH3D root path>/dataset_kicker
```
It is very easy to use, and you can modify our code as you need.
