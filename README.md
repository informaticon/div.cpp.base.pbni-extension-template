# div.cpp.base.pbni-extension-template

Template for creating PBNI Extensions

## What needs changing

The project name is the package name according to the informaticon universal naming convention (e.g. lib.pbni.base.mail-client).

- Replace every occurence of `°°°PACKAGE_NAME°°°` in `CMakeLists.txt` with the name of your project
    - *If you want to use VSCode's CMake plugin, also replace the ones inside `CMakePresets.json`*
- Create your sourcefiles at `src/` and add them to `CMakeLists.txt` in the `add_library` function (replace `°°°SOURCE_FILES°°°` with them).

## Setting up an environment

If this is your first time building a PBNI Extension, [install vcpkg](https://vcpkg.io/en/getting-started.html) to `C:\vcpkg`
*If for some reason you cannot install vcpkg in `C:\vcpkg` you'll have to add `-DCMAKE_TOOLCHAIN_FILE="your_vcpkg_path/scripts/buildsystems/vcpkg.cmake"` to every cmake command that includes `--preset vcpkg[64]`*

Then configure the project including installing the dependencies using one of:

```ps1
# For 32-bit builds
cmake . -B build --preset vcpkg 

# For 64-bit builds
cmake . -B build --preset vcpkg64
```

Then you can open `build/${YOUR_PROJECT_NAME}.sln` using Visual Studio

## Building

First setup the environment, then either open the Project in Visual Studio or run inside the root folder:

```ps1
cmake --build build/ --config MinSizeRel
```

## Example code

arithmetic.h
```cpp
namespace Inf {
    class arithmetic : public PBNI_Class {
    public:
        PBInt f_add(PBInt, PBInt);
    };
}
```

arithmetic.cpp
```cpp
#include "arithmetic.h"

namespace Inf {
    INF_REGISTER_CLASS(arithmetic, L"u_pbni_arithmetic");

    INF_REGISTER_FUNC(f_add, L"of_add", L"ai_left", L"ai_right");
    PBInt arithmetic::f_add(PBInt arg0, PBInt arg1) {
        return arg0 + arg1;
    }
}
```
