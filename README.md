# Docker
Setup docker in Paperspace machine (Ubuntu 16.04)
cuda 8.0
cudann 5.1
tensorflow 1.0.0
keras 2.0.1

### Basics
* First, open a terminal and run the following commands to make sure your OS is up-to-date

        sudo apt-get update  
        sudo apt-get upgrade  
        sudo apt-get install build-essential cmake g++ gfortran git pkg-config python-dev software-properties-common wget
        sudo apt-get autoremove 
        sudo rm -rf /var/lib/apt/lists/*

### Nvidia Drivers
* Find your graphics card model

        lspci | grep -i nvidia
        
At the time of this writing, current official release is 387. 
Install the drivers 

	sudo add-apt-repository ppa:graphics-drivers/ppa
	sudo apt-get update
	sudo apt-get install nvidia-384

Restart machine
	
	sudo shutdown -r now
	
Check the nvidia driver version
	
	cat /proc/driver/nvidia/version
	
Install cuda toolkit
	
	cd downloads
	wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
	sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
 	sudo apt-get update
 	sudo apt-get install cuda-8-0
	
Ensure that correct version of cuda is installed (http://arnon.dk/check-cuda-installed/)
	
	nvcc -V
	
Install cudnn
	
	cd ~/downloads
	wget http://files.fast.ai/files/cudnn-8.0-linux-x64-v5.1.tgz
	mkdir cudnn8
	tar xvf cudnn-8.0-linux-x64-v5.1.tgz -C cudnn8
	cd cudnn8/cuda
	sudo cp */*.h /usr/local/cuda/include/
	sudo cp */libcudnn* /usr/local/cuda/lib64/
	sudo chmod a+r /usr/local/cuda/lib64/libcudnn*

Restart the machine

### Nvidia-Docker

Find latest NVIDIA Docker here [https://github.com/NVIDIA/nvidia-docker].
	
	cd ~/downloads
	wget -P https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
	sudo dpkg -i nvidia-docker*.deb

Restart Nvidia Driver and verify that docker is installed
	
	sudo systemctl restart nvidia-docker
	nvidia-docker run --rm nvidia/cuda nvidia-smi
	
### Image and Container

Build docker image with name 'fastai-keras' (replace if using any other name)
	
	sudo nvidia-docker build -t fastai-keras --rm -f ~/Docker_Tutorial/fastai-Dockerfiles/Dockerfile_keras ~/Docker_Tutorial/fastai-Dockerfiles/
	
Run a container using image created above.
	
	sudo bash run_container.sh fastai fastai-keras
	

### References

I have gone through multiple resources available on web to setup deep learning workspace using docker.Some of them are provided here.

-	https://github.com/anurag/fastai-course-1
-	https://github.com/hamelsmu/Docker_Tutorial
-	https://github.com/floydhub/dl-setup#nvidia-drivers
- 	https://medium.com/@vivek.yadav/deep-learning-setup-for-ubuntu-16-04-tensorflow-1-2-keras-opencv3-python3-cuda8-and-cudnn5-1-324438dd46f0




