# Actually creating the mod

Now its time to do some coding! Lets write our first mod for Super Mario Odyssey! First open up the base that we downloaded in your ide of choice. Then navigate to to the main.cpp file found in the user/src folder. In the main.cpp file you will see alot of code already, This is for the logging feature, dont remove it. Now lets open ghidra and start the hard part, Looking for the function or symbol to hook onto. In ghidra press file and new project, You can name it whatever you want. Once you have created a new project press file again then import file, Navigate to the exefs folder we created before and select main. When you select it ghidra will automatically detect that it is a nintendo switch binary if you installed the switch loader correctly. Once it has imported the main file double click it and ghidra will open the decompiler. When it has loaded ghidra will ask you to analyse the file press yes and select the option at the top "(Switch) IPC Analyzer" then press Analyze. It will take a while so just be patient once its done then you will know because there will be nothing going on in the bottom right corner.

Now this is what we use ghidra for. Ghidra is used to search through the code so we can find where we want to hook. 

For this mod we are going to make a simple mod that increases the speed of mario after you collect a moon. So we need to look through ghidra to find the hook for when you collect a moon. TODO

Now that we have our hook we need to write the actual code for the mod! At the bottom of the main.cpp file in our base that we downloaded, you will see 
```cpp
extern "C" void userMain() {

}
```

In here at the bottom put `GetMoonHook::InstallAtSymbol("<ourhookwefoundbefore>");`

Now above that create a now struct like this 
```cpp
struct GetMoonHook : public mallow::hook::Trampoline<GetMoonHook> {
    static void Callback() {
        
    }
}```

In the Callback function put an if statment with the parameter `al::isFirstStep(-1)` you will need to include this function. You can check in the `OdysseyDecomp` on github to find which file `al::isFirstStep` can be found. 

This makes sure that the code is only ran once during the execution of the hook, otherwise our code will run once every frame! 

In our code we are going to