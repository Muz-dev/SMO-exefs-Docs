# Setting Up Our First Mod

To write our first exefs mod we need a base. A base is a c++ project that has been configured to compile into a binary file to mod the main executable. The base that we are going to use for this is smo-exlaunch-base-clang. For people that are on windows or linux we can use the base repo linked here [smo-exlaunch-base-clang](https://github.com/lynxdev2/smo-exlaunch-base-clang). However if you are on mac then you need to use a old version of the repo modified to work with MacOS linked here [smo-exlaunch-base-clang](https://github.com/muz-dev/smo-exlaunch-base-clang). Make sure to clone the repo recursivly with --recursive after the url!

As you should be able to see in the repo there are two tools required to use this base. CMake and Ninja. The rest are downloaded for you. You can download cmake and Ninja on windows with winget, port (macports) on MacOS and your distros package manager on linux.

Now to test that you can compile your code open a terminal in the directory that you cloned smo-exlaunch-base-clang into. Now type "cmake -S . -B build -G Ninja --toolchain=cmake/toolchain.cmake" if you did everything before correctly it should start to download the required tools for the base. Once thats done you can run "ninja -C build" and it will be compiled.

# Setting up ghidra

When we code our mods we need to symbol to hook onto, this will be explained for later on. We can find these symbol's in ghidra, a decompiler.

First download it from here [Ghidra](https://github.com/NationalSecurityAgency/ghidra/releases). Next download the ghidra switch loader from here [Ghidra Switch Loader](https://github.com/Abuddz/Ghidra-Switch-Loader/releases). Now that you have downloaded ghidra extract it and run it. Once ghidra has launched press file then install extensions then the plus icon in the top corner, Now select the ghidra switch loader zip file and press install.

Now we need to extract the exefs from the rom for ghidra. The easiest way to do this is to dump your 1.0.0 rom from your switch using nxdumptool. Download nxdump tool from the homebrew app store or github (if you choose github then make sure to copy it to the switch folder!) Now open the homebrew launcher and launch nxdumptool, then select user titles menu -> 01000...10000 -> nca dump options -> look through the options untill you see exefs (You will see the name when you are selected on it) -> start nca dump.

Once thats done connect your switch to your pc and go to the sd card then open the nxdt_rw_proc/nca/01000...10000/ then copy the exefs folder to somewhere on your pc that you will be able to find. 

