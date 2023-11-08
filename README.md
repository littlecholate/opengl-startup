## Cross-platform OpenGL startup with glad and glfw3

Tiny project when learning cmake, only create a window with glad and glfw to keep everything simple.

Code in src/main.cpp is directly copied from the [tutorial](https://learnopengl.com/Getting-started/Hello-Window).

## How to use

#### Windows

```
mkdir build
cd build
git submodule update --init --recursive
cmake -G "MinGW Makefiles" ..
mingw32-make
.\opengl-startup.exe
```

#### Linux

```
mkdir build
cd build
git submodule update --init --recursive
cmake ..
make
./opengl-startup
```

## File Structure

| Folder Name | Purpose                                 |
| ----------- | --------------------------------------- |
| external/   | put external library <br />             |
| res/        | put resources like img and music <br /> |
| src/        | put main code <br />                    |

## Reference

1. [The only CMake tutorial you will ever need](https://www.youtube.com/watch?v=A735Y4kMIPM)
2. [Git Submodules](https://www.youtube.com/watch?v=ED-WUk440qc)
3. [Use CMake to Build Cross-Platform Application](https://ken00535.medium.com/use-cmake-to-build-cross-platform-application-8888db861cb3)
