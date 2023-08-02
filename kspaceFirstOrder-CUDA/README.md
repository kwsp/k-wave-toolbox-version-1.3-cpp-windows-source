## k-wave source code patched for VC2022 + VCPKG

## Build instructions

1. Install [VCPKG](https://github.com/microsoft/vcpkg) and CUDA toolkit.
2. Run `C:\src\vcpkg\vcpkg.exe install --triplet x64-windows` to install the other dependencies (HDF5, zlib, szip) to `vcpkg_installed`
3. Edit `Sources\kspaceFirstOrder-CUDA.vcxproj` with a text editor:

    i. Change the CUDA toolkit version you want to use. If you installed the CUDA toolkit with Visual Studio support, the support files should've been installed in `C:\Program Files\Microsoft Visual Studio\2022\Community\Msbuild\Microsoft\VC\v170\BuildCustomizations`. In the vcxproj file, the two lines you need to modify look something like

        <ImportGroup Label="ExtensionSettings">
          <Import Project="$(VCTargetsPath)\BuildCustomizations\CUDA 11.7.props" />
        </ImportGroup>

        ...

        <ImportGroup Label="ExtensionTargets">
          <Import Project="$(VCTargetsPath)\BuildCustomizations\CUDA 11.7.targets" />
        </ImportGroup>

    ii. Add the CUDA architecture for your GPU if its a newer GPU. Check this [link](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/) for the GPU architecture name vs. the number. RTX 3090 is Ampere (`sm_80`), and RTX 4090 is Ada (`sm_89`).

        <CudaCompile>
          <TargetMachinePlatform>64</TargetMachinePlatform>
          <GenerateRelocatableDeviceCode>true</GenerateRelocatableDeviceCode>
          <CodeGeneration>compute_52,sm_52;compute_60,sm_60;compute_61,sm_61;compute_70,sm_70;compute_75,sm_75;compute_80,sm_80;</CodeGeneration>
          <FastMath>true</FastMath>
          <MaxRegCount />
        </CudaCompile>

4. Open the VS solution `kspaceFirstOrder-CUDA.sln` in Visual Studio and build in Release mode. Let me know if this doesn't work.


