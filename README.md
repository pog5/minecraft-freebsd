# Minecraft 1.20.2+ on FreeBSD: Getting Started

### This repository uses LWJG from [#431](https://github.com/LWJGL/lwjgl3/issues/421#issuecomment-1793764434).

## If you are affected by https://github.com/pog5/minecraft-freebsd/issues/8, use [this version of the repo](https://github.com/pog5/minecraft-freebsd/tree/b7bc8cbdd43864a2cabd4021e87f9f7e8c6d3838) instead of the normal one!

**Thanks to their work!**

*with the build versions of [er2off](https://github.com/er2off)  used here*

You will now be able to run Minecraft 1.20.2+ on FreeBSD.

And **Minecraft will be able to recognize multiple cpu cores!**(for me, only 1.20.2 now, you maybe want Check the link above)

## Setting up Prism Launcher

We will mostly be following the OpenBSD build instructions at [https://prismlauncher.org/wiki/development/build-instructions/#openbsd](https://prismlauncher.org/wiki/development/build-instructions/#openbsd).

0. Install Dependencies: `sudo pkg install qt5 qt6 cmake kf5-extra-cmake-modules openjdk8 openjdk17 lwjgl glfw git`
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

<details>
	<summary>Try installing `games/lwjgl3` from ports first, if that doesn't work, follow this: </summary>
	
Before we get started, you might want to check [this](https://github.com/LWJGL/lwjgl3/issues/421).

---

1. Download [lwjgl3.tar.gz](lwjgl3.tar.gz) and extract it somewhere.
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
2. Set Java Runtime/Tick and set Java Installation to the location of the minecraft-runtime script from the `make install` step above this one.
3. Click Test, if you did everything correctly, it should say that the Test succeeded.

</details>

<details>
	<summary>Alternative Solution:</summary>
<quote>Qutoed from https://github.com/pog5/minecraft-freebsd/issues/8?notification_referrer_id=NT_kwDOA7VwZLM4NzA5Njk5ODcyOjYyMjIyNDM2#issuecomment-2031646216:</quote>

 
 @Gamer100Dev's solution worked for me. 

Yes, I'm on FreeBSD 14.0 RELEASE

To be clearer, git clone https://github.com/LWGJL/lwjgl3.

- Download https://github.com/pog5/minecraft-freebsd/blob/main/lwjgl3.tar.gz

- Extract the tar.gz file

- Copy the "Makefile" from the extracted tar.gz file into where you cloned lwjgl3; overwriting the original

- Run this command inside of the lwjgl3 dir that you cloned:

`/usr/local/bin/cmake -E env JAVACMD=/usr/local/openjdk17/bin/java JAVA8_HOME=/usr/local/openjdk8 ant all && /usr/local/bin/cmake -E env JAVACMD=/usr/local/openjdk17/bin/java JAVA8_HOME=/usr/local/openjdk8 ant release -Dbuild.offline=yes -Djavadoc.skip=yes`

- Run: `# mkdir /usr/local/share/java/classes/lwjgl3 /usr/local/lib/lwjgl3`

- Run: `# find /PATH/TO/GIT/lwjgl3 -name "*.so" -exec cp {} /usr/local/lib/lwjgl3/ \;`

- Run: `find /PATH/TO/GIT/lwjgl3 -name "*.jar" -exec cp {} /usr/local/share/java/classes/lwjgl3/ \;`

- Install minecraft-client & openjdk17-jre:
`# pkg install minecraft-client openjdk17-jre`

- Overwrite the original minecraft-runtime file with the one from the extracted tar: 
`# cp /PATH/TO/EXTRACTED/TAR/lwjgl3/minecraft-runtime /usr/loca/share/minecraft-client/minecraft-runtime`

- In PrismLauncher, go to `Settings` > `Java` and set "Java Path" to:
`/usr/local/share/minecraft-client/minecraft-runtime`
</details>

## IMPORTANT: FOR PEOPLE RUNNING SNAPSHOTS OF 1.13 AND LOWER:
You need to add `-Dorg.lwjgl.librarypath=/usr/local/lib/lwjgl` as a additional flag (Thanks to @er2off on Discord for this info.)

## Sources
- [https://github.com/LWJGL/lwjgl3/issues/421](https://github.com/LWJGL/lwjgl3/issues/421)
- [https://forums.freebsd.org/threads/latest-minecraft-on-freebsd.78774/](https://forums.freebsd.org/threads/latest-minecraft-on-freebsd.78774/)
- [https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=253021#c4](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=253021)
