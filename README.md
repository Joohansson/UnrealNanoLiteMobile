# Unreal Nano Mobile

## Prereqs UE
1. Download and install the latest [Unreal Engine](https://www.unrealengine.com/en-US/download) (Publishing license)

## Prereqs Android
1. Download and install Android Studio 3.5.3. [Instructions](https://docs.unrealengine.com/en-US/Platforms/Mobile/Android/Setup/AndroidStudio/index.html)
2. Run the SetupAndroid (for example .bat if windows) script located in UnrealEngine-release\Engine\Extras\Android
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
3. Open UnrealNanoLite.sln in Visual Studio or UnrealNanoLite.xcodeproj xcode (Windows Vs. Mac)
4. Make sure "Development editor" and "Win64" is selected in the dropdowns (Project/Scheme/Edit scheme in xcode)
5. Right click on the Games/UnrealNanoLite in the solution explorer and Build (this will build the Nano plugin)
6. "Debug/Start without debugging" to open the editor (Product -> Run in xcode) or close VS and run the UnrealNanoLite.uproject (should launch in correct editor). Step 6 is not needed if only packaging on Windows. But on a Mac you need to package from Unreal Engine

## Package Instructions [Android](https://docs.unrealengine.com/en-US/Platforms/Mobile/Android/PackagingAndroidProject/index.html) - Mac
1. Start the game engine via step 6 above
2. Edit/Project settings => Android. APK => "configure for android" button. Also enter your keystore file info (the file should be copied to "Build/Android" and named UnrealNano.keystore)
3. If a device is connected: Test run the project via launch button arrow (select All_Android). If working, continue with 4
4. File/Package project/Android/ETC2

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