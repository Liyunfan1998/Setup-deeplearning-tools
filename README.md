[![](https://img.shields.io/badge/Lauguage-English-blue)](./) [![](https://img.shields.io/badge/CUDA%20version-v10.0-lightgrey)](https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=deblocal) [![](https://img.shields.io/badge/cuDNN-v7.6.5-red)](https://developer.nvidia.com/rdp/cudnn-download)

# Install / Remove CUDA and cudnn part.

## Remove
```
sudo apt-get remove cuda-10.1 
sudo apt autoremove
```

After the steps above, go to `/etc/apt/sources.list.d` and remove those files which are relevant with the words of CUDA.

```
sudo rm cuda.list 
```

## Install CUDA
1. First, download the .deb file from here. 
	https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=deblocal
2. sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
3. sudo apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub 
4. sudo apt-get update
5. sudo apt-get install cuda![meta-package](./assets/cuda.png)
6. sudo apt-get install cuda-libraries-dev-10-0 
> Other installation options are available in the form of meta-packages. For example, to install all the library packages, replace "cuda" with the "cuda-libraries-10-0" meta package. For more information on all the available meta packages click [here](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#package-manager-metas).
7. sudo apt-get install cuda-libraries-10-0 
8. sudo apt-get install cuda-runtime-10-0
9. sudo apt-get install cuda-toolkit-10-0
10. sudo apt-get install cuda-10-0

**Please don't forget to add the path of CUDA in .zshrc or .bashrc.**

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.0/lib64
export CUDA_INSTALL_DIR=/usr/local/cuda-10.0
export PATH=$PATH:/usr/local/cuda-10.0/bin
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-10.0
export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

## Install cudnn
Download from : https://developer.nvidia.com/rdp/cudnn-download
(Recommend to download the .tar file.)

Copy these files to the folder of `/cuda/include/` and `/cuda/lib64/`

```
> sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
> sudo cp cuda/lib64/lib* /usr/local/cuda/lib64/
```
Go to the folder of `/usr/local/cuda/lib64/` 
```
cd /usr/local/cuda/lib64/
```
Build the symbolic link (You need to use your version number instead of 7.6.5 if your version is different with mine.)
```
sudo chmod +r libcudnn.so.7.6.5
sudo ln -sf libcudnn.so.7.3.1 libcudnn.so.7
sudo ln -sf libcudnn.so.7 libcudnn.so
sudo ldconfig
```

# Check it

```
nvidia-smi
```

```
nvcc -V
```