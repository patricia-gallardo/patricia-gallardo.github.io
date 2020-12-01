---
title: ASan on Windows in CMake in CLion
description: Quick Notes
author: Patricia Aas
layout: post
icon: fa-film
image: "/assets/images/graffiti-4940293_640.jpg"
---

This post is mostly to future Patricia because she will be very annoyed with me if I don't write it. As usual she gets no nice fluffy text and so you don't either. Sorry.

This works - that does not mean it is all needed.

In the CMakeLists.txt in the lib folder:

``` cmake
file(GLOB_RECURSE sources CONFIGURE_DEPENDS "*.cpp")
add_library(libpacman ${sources})
target_compile_options(libpacman PRIVATE -fsanitize=address) # /MD will be used implicitly
target_link_directories(libpacman PRIVATE "$ENV{ProgramFiles\(x86\)}/Microsoft Visual Studio/2019/Community/VC/Tools/Llvm/x64/lib/clang/10.0.0/lib/windows")
target_link_libraries(libpacman PRIVATE sdl2::sdl2 sdl2_image::sdl2_image clang_rt.asan_dynamic-x86_64 clang_rt.asan_dynamic_runtime_thunk-x86_64)
target_link_options(libpacman PRIVATE /wholearchive:clang_rt.asan_dynamic_runtime_thunk-x86_64.lib /wholearchive:clang_rt.asan_dynamic-x86_64.lib)
```

In the CMakeLists.txt in the src folder:
``` cmake
file(GLOB_RECURSE sources CONFIGURE_DEPENDS "*.cpp")
add_executable(pacman ${sources})
target_compile_options(pacman PRIVATE -fsanitize=address) # /MD will be used implicitly
target_link_directories(pacman PRIVATE "$ENV{ProgramFiles\(x86\)}/Microsoft Visual Studio/2019/Community/VC/Tools/Llvm/x64/lib/clang/10.0.0/lib/windows")
target_link_libraries(pacman PRIVATE libpacman clang_rt.asan_dynamic-x86_64 clang_rt.asan_dynamic_runtime_thunk-x86_64)
target_link_options(pacman PRIVATE /wholearchive:clang_rt.asan_dynamic-x86_64.lib /wholearchive:clang_rt.asan_dynamic_runtime_thunk-x86_64.lib)
```
Then bluntly copy everything in "$ENV{ProgramFiles\(x86\)}/Microsoft Visual Studio/2019/Community/VC/Tools/Llvm/x64/lib/clang/10.0.0/lib/windows" to cmake-build-debug/pacman/bin/

This is a hammer, but you should be able to work it out, Patricia. And maybe inprove on this text? ;)

Based on 
* [AddressSanitizer (ASan) for Windows with MSVC](https://devblogs.microsoft.com/cppblog/addresssanitizer-asan-for-windows-with-msvc/)
* [How to Build C++ Projects with the Address Sanitizer on Windows](https://www.kdab.com/cpp-projects-asan-windows/)
