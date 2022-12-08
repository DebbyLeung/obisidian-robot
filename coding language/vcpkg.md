In .vs CMakeWorkspaceSettings.json

Add
```json
{
  "cmake.configureSettings": {
    "CMAKE_TOOLCHAIN_FILE": "C:\\<path>\\vcpkg\\scripts\\buildsystems\\vcpkg.cmake",
    "VCPKG_TARGET_TRIPLET": "x64-windows"
  }
}
```
