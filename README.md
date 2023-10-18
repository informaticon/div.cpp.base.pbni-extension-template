# div.cpp.base.pbni-extension-template
Template for creating PBNI Extensions

## What needs changing
- Change the project name in `CMakeLists.txt`, this will be the names of the DLLs
- Replace every occurence of `templateLib` in `CMakeLists.txt` with the name of your project
- Create your sourcefiles at `src/` and add them to `CMakeLists.txt` in the `add_library` function
- [If you add CMake libraries] add them to `.github/workflows/build-release.yml`s `Install packages` step
- [If you use VSCode] Rename the targets in `CMakePresets.json` and remove `Install` target if you dont need it


## Setting up an environment
If this is your first time building a PBNI Extension, [instal vcpkg](https://vcpkg.io/en/getting-started.html). Then install boost:
```ps1
vcpkg install --triplet=x86-windows-static `
	boost-stacktrace `
	boost-utility `
	boost-multiprecision `
	boost-algorithm `
```

Run Cmake inside this folder
```ps1
mkdir build; cd build
cmake .. --preset vcpkg
```

Open `build/${YOUR_PROJECT_NAME}.sln`

## Building
First setup the environment, then either open the Project in Visual Studio or run inside the build folder
```ps1
cmake --build . --config MinSizeRel
```
