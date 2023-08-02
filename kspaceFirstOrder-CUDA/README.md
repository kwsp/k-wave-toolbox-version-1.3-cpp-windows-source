## k-wave source code patched for VC2022 + VCPKG

## Build instructions

1. Install [VCPKG](https://github.com/microsoft/vcpkg) and CUDA toolkit.
2. Run `C:\src\vcpkg\vcpkg.exe install --triplet x64-windows` to install the other dependencies (HDF5, zlib, szip) to `vcpkg_installed`
3. Modify `Sources\kspaceFirstOrder-CUDA.vcxproj` with a text editor to modify the CUDA toolkit version you want to use. The two lines you need to modify look something like

```
  <ImportGroup Label="ExtensionSettings">
    <Import Project="$(VCTargetsPath)\BuildCustomizations\CUDA 11.7.props" />
  </ImportGroup>

...

  <ImportGroup Label="ExtensionTargets">
    <Import Project="$(VCTargetsPath)\BuildCustomizations\CUDA 11.7.targets" />
  </ImportGroup>
```

4. Open the VS solution `kspaceFirstOrder-CUDA.sln` in Visual Studio and build in Release mode.
