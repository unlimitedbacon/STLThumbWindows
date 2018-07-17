# STLThumbWindows
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
