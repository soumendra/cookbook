# Setting up your environment

## Setting up your environment

* `conda` doesn't work well for production systems with CI/CD. It tries to do both python version management and project dependancy management, and doesn't do either of them very well. It does provide faster compiled versions on numpy, so there is that.
* Consider `poetry` and `venv` for non-docker-based workflow \(we cover docker-based workflow here\)

### Setting up Tensorflow 2 with Docker on Ubuntu

```bash
# Remove previously installed versions
sudo apt-get remove docker docker-engine docker.io containerd runc

# Install packages to allow apt to use a repository over HTTPS:
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

# Add Docker’s official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add repo
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# Install docker ce
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Add your-username to `docker` group to run commands as non-root
# Note: You'll need to restart your computer for this to take effect
sudo usermod -aG docker your-username

# Configure Docker to start on boot
sudo systemctl enable docker
```

#### Testing docker install

```text
docker run hello-world
```

#### Removing docker \(eventually\)

```bash
sudo apt-get purge docker-ce
sudo rm -rf /var/lib/docker
```

### Set up nvidia docker support in Linux \(`nvidia-container-toolkit`\)

[Official instructions can be found here](https://github.com/NVIDIA/nvidia-docker).

#### Ubuntu 19.04

We set `distribution` to 18.04 manually.

```bash
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/ubuntu18.04/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update
sudo apt-get install nvidia-container-toolkit
sudo systemctl restart docker
```

### Install Tensorflow

```bash
 docker pull tensorflow/tensorflow                  # Download latest image
 docker run -it -p 8888:8888 tensorflow/tensorflow  # Start a Jupyter notebook server
```

#### Testing Tensorflow install \(cpu\)

```bash
docker run -it --rm tensorflow/tensorflow \
    python -c "import tensorflow as tf; print(tf.__version__)"
```

### Tensorflow with GPU support

Test if a GPU is available:

```bash
lspci | grep -i nvidia

> 01:00.0 VGA compatible controller: NVIDIA Corporation GP104M [GeForce GTX 1070 Mobile] (rev a1)
> 01:00.1 Audio device: NVIDIA Corporation GP104 High Definition Audio Controller (rev a1)
```

```bash
# docker run --gpus all --rm nvidia/cuda nvidia-smi
docker run --gpus all -it --rm tensorflow/tensorflow:latest-gpu \
   python -c "import tensorflow as tf; print(tf.__version__)"
```

## Reference

1. [docker installation](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
2. [nvidia docker support installation](https://github.com/NVIDIA/nvidia-docker)
3. [nvidia docker support for Ubuntu 19.04](https://www.pugetsystems.com/labs/hpc/Workstation-Setup-for-Docker-with-the-New-NVIDIA-Container-Toolkit-nvidia-docker2-is-deprecated-1568/)
4. [Install Tensorflow](https://www.tensorflow.org/install)

