# minecraft-freebsd: Getting Started

## Setting up Prism Launcher

We will mostly be following the OpenBSD build instructions at [https://prismlauncher.org/wiki/development/build-instructions/#openbsd](https://prismlauncher.org/wiki/development/build-instructions/#openbsd).

0. Install Dependancies: `sudo pkg install qt5 qt6 cmake openjdk8 lwjgl git`
1. Clone the repo: `git clone --recursive https://github.com/PrismLauncher/PrismLauncher.git` and `cd PrismLauncher`
2. Configure environment: 
``
cmake -S . -B build
   -DCMAKE_BUILD_TYPE=Release
   -DCMAKE_INSTALL_PREFIX="/usr/local"
   -DCMAKE_PREFIX_PATH=/usr/local/lib/qt5/cmake
   -DENABLE_LTO=ON
``
3. Actually build Prism Launcher: `cd build` and `sudo make -j$(nproc) install`
