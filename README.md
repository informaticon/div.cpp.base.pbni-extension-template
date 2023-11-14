# div.cpp.base.pbni-extension-template

Template for creating PBNI Extensions

## What needs changing

The project name is the package name accoring to the informaticon universal naming convention (e.g. lib.pbni.base.mail-client).

- Replace every occurence of `°°°PACKAGE_NAME°°°` in `CMakeLists.txt` with the name of your project
- Create your sourcefiles at `src/` and add them to `CMakeLists.txt` in the `add_library` function (replace `°°°SOURCE_FILES°°°` with them).

## Setting up an environment

If this is your first time building a PBNI Extension, [instal vcpkg](https://vcpkg.io/en/getting-started.html).
Then condiugre the project including installing the dependencies:

```ps1
cmake . -B build --preset vcpkg 
```

Open `build/${YOUR_PROJECT_NAME}.sln`

## Building

First setup the environment, then either open the Project in Visual Studio or run inside the root folder:

```ps1
cmake --build build/ --config MinSizeRel
```
