Setting Up Our First Mod
===============================

If you ever get stuck following the guide join the smo modding hub on discord. And ask for help.


To write our first exefs mod we need a base. A base is a c++ project that has been configured to compile into a binary file to mod the main executable. The base that we are going to use for this is smo-exlaunch-base-clang. For people that are on windows or linux we can use the base repo linked here https://github.com/lynxdev2/smo-exlaunch-base-clang. However if you are on mac then you need to use a old version of the repo modified to work with MacOS linked here https://github.com/muz-dev/smo-exlaunch-base-clang. Make sure to clone the repo recursivly with --recursive after the url!

As you should be able to see in the repo there are two tools required to use this base. CMake and Ninja. The rest are downloaded for you. You can download cmake and Ninja on windows with winget, port (macports) on MacOS and your distros package manager on linux. 

Now to test that you can compile your code open a terminal in the directory that you cloned smo-exlaunch-base-clang into. Now type "cmake -S . -B build -G Ninja --toolchain=cmake/toolchain.cmake" if you did everything before correctly it should start to download the required tools for the base. Once thats done you can run "ninja -C build" and it will be compiled. 




Setting up ghidra
===================

When we code our mods we need to symbol to hook onto, this will be explained for later on. We can find these symbol's in ghidra, a decompiler. First download it from here https://github.com/NationalSecurityAgency/ghidra/releases. Next download the ghidra switch loader from here https://github.com/Adubbz/Ghidra-Switch-Loader/releases/tag/1.7.0. Now that you have downloaded ghidra extract it and run it. Once ghidra has launched press file then install extensions then the plus icon in the top corner, Now select the ghidra switch loader zip file and press install. Now we need to extract the exefs from the rom for ghidra. The easiest way to do this is to dump your 1.0.0 rom from your switch using nxdumptool. Download nxdump tool from the homebrew app store or github (if you choose github then make sure to copy it to the switch folder!) Now open the homebrew launcher and launch nxdumptool, then select user titles menu -> 01000...10000 -> nsp dump options -> dump base application -> start nsp dump. Once thats done connect your switch to your pc and copy the nx_... folder, then nsp, then copy the Super Mario Odyssey folder to somewhere on your pc that you will be able to find. Now download file joiner from https://www.igorware.com/file-joiner and extract it and run it, if you on MacOS or linux then use wine. Now select add a folder and select the Super Mario Odyssey folder. Then join. In the Super Mario Odyssey folder there will now be a new file in there. It should be around 5.2 Gb rename that file to "Super Mario Odyssey.nsp". Now go back to your switch sd card on your pc and download lockpick_rcm.bin and copy it to the bootloader/payloads folder on your switch. Now eject your switch sd card and (if your not already) reboot to hekate and select the payloads tab then lockpick_rcm.bin. Once in the menu use the power button to select "Dump from sysnand". Once you've done that use the volume buttons to navigate to reboot to hekate and then connect your sd card to your pc (or do whatever you do to connect your switch to your pc). Go into the switch folder and copy the prod.keys to somehwere on your pc. Now, Launch download and launch ryujinx. At the top of the screen click file then open ryujinx folder. Now copy prod.keys to the system folder found when opening the ryujinx folder. Now exit back into ryujinx and select options -> settings. Now press add and select the folder with the Super Mario Odyssey.nsp file. Then press ok. Now open your file explorer and create a new folder called exefs. Now go back to ryujinx and right click Super Mario Odyssey (If it doesnt show up then press the reload button in the bottom left corner) and press extract data -> ExeFs then select the exefs folder that you created before. Then it will say extracting data and the exefs will have been extracted to a folder, It should only take a moment. Now that's done you can close out of ryujinx, we are ready to start using ghidra and coding the mod  




Actually creating the mod
===============================

Now its time to do some coding! Lets write our first mod for Super Mario Odyssey!
First open up the base that we downloaded in your ide of choice. Then navigate to to the main.cpp file found in the user/src folder. In the main.cpp file you will see alot of code already, This is for the logging feature, dont remove it. Now lets open ghidra and start the hard part, Looking for the function or synbol to hook onto. In ghidra press file and new project, You can name it whatever you want. Once you have created a new project press file again then import file, Navigate to the exefs folder we created before and select main. When you select it ghidra will automatically detect that it is a nintendo switch binary if you installed the switch loader correctly. Once it has imported the main file double click it and ghidra will open the decompiler. When it has loaded ghidra will ask you to analyse the file press yes and select the option at the top "(Switch) IPC Analyzer" then press Analyze. It will take a while so just be patient once its done then you will know because there will be nothing going on in the bottom right corner.
