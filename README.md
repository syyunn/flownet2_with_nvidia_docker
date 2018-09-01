# Flownet2 With Nvidia Docker
this ReadMe explains the working process of how to set the enviornment for use of flownet2 with nvidia_docker

# Launch your instance with dl_ami AWS launch template and Connect to it 
> ssh -i "XXXX.pem" ubuntu@ecX-XX-XXX-XX-XX.us-east-2.compute.amazonaws.com

# Execute the Following commands in order

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo apt-key fingerprint 0EBFCD88
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt-get update
    sudo apt-get install docker-ce
    sudo service docker restart

Then, proceed to adding the required repositories and installing the needed software:

Start with `nvidia-docker-runtime`:

**For Ubuntu distributions (Xenial x86_64):**

First, if you have older nvidia-docker installations, purge the installation and all associated GPU containers:

    docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
    sudo apt-get purge -y nvidia-docker

Then proceed:

    curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
      sudo apt-key add -
    curl -s -L https://nvidia.github.io/nvidia-container-runtime/ubuntu16.04/amd64/nvidia-container-runtime.list | \
      sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
    sudo apt-get update
    
    # Install nvidia-docker2 and reload the Docker daemon configuration
