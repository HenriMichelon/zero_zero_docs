Building & using ZeroZero
===========================================================================

Dependencies
---------------------------------------------------------------------------
Most of the dependencies used by ZeroZero are automatically configured
by the `CMakeLists.txt` of the engine except the Vulkan SDK and the build tools.

**Install the Vulkan SDK**
- [Vulkan SDK 1.3.x+](https://vulkan.lunarg.com/)

**Install the build tools**

For Microsoft Windows :
- [LLVM 19+](https://github.com/mstorsjo/llvm-mingw/releases) or [MSVC 19+ (VS 2022)](https://visualstudio.microsoft.com/fr/)
- [CMake 3.29+](https://cmake.org/download/) ([Visual Studio](https://learn.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio?view=msvc-170)) with a [build tool](https://github.com/ninja-build/ninja/releases)

For Linux and macOS :<br>We are waiting for your push request !

Create new project 
---------------------------------------------------------------------------
Use the [Template project](https://github.com/HenriMichelon/zero_zero_template) to
create a project that use the engine :
- Clone the template project and the [ZeroZero repository](https://github.com/HenriMichelon/zero_zero)
- Create a `.env.cmake` file in your project with a variable called `Z0_PROJECT_DIR` to reference the ZeroZero cloned directory, for example :
  `set(Z0_PROJECT_DIR "C:/Users/MyUser/Documents/GitHub/zero_zero")`
- If needed, adjust the `CMakeLists.txt` settings to your needs
- `cmake -B build -G Ninja -D CMAKE_BUILD_TYPE=Release`
- `cmake --build build`

Standalone build
---------------------------------------------------------------------------

- Clone the [ZeroZero repository](https://github.com/HenriMichelon/zero_zero)
- `cmake -B build -G Ninja -D CMAKE_BUILD_TYPE=Release` (adapt for your build tool)
- `cmake --build build`

