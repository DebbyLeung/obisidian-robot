install external package for c and [[C++]].
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
#codingLanguage #cpp
cmake -B "C:\\Users\\Debby\ Leung\\source\\repos\\V2_agv_development\\out\\build" -S . -DCMAKE_TOOLCHAIN_FILE ="C:\\Users\\Debby\ Leung\\source\\scripts\\buildsystems\\vcpkg.cmake"