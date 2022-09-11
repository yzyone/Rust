# Windows (MSVC with vcpkg) #

1. Install MS build tools and vcpkg
2. Install the needed SDL2 libs: vcpkg.exe install sdl2-ttf:x64-windows sdl2:x64-windows
3. Open a x64 native tools prompt (x64 Native Tools Command Prompt for VS 2019)
4. set env vars:

```
SET PATH=%PATH%;C:\Users\my_user\dev\vcpkg\installed\x64-windows\bin
SET INCLUDE=%INCLUDE%;C:\Users\my_user\dev\vcpkg\installed\x64-windows\include
SET LIB=%LIB%;C:\Users\my_user\dev\vcpkg\installed\x64-windows\lib
```

5. cargo build