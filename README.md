# Flownet2 With Nvidia Docker
this ReadMe explains the working process of how to set the enviornment for use of flownet2 with nvidia_docker

# Launch your instance with dl_ami AWS launch template and Connect to it 
> ssh -i "XXXX.pem" ubuntu@ecX-XX-XXX-XX-XX.us-east-2.compute.amazonaws.com

# Execute the Following commands in order
>curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
>sudo apt-key fingerprint 0EBFCD88
>sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
>sudo apt-get update
>sudo apt-get install docker-ce
>sudo service docker restart
>docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
>sudo apt-get purge -y nvidia-docker

# Add the package repositories
>curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
>  sudo apt-key add -
>distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
>curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
>  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
>sudo apt-get update

# Install nvidia-docker2 and reload the Docker daemon configuration
>sudo apt-get install -y nvidia-docker2
>sudo pkill -SIGHUP dockerd

# Test nvidia-smi with the latest official CUDA image
>docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi
