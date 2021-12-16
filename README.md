**Taichi** is an open-source computer graphics library that aims to provide easy-to-use infrastructures for computer graphics R&D. It's written in C++14 and wrapped friendly with Python.

This is a **fork** of **Taichi legacy** to use [Taichi-MPM](https://github.com/yuanming-hu/taichi_mpm) with some modifications.

To install Taichi and Taichi-MPM follow these instructions (Tested on Ubuntu 20.04 with an Intel Skylake).

1. Clone the repository

```bash
git clone https://github.com/dblanm/taichi.git
```

2. Go into the repository, clone the external dependencies and start the submodules
```bash
cd taichi
git clone https://github.com/yuanming-hu/taichi_runtime external/lib -b linux --depth 1
git submodule update --init --recursive
```

3. Install all the required libraries
```bash
sudo apt-get update
sudo apt-get install python3-dev git build-essential cmake make g++ libx11-dev
sudo apt-get install libtinfo-dev clang-7 libc++-dev
pip install --user psutil
pip install --user colorama numpy Pillow flask scipy pybind11 flask_cors GitPython yapf distro requests PyQt5
```

4. Create the build directory and the build directives
```bash
mkdir build && cd build
cmake .. -DCMAKE_CXX_COMPILER=/usr/bin/clang++-7
```

For new CPU architectures **the architecture might not be found**.
In that case modify the compiler directive to your architecture (the available architectures can be found in the file taichi/cmake/OptimizeForArchitecture.cmake).
You can replace *skylake* with your CPU architecture.
```bash
cmake .. -DCMAKE_CXX_COMPILER=/usr/bin/clang++-7 -DTARGET_ARCHITECTURE=skylake
```

To find your architecture in linux you can use the command:
```bash
gcc -march=native -Q --help=target|grep march
```

5. Now build the library
```bash
make -j5
```

6. Finally add the environment variables to your `.bashrc` file:
```bash
export TAICHI_NUM_THREADS=8
export TAICHI_REPO_DIR=/your/path/to/taichi
export PYTHONPATH=$TAICHI_REPO_DIR/python/:$PYTHONPATH
export PATH=$TAICHI_REPO_DIR/bin/:$PATH
```
where you should set TAICHI_REPO_DIR to your own directory.



And that's it, you are ready to go!


