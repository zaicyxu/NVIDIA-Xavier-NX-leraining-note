# Jetson frame wheel estublish

## For prebegining

- Update
- 

```python
sudo apt-get update
sudo apt-get upgrade
```

- Miniconda:
- Links: https://github.com/conda-forge/miniforge
- Enter the directory containing the miniforge installation package, right-click to open the terminal and enter the command to install：

```python
bash Miniforge3-Linux-aarch64.sh -b
```

- After the installation is complete, initialize conda as follows, and reopen the terminal after initialization.
- 

```python
# 编辑环境变量
vim ~/.bashrc
# 增加环境变量, 将<username>换成你的用户名
export PATH=/home/<username>/miniforge-pypy3/bin:$PATH
# 激活环境变量
source ~/.bashrc
# 显示(base)
source activate
```

```python
~/miniforge3/bin/conda init
```

## For Pytorch

- Links: [https://forums.developer.nvidia.com/t/pytorch-for-jetson-version-1-11-now-available/72048](https://forums.developer.nvidia.com/t/pytorch-for-jetson-version-1-11-now-available/72048)
- Create a virtual environment please don’t forget.(python=3.6)!!!

```python
pip3 install numpy torch-1.10.1-cp36-cp36m-linux_aarch64.whl# For your own edition
```

- Or for this way:
- 

```python
pip3 install -U future psutil dataclasses typing-extensions pyyaml tqdm seaborn
wget https://nvidia.box.com/shared/static/p57jwntv436lfrd78inwl7iml6p13fzh.whl -O torch-1.8.0-cp36-cp36m-linux_aarch64.whl 
sudo apt-get install python3-pip libopenblas-base libopenmpi-dev
pip3 install Cython -i 
pip3 install torch-1.8.0-cp36-cp36m-linux_aarch64.whl
```

- Install torchvision:
- If you don’t care cpu edition or gpu edition, just follw as below:

       1. From this links to download match edition: 

```python
git clone -b v0.7.0 https://hub.fastgit.org/pytorch/vision.git
cd vision
python3 setup.py install
```

- Tips: if there is a bug like this: Command ‘:/usr/local/cuda/bin/nvcc’   failed with exit status 1

       please solve it in this way:

```python
vim /.bashrc
```

```python
# Change:
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda
# To
export CUDA_HOME=/usr/local/cuda
```

```python
source /.bashrc
```

```python
rm -rf build
```

## For detectron2

- Under the virtual environment of Pytorch.
- Edition of detectron2==0.6 only match python≥3.7, and torch≥1.8.0.

```python
#Only for edition of 0.6
python3 -m pip install 'git+https://github.com/facebookresearch/detectron2.git'
# OR in this edition
python -m pip install detectron2==0.4 -f \
  https://dl.fbaipublicfiles.com/detectron2/wheels/cu102/torch1.8/index.html
```

- Or Download the edition which you want in this links: https://github.com/facebookresearch/detectron2/releases

      and then:

```python
python setup.py build develop
```

Jetson Zoo: [https://elinux.org/Jetson_Zoo#PyTorch_.28Caffe2.29](https://elinux.org/Jetson_Zoo#PyTorch_.28Caffe2.29)