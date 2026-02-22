# NoScreen

This function is used in setwindowaffinity, but unlike the original API function, this function does not create detection vectors, for example, when using setwindowaffinity, this function can easily be detected through getwindowdisplayaffinity, this function is exempt from this, in addition, you can put this protection on any window in the process without interfering with the memory of the process itself.

![hippo](https://i.ibb.co/JzBRcs6/gif.gif)

## How to Compile

### Prerequisites

- **Visual Studio 2019 or 2022** with the **Desktop development with C++** workload installed
- **Windows Driver Kit (WDK) 10.0.22621 or later** matching your Visual Studio version
  - Download from: https://learn.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk
  - The WDK extension for Visual Studio must be installed alongside the WDK
- **Windows SDK** (installed automatically with Visual Studio or WDK)

> **Note for Visual Studio 2026 users:** VS2026 may ship with WDK build tasks (version 18.0) that are not yet included in the current WDK installer. Use Visual Studio 2022 with the matching WDK to avoid build errors.

### Building the Kernel Driver

1. Open `kernel/kernel.sln` in Visual Studio.
2. Select the **Release | x64** configuration from the toolbar.
3. Build the solution (**Build → Build Solution** or `Ctrl+Shift+B`).
4. The compiled driver (`.sys`) will be placed in `kernel/x64/Release/`.

### Building the User-Mode Application

1. Open `user/user.sln` in Visual Studio.
2. Select the **Release | x64** configuration from the toolbar.
3. Build the solution (**Build → Build Solution** or `Ctrl+Shift+B`).
4. The compiled executable (`.exe`) will be placed in `user/x64/Release/`.

### Troubleshooting

**Error: `ValidateNTTargetVersion` task could not be loaded from `Microsoft.DriverKit.Build.Tasks.18.0.dll`**

This error occurs when the WDK build task assembly is missing, which typically happens with newer versions of Visual Studio that the installed WDK does not yet support. Solutions:

1. Use **Visual Studio 2022** together with the WDK for Windows 11 (10.0.22621 or 10.0.26100).
2. Ensure both Visual Studio and the WDK are the same release generation (e.g., both from the same Windows 11 SDK release).
3. Run the WDK installer again and select **Repair** to ensure all components are correctly installed.
4. Make sure the **Windows Driver Kit Visual Studio extension** (VSIX) step in the WDK installer completed successfully.
