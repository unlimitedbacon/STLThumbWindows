# STLThumbWindows

[![Build status](https://ci.appveyor.com/api/projects/status/ym2e7c0fykkr3f4o?svg=true)](https://ci.appveyor.com/project/unlimitedbacon/stlthumbwindows)

This is the Windows shell extension and Windows installer for [stl-thumb](https://github.com/unlimitedbacon/stl-thumb).

## Build Instructions

### Requirements

* [Rust](https://www.rust-lang.org/en-US/install.html)
* Visual Studio 2017
* [WiX Toolset](http://wixtoolset.org/releases/)
* [WiX Toolset Visual Studio 2017 Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)

### Steps

1. In the stl-thumb folder, run `cargo build --release`. This is necessary since Visual Studio does not (yet) support Rust projects.
2. Open STLThumbWindows.sln in Visual Studio and build the solution. The shell extension .dll will be in the x64 folder. The installer package will be in STLThumbSetupBundle\bin.

## Debugging

### Compile the extension
1. In the stl-thumb folder, run `cargo build --release`.
2. In Visual Studio, build the solution in Debug configuration.
3. Copy `STLThumbWindows\stl-thumb\target\release\stl-thumb.exe` to `STLThumbWindows\x64\Debug\`.

### Register extension with the Windows shell
4. Uninstall stl-thumb if it is installed.
5. Open a command prompt as administrator and navigate to `STLThumbWindows\x64\Debug\`.
6. Run `regsvr32.exe STLThumbWinShellExtension.dll`.
7. Use Regedit to add this registry key: `Computer\HKEY_CLASSES_ROOT\CLSID\{AF07F051-9D08-44A7-8C63-9296ADFEDDD7}\DisableProcessIsolation=REG_DWORD:1`. This forces the extension to run in-process in explorer.exe instead of in it's own process.

### Attach the debugger to Windows Explorer
8. In Visual Studio, go to Debug > Attach to Process... and choose `explorer.exe`.
9. Create or edit an STL file, causing a new thumbnail to be generated.

The output of `stl-thumb.exe` will be logged to the file `out.log`. Be aware that when you hit a breakpoint the Windows shell will freeze, making the desktop and taskbar unresponsive.