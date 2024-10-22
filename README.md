# Unreal Nano Lite for Mobile

* [Youtube Trailer](https://youtu.be/IM03kMzry8I)
* [Downloads](https://unreal.nanos.cc)
* [Unreal Nano Lite Desktop](https://github.com/Joohansson/UnrealNanoLiteDesktop)

## Prereqs UE
1. Download and install [Unreal Engine](https://www.unrealengine.com/en-US/download) (Publishing license)
2. Currently tested and developed on Unreal Engine 4.26. Not backward compatible but hopefully forward with little effort.

## Prereqs Android
1. Download and install Android Studio 3.5.3. [Instructions](https://docs.unrealengine.com/en-US/Platforms/Mobile/Android/Setup/AndroidStudio/index.html)
2. Run the SetupAndroid (for example .bat if windows, .sh if Mac) script located in UnrealEngine\Engine\Extras\Android. Mac: /Users/Shared/Epic Games/UE_4.26/Engine/Extras/Android
3. A keystore file and password that represent your Android dev account [Instructions](https://docs.unrealengine.com/en-US/Platforms/Mobile/Android/DistributionSigning/index.html)

If 2 can't find SdkPath. Add it to regedit at Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Android Studio such as "C:\NVPACK\android-sdk-windows"

## Prereqs iOS
1. A Mac
2. Itunes
3. xcode
4. Apple certificate or possibly provision file (maybe only needed if testing on a device)

## Build Instructions for the Game
1. Clone this repo
2. Right click on UnrealNanoLite.uproject and "switch unreal engine version". Select the UE source you just installed (should be listed)
3. If Mac: Right click on UnrealNanoLite.uproject and "Generate Xcode Project" (Check the troubleshoot section further down)
4. Step 5-8 is not needed on Mac. Can just open UnrealNanoLite.uproject directly and it should ask to build the Nano plugin
5. Open UnrealNanoLite.sln in Visual Studio or UnrealNanoLite.xcodeproj xcode (Windows Vs. Mac)
6. Make sure "Development editor" and "Win64" is selected in the dropdowns (Product/Scheme/Edit scheme in xcode)
7. Right click on the Games/UnrealNanoLite in the solution explorer and Build (Windows) or Product/Build (Mac) (this will build the Nano plugin)
8. "Debug/Start without debugging" to open the editor (Windows) or Product -> Run in xcode (Mac) or close VS and run the UnrealNanoLite.uproject (should launch in correct editor). Step 6 is not needed if only packaging on Windows. But on a Mac you need to package from Unreal Engine

## Package Instructions [Android](https://docs.unrealengine.com/en-US/Platforms/Mobile/Android/PackagingAndroidProject/index.html) - Mac
1. Start the game engine via step 6 above
2. Edit/Project settings => Android. APK => "configure for android" button. Also enter your keystore file info (the file should be copied to "Build/Android" and named UnrealNano.keystore)
3. Edit/Plugins => Disable "Oculus VR" and restart editor (Or the app will complain about missing texture??)
4. If a device is connected: Test run the project via launch button arrow (select All_Android). If working, continue with 4
5. File/Package project/Android/ETC2

## Package Instructions [iOS](https://docs.unrealengine.com/en-US/Platforms/Mobile/iOS/PackagingiOSProject/index.html) - Mac
1. Start the game engine via step 6 above
2. Edit/Project settings => iOS and import your Apple provision (needed?) and certificate
3. If a device is connected: Test run the project via launch button arrow (select All_iOS). If working, continue with 4
4. File/Package project/iOS

## Package Instructions Android - Windows without using the Engine which saves time
1. Copy your keystore file to "Build/Android"
2. Edit Config/DefaultEngine.ini and change KeyStore, KeyAlias and KeyStorePassword to match yours
3. Copy UNREALNANOLIGHT_89E22627467FD0611C2E46B115F0F6FD.ulp2 to UnrealEngine-release\Engine\Programs\UnrealFrontend\Profiles
4. Launch UnrealEngine-release\Engine\Binaries\Win64\UnrealFrontend.exe
5. Make sure the correct platforms are selected for example Android and iOS
6. Add the project path at the top
7. Run the profile

## Package Instructions iOS - Windows
1. Will need a mac to remote SSH to
2. [Docs](https://docs.unrealengine.com/en-US/Platforms/Mobile/iOS/Windows/index.html)

## Install Android app (Windows)
1. Just run the Install bat file from the build folder. It will install the apk on the connected device (if it has debugging enabled)

## Install iOS app (Windows)
1. Use iPhonePackager [Docs](https://docs.unrealengine.com/en-US/Platforms/Mobile/iOS/iPhonePackager/index.html)

## Troubleshooting on Mac
Could be permission bugs when using UE4.26. First when generating xcode project files and then when building inside xcode. One solution for when generating xcode files fails is to press arrow up key in the terminal to get latest command and put "sudo" in front of the command. Another way is to run this (given these are the files it complains about). Not sure of chmod is needed.
Replace "user" with your username (maybe also the group "staff").

```
sudo chown user:staff "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/DotNETCommon/DotNETUtilities/obj/Development/DotNETUtilities.dll"
sudo chown user:staff "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/DotNETCommon/DotNETUtilities/obj/Development/DotNETUtilities.pdb"
sudo chown user:staff "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/DotNETCommon/DotNETUtilities/obj/Development/DotNETUtilities.csproj.FilesWrittenAbsolute.txt"
sudo chmod 777 "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/DotNETCommon/DotNETUtilities/obj/Development/DotNETUtilities.dll"
sudo chmod 777 "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/DotNETCommon/DotNETUtilities/obj/Development/DotNETUtilities.pdb"
sudo chmod 777 "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/DotNETCommon/DotNETUtilities/obj/Development/DotNETUtilities.csproj.FilesWrittenAbsolute.txt"
```

It's also likely you will get a similar permission error when building the game in xcode (different file). This should work:

```
sudo chown user:staff "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/UnrealBuildTool/obj/Development/UnrealBuildTool.csproj.FilesWrittenAbsolute.txt"
sudo chmod 777 "/Users/Shared/Epic Games/UE_4.26/Engine/Source/Programs/UnrealBuildTool/obj/Development/UnrealBuildTool.csproj.FilesWrittenAbsolute.txt"
```

## Special Thanks
[Nano Plugin for Unreal Engine](https://github.com/wezrule/UE4NanoPlugin)
