## FFmpeg Build Script

I write a script to simplify the build. The script is in QtAV/scripts/build_ffmpeg.sh. It supports mingw gcc, msvc(2013), android, maemo5, maemo6(meego), sailfish os etc. Just put the script in ffmpeg source tree and run

    ./build_ffmpeg.sh

To cross build for android, maemo etc, you have to set some vars, for example NDK_ROOT for android. The vars can be set in config-android.sh, config-maemo5.sh etc.

#### Install

    make install prefix=some_dir

ref: http://ffmpeg.org/platform.html#Microsoft-Visual-C_002b_002b-or-Intel-C_002b_002b-Compiler-for-Windows

## Build with VC

Open vs prompt, go to msys' bin dir and run

    sh --login -i

Then your are ready to use bash environment and with VC environment. Then go to ffmpeg source dir and run './build_ffmpeg.sh vc'

if get error about gawk, just ignore `make -ki`

## Additional Tools for Windows

Your msys may lack of some command line tools that ffmpeg build system needs, such as pr, od, install, pkg-config, nasm. You can download one of build-ffmpeg-win-additinal-tools_msys2/gnuwin32.7z here: https://sourceforge.net/projects/qtav/files/depends/

extract and append it's bin dir to PATH. then you can build ffmpeg with gcc or vc.

If you build with vc and not vs2013, you have to download [c99wrap](https://github.com/libav/c99-to-c89/)


## Use MinGW libraries in VC

If we build FFmpeg using mingw gcc, the `*,lib` are also created and installed in /usr/local/bin. So VC linker can use those. `*,lib` are generated by vc toolchain's `lib.exe` and `link.exe` if they are found. Otherwise `dlltool` is used. You may need additional link flag `/SAFESEH:NO` when linking to libs created by dlltool to avoid link error.

If gcc does not create `*.lib`, for example, portaudio, then you can do it yourself.

    dlltool -m i386 -d libportaudio-2.dll.def -l portaudio.lib -D libportaudio-2.dll

the def file can be found in lib/.lib for portaudio

## Build PortAudio

cmake is recommended. It's not difficult.


## Build QtAV

https://github.com/wang-bin/QtAV/wiki/Build-QtAV


[prebuilt FFmpeg+portuaido](https://sourceforge.net/projects/qtav/files/depends)