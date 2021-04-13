# cggii 
 * cmake
 * glfw
 * glad
 * imgui

# LICENSE: MIT

# packages:
  * glfw 3.3.4
  * glad 2.0.0-BETA
  * imgui 1.82
  * cmake 3.20.1
  * opengl 3.3

# Information:
  Creating simple window that used imgui for graphic interface with glfw and glad for window and render build using the cmake build. But note that it still need compiler tools and opengl3 if install.

# Build:
  Tested window 10 64 bit Visual Studio Community 2019, Windows Kits and CMake.

  First error build. It need lib set up.

# Notes:
 * First error build that cmake link error glfw3.lib. Second time it should work.
 * Order of the build since used fetch git file build. Will cause error.
 * 

# Glad:
  There is premade files to help quick build test. It used web service generate the files.

# glad1:
 * https://github.com/Dav1dde/glad

# glad2: 2.0.0-BETA
 * https://github.com/Dav1dde/glad/tree/glad2

```
Language: c/c++

API:
  el version 1.5
  gl version 3.3
  gless1 version 1.0
  gles2 version 3.2
  glsc2 version 2.0
  glx version 1.4
  vulkan version 1.2
  wgl version 1.0

Options:
  -[ ] alias        Enables function pointer aliasing
  -[ ] debug        Enables generation of a debug build
  -[ ] header only  Generate a header only version of glad
  -[x] loader       Include internal loaders for APIs
  -[ ] merge        Merge multiple APIs of the same specification into one file.
  -[ ] mx           Enables support for multiple GL contexts
  -[ ] mx global    Mimic global GL functions with context switching
  -[ ] on demand    On-demand function pointer loading, initialize on use (experimental)
```