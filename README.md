Gibbon's Duke Nukem 3D Port
==========================
Thanks to JFDuke / Jonathon Fowler, with contributions by Ken Silverman and others.

The goal of this source port is to make Duke3D as close to the original DOS as possible.

I will be doing the following:
* porting the menu code from the original source release as well as fixes from xDuke and the Icculus source port.
* reverse engineering the v1.5 executable so that the DOS release demos are compatible.  I won't be doing a compat layer but instead will support only v1.5 demos eventually.
* allow demos to playback on the menu screen just like the original.
* remove all modern features from the menu and video options (no hi-res, no GLES/GL rendering at all).  Software 8-bit only.
* netcode will be taken from xDuke.
* legacy resolutions and aspect ratio corrections

Minimum system requirements
---------------------------

* 32 or 64-bit CPU. These have been tried first-hand:
  * Intel x86, x86_64
  * ARM 32-bit hard-float, 64-bit
  * Apple M1 (ARMv8)
* A modern operating system:
  * Linux, BSD, possibly other systems supported by [SDL 2.0](http://libsdl.org/).
  * macOS 11.5+
  * Windows 10/11

You will require game data from an original release of Duke Nukem 3D

Compilation
-----------

Before you begin, clone this repository or unpack the source archive. If you cloned using
Git, be sure to initialise the submodules of this repository (i.e. `git submodule update --init`).

Now, based on your chosen OS and compiler:

### Linux and BSD

1. Install the compiler toolchain and SDL2 development packages, e.g.
   * Debian 9: `sudo apt-get install build-essential libsdl2-dev`
   * FreeBSD 11: `sudo pkg install gmake sdl2 pkgconf`
2. Install optional sound support development packages.
   * Debian 9: `sudo apt-get install libvorbis-dev libfluidsynth-dev`
   * FreeBSD 11: `sudo pkg install libvorbis fluidsynth`
3. Install GTK+ 3 development packages if you want launch windows and editor file choosers, e.g.
   * Debian 9: `sudo apt-get install libgtk-3-dev`
   * FreeBSD 11: `sudo pkg install gtk3`
4. Open a terminal, change into the source code directory, and compile the game with: `make` or `gmake` (BSD)
5. Assuming that was successful, run the game with: `./duke3d`

### macOS

1. [Install Xcode from the Mac App Store](https://itunes.apple.com/au/app/xcode/id497799835?mt=12).
2. Fetch and install the SDL 2.0 development package:
   1. Fetch _SDL2-2.0.x.dmg_ from http://libsdl.org/download-2.0.php.
   2. Copy _SDL2.framework_ found in the DMG file to `~/Library/Frameworks`. Create the
      _Frameworks_ directory if it doesn't exist on your system.
3. Open _duke3d.xcodeproj_ from within the Naked Duke's source code's _xcode_ folder.
4. From the Product menu choose Run.

### Windows using Microsoft Visual Studio 2022 and NMAKE

1. If needed, [install Visual Studio Community 2017 for free from
   Microsoft](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio).
   Terms and conditions apply. Install at minimum these components:
   * MSVC 2022 v141 toolset for desktop (x86,x64,arm)
   * Windows Universal CRT SDK
   * Windows 10 SDK
2. Open the command-line build prompt. e.g. _VS2022 x64 Native Tools Command Prompt_
   or _VS2022 x86 Native Tools Command Prompt_.
3. Change into the JFDuke3D source code folder, then compile the game with: `nmake /f Makefile.msvc`
5. Assuming success, run the game with: `nakedduke`

Compilation options
-------------------

Some engine features may be enabled or disabled at compile time. These can be passed
to the MAKE tool, or written to a Makefile.user (Makefile.msvcuser for MSVC) file in
the source directory.

These options are available:

 * `RELEASE=1` – build with optimisations for release.
 * `RELEASE=0` – build for debugging.
 * `USE_POLYMOST=1` – enable the true 3D renderer.
 * `USE_POLYMOST=0` – disable the true 3D renderer.
 * `USE_OPENGL=1` – enable use of OpenGL 2.0 acceleration.
 * `USE_OPENGL=USE_GL2` – enable use of OpenGL 2.0 acceleration. (GCC/clang syntax.)
 * `USE_OPENGL=USE_GLES2` – enable use of OpenGL ES 2.0 acceleration. (GCC/clang syntax.)
 * `USE_OPENGL=0` – disable use of OpenGL acceleration.
 * `WITHOUT_GTK=1` – disable use of GTK+ to provide launch windows and load/save file choosers.


Enjoy!

~Gibbon
