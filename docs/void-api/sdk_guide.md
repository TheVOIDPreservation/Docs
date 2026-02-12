# SDK Guide

## Build Requirements

Building this project requires a legacy environment. If you choose to build from source, ensure your environment matches these specifications exactly.

### 1. Visual Studio Version
* **Recommended:** Visual Studio 2017
* **Alternative:** Visual Studio 2022 (requires **v141 / 2017 Build Tools** installed via the Visual Studio Installer).

### 2. Required Workloads and Components
Ensure the following are selected in the Visual Studio Installer:

**Workloads**

* Desktop development with C++
* Game development with C++

**Individual Components**

* Windows 10 SDK (10.0.17134.0)
* MSVC v141 - VS 2017 C++ x64/x86 build tools
* Windows 8.1 SDK (Must be installed manually from the Microsoft website).

---

## Critical Setup (Required)
The legacy Unreal Build Tool (UBT) is prone to version drift. It will often attempt to use the newest SDK on your system, which is incompatible for these games.

### Step 1: Force SDK Compatibility (SDK Hiding)
If you have Windows 10 or 11 SDKs newer than 17134 installed, you must temporarily hide them from the compiler:

1. Navigate to: `C:\Program Files (x86)\Windows Kits\10\Include`
2. Locate any folders newer than `10.0.17134.0`.
3. Rename them by adding an underscore prefix (e.g., rename `10.0.26100.0` to `_10.0.26100.0`).
4. **Important:** Remember to revert these names when working on modern projects or other engines.

### Step 2: Refresh Project Files
You must regenerate Visual Studio project files after installing new components or modifying the SDK directory. Right-click the `.uproject` file in your file explorer and select **Generate Visual Studio project files**.

---

## Packaging the mod
Because this project targets legacy dependencies, the standard "Package Project" option in the Unreal Editor will fail as it attempts to re-build. You must manually Cook the content and then use a standalone UnrealPak tool to create the final .pak file.

### 1. Cooking the Content
Before packaging, you must "cook" your assets to the platform-specific format:

1. Open your project in the Unreal Editor.
2. Go to **File > Cook Content for Windows**.
3. Wait for the process to complete. Your cooked assets will be located in:
`[ProjectFolder]\Saved\Cooked\WindowsNoEditor\`

### 2. Manual Content Cleanup
To ensure compatibility with the game and avoid unnecessary bloat, you must prune the cooked directory. Navigate to your cooked content folder and **delete** the following:

* `Engine/` (The entire engine folder)
* `AssetRegistry.bin`
* Delete everything in `Content` except for the `Mods` folder

### 3. Creating the .pak File
You will need the [UnrealPak tool](https://github.com/xamarth/unrealpak) to package the cooked assets.

1. Download and extract the UnrealPak utility.
2. Drag your cleaned `WindowsNoEditor` folder onto the `UnrealPak-With-Compression.bat` (with or without compression doesn't matter).
3. Rename the resulting `.pak` file to match the game's naming convention (usually `WindowsNoEditor.pak`).
4. You will need to rename this pak to `utils`
5. Place the pak file in the game's content directory to test.
