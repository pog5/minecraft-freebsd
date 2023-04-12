# minecraft-freebsd: Getting Started

## Setting up Prism Launcher

We will mostly be following the OpenBSD build instructions at [https://prismlauncher.org/wiki/development/build-instructions/#openbsd](https://prismlauncher.org/wiki/development/build-instructions/#openbsd).

0. Install Dependancies: `sudo pkg install qt5 qt6 cmake openjdk8 openjdk17 lwjgl glfw git`
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

## Setting up LWJGL3

*If you're planing to run <1.12 then you probably won't need this, but if running it does not work then follow this guide for it too.*

### Library Setup
1. Download [lwjgl-3.2.3.1-freebsd.tar](/lwjgl-3.2.3.1-freebsd.tar) and extract it somewhere. For this guide I'll extract it to `/opt/lwjgl3/`, there should be a folder called `bin` and a script called `minecraft-runtime` there.
2. Open `/opt/lwjgl3/minecraft-runtime` in a text editor, you will need to most probably modify 2 values near the top.
3. Set the `ROOT` variable in minecraft-runtime to the location where you extracted LWJGL3, in my case, it would be `ROOT=/opt/lwjgl3/`
4. `JAVA_HOME` should already be set correctly, but if its not, set it to `export JAVA_HOME=/usr/local/openjdk17`

### Configuring Prism
1. Go in Settings (either Global or Instance), then go in the Java section.
2. Set Java Runtime/Tick and set Java Installation to the location of the minecraft-runtime script, in my case, `/opt/lwjgl3/minecraft-runtime`
3. Click Test, if you did everything correctly, it should say that the Test succeeded.
