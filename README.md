# Minecraft 1.20.2 on FreeBSD: Getting Started

## This repository uses LWJG from [#431](https://github.com/LWJGL/lwjgl3/issues/421#issuecomment-1793764434).

**Thanks their work!**

*with the build versions of [er2off](https://github.com/er2off)  used here*


You will now be able to run Minecraft 1.20.2 on FreeBSD.

And **Minecraft will be able to recognize multiple cpu cores!**(for me, only 1.20.2 now, you maybe want Check the link above)

## Setting up Prism Launcher

We will mostly be following the OpenBSD build instructions at [https://prismlauncher.org/wiki/development/build-instructions/#openbsd](https://prismlauncher.org/wiki/development/build-instructions/#openbsd).

0. Install Dependencies: `sudo pkg install qt5 qt6 cmake kf5-cmake-extra-modules openjdk8 openjdk17 lwjgl glfw git`
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

## Building LWJGL3 and configuring script

**For FreeBSD 13.2+ or other version:**

Before get started, you maybe want to check [this](https://github.com/LWJGL/lwjgl3/issues/421).

---

1. Download [lwjgl3.tar.gz](https://github.com/Spokzooy/minecraft-freebsd/blob/main/lwjgl3.tar.gz) and extract it somewhere.
2. Go to the folder you extracted, `make install clean`
3. If the build succeeds, you should be able to find the built files in the following path:

	`/usr/local/lib/lwjgl3`

	`/usr/local/share/java/classes/lwjgl3`

	This should be correct for FreeBSD 13.2,
	But if not, open `minecraft-runtime` in a text editor, modify it:

	`LWJGL_JLP_OVRD`

	`LWJGL_OVRD`

	`LWJGL_OGL_OVRD`

	`LWJGL_OAL_OVRD`

	`LWJGL_GLFW_OVRD`

	`LWJGL_STB_OVRD`

	`LWJGL_JEM_OVRD`

---

### Configuring Prism
1. Go to Settings (either Global or Instance), then go in the Java section.
2. Set Java Runtime/Tick and set Java Installation to the location of the minecraft-runtime script.
3. Click Test, if you did everything correctly, it should say that the Test succeeded.

## Sources
- [https://github.com/LWJGL/lwjgl3/issues/421](https://github.com/LWJGL/lwjgl3/issues/421)
- [https://forums.freebsd.org/threads/latest-minecraft-on-freebsd.78774/](https://forums.freebsd.org/threads/latest-minecraft-on-freebsd.78774/)
- [https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=253021#c4](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=253021)
