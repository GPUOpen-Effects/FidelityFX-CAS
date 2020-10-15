# CasCmdLine

Simple command line tool that processes image files using the FidelityFX Contrast Adaptive Sharpening (FidelityFX CAS) shader.

```
CasCmdLine 1.4
Command line syntax:
  CasCmdLine.exe [Options] <SrcFile1> <DstFile1> <SrcFile2> <DstFile2> ...
Options:
  -Scale <DstWidth> <DstHeight>
  -Mode <Mode>
    Mode can be: CAS (default), NearestNeighbor, Linear, Cubic, HighQualityCubic, Fant
  -Sharpness <Value>
    Sharpness for CAS, between 0 (default) and 1.
  -FP16
    If not set (default), uses R8G8B8A8_UNORM GPU texture format for CAS.
    If set, uses R16G16B16A16_FLOAT GPU texture format for CAS.
  -Linear
    If not set (default), treats input and output image as sRGB.
    If set, treats input and output image as linear.
    Works only when -FP16 is not specified.
Supported formats: BMP, PNG, ICO, JPG, TIF, GIF, DDS
```

Written in C++ using Visual Studio 2019. No external dependencies other than Windows API and Direct3D 11. Image file formats are handled using [Windows Imaging Component (WIC)](https://docs.microsoft.com/en-us/windows/win32/wic/-wic-about-windows-imaging-codec) which is part of the Win32 API. Shaders are compiled to H files (with a little help from the [Fx Batch Compiler](https://github.com/sawickiap/FxBatchCompiler) tool) and bundled with source code to be embedded into the executable.

A standalone prebuilt binary is also available: [x64\Release\CasCmdLine.exe](x64/Release/CasCmdLine.exe)
