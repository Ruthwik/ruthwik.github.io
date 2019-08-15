---
layout: post
title: How to install TensorFlow 1.14 with GPU support on Ubuntu 18.04 LTS + CUDA 10.1
subtitle: TensorFlow with GPU for deeplearning
published: true
categories: machinelearning
tags: [GPU, TensorFlow]

bigimg:
  - /img/tensorflownutshell/tensorflowimage.jpg

---


<p>
The first thing I did after I bought a laptop with NVIDIA GPU was to install TensorFlow. I skimmed through many blogs and pages on how to install and I found this page by Christian Janze. He did a great job of putting everything together in one place. I'm creating this page on similar lines but adding few of my own touches and experiences while installing TensorFlow.

<h3>Level 0</h3>
<p>
All the Prerequisites required before starting the installation.

<ul>
<li> <strong><em>Install GNU Compiler Collection (GCC)</em></strong>


  ```
    sudo apt update && sudo apt install gcc

  ```

  <img src="/img/install_tensorflow_gpu/gcc.jpg" alt="docker_core" height="85%" width="100%">
  </li>

  <li> <strong><em>Install build-essential package</em></strong>

  ```
    sudo apt update && sudo apt install build-essential

  ```

  <img src="/img/install_tensorflow_gpu/essential.jpg" alt="docker_core" height="85%" width="100%">
  </li>

  <li> <strong><em>Install OpenGL Utility Toolkit (FreeGlut) and X11 Input extension library</em></strong>

  ```
  sudo apt update && sudo apt install freeglut3 freeglut3-dev libxi-dev libxmu-dev

  ```

  </li>

</ul>

</p>

<h3>Level 1 : Installing NVIDIA’s Linux Display Driver</h3>


<p>
The driver can be either downloaded from [here.](https://www.nvidia.com/Download/index.aspx?lang=en-us)
I used the following commands to install as it easy and simple.

```
  sudo apt update

  sudo ubuntu-drivers autoinstall

```

If everything goes well after firing these commands, then reboot your machine. The status of Nvidia GPU can be checked with the <code>nvidia-smi</code>.

<img src="/img/install_tensorflow_gpu/nvidia_smi.jpg" alt="docker_core" height="85%" width="100%">

</p>



<h3>Level 2: Installing CUDA Toolkit 10 via Runfile</h3>



> CUDA is a parallel computing platform and application programming interface (API) model created by Nvidia. The NVIDIA® CUDA® Toolkit provides a development environment for creating high-performance GPU-accelerated applications. With the CUDA Toolkit, you can develop, optimize and deploy your applications on GPU-accelerated embedded systems, desktop workstations, enterprise data centers, cloud-based platforms and HPC supercomputers. The toolkit includes GPU-accelerated libraries, debugging and optimization tools, a C/C++ compiler and a runtime library to deploy your application.



<p>
I installed using runfile as I need to set the PATH after installation. I need to install it at the path of my choice. I faced few problems here as I need to disable nividia driver before installing cuda. But I articulated all the steps here so that there won't be any problems.


</p>



<h4>1. Download the NVIDIA® CUDA® Toolkit from [here](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal)</h4>
<p>
<img src="/img/install_tensorflow_gpu/cuda_toolkit.jpg" alt="docker_core" height="85%" width="100%">

</p>

<h4>2. Switch to tty3 by pressing Ctl+Alt+F3</h4>
<p>
</p>

<h4>3. Unload nvidia-drm before proceeding</h4>
<p>
<ul>
<li> <strong><em>Isolate multi-user.target</em></strong>

  ```
  sudo systemctl isolate multi-user.target

  ```
  </li>

  <li> <strong><em>Check for nvidia-drm in use</em></strong>

  ```
  lsmod | grep nvidia.drm

  ```

  </li>

  <li> <strong><em>Unload nvidia-drm</em></strong>

  ```
  sudo modprobe -r nvidia-drm

  ```

  </li>

  <li> <strong><em>Note that nvidia-drm is not in use anymore</em></strong>

  ```
    lsmod | grep nvidia.drm

  ```

  </li>

  <li> <strong><em>Go to your download folder and run the cuda installation.</em></strong>

  ```
  sudo sh cuda_10.1.168_418.67_linux.run

  ```

  </li>

  <li> <strong><em>Start the GUI again.</em></strong>

  ```
  sudo systemctl start graphical.target

  ```

  </li>

</ul>
</p>
<h4>Setup the environment variables</h4>
<p>

Add the path in .bashrc file:

```
  sudo nano ~/.bashrc

  export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}

  export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

  source ~/.bashrc

```
</p>

<h4>Verify the installation of NVIDIA’s CUDA Toolkit 10 compiler driver</h4>
<p>


  ```

  nvcc -V

  ```
<img src="/img/install_tensorflow_gpu/nvcc.jpg" alt="docker_core" height="85%" width="100%">
</p>

<h3>Level 3: Installing cuDNN</h3>
<p>
Please head over to the NVIDIA cuDNN website and click on the green Download cuDNN button. Unfortunately, you have to register for the NVIDIA Developer Program. Once you are registered, go to the NVIDIA cuDNN website and fill in the survey to reach the download page.

<img src="/img/install_tensorflow_gpu/cuDNN_download.jpg" alt="docker_core" height="85%" width="100%">


```

  sudo dpkg -i libcudnn7_7.6.2.24-1+cuda10.1_amd64.deb

  sudo dpkg -i libcudnn7-dev_7.6.2.24-1+cuda10.1_amd64.deb

  sudo dpkg -i libcudnn7-doc_7.6.2.24-1+cuda10.1_amd64.deb

```
<img src="/img/install_tensorflow_gpu/cuDNN.jpg" alt="docker_core" height="85%" width="100%">

</p>

<h4>Verify the installation of NVIDIA’s CUDA Toolkit 10 compiler driver</h4>
<p>

```

  cp -r /usr/src/cudnn_samples_v7/ $HOME

  cd $HOME/cudnn_samples_v7/mnistCUDNN

  make clean && make

  ./mnistCUDNN

```

<img src="/img/install_tensorflow_gpu/cudaa_test.jpg" alt="docker_core" height="85%" width="100%">

</p>

<h3>Installing TensorFlow 1.14</h3>

<p>
This can be done in two ways one by using pip and another by using conda if you want to use anaconda.

```

  sudo apt install virtualenv

  virtualenv --system-site-packages -p python3 ./venv

  source ./venv/bin/activate

  pip install --upgrade pip

  pip list

  pip install tensorflow-gpu

```
</p>

<h4>Verify TensorFlow installation</h4>
<p>

```
  python -c "from tensorflow.python.client import device_lib; print(device_lib.list_local_devices())"

```


</p>
<p>If you have any question or feedback, please do reach out to me by commenting below.</p>
