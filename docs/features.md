---
layout: page
title: Features
permalink: /features/
---

The VulkanSceneGraph project is comprised of the main VulkanSceneGraph library (provided by this repo) and a collection of optional libraries, each in their own dedicated repositories hosted alongside each other on [https://github.com/vsg-dev](https://github.com/vsg-dev), that provide additional features and example programs and templates for your own VulkanSceneGraph projects.

### Features provided by the core VulkanSceneGraph library are:

* Robust, thread safe memory management with custom block memory allocator and high performance smart pointers that are smaller and faster than std equivalents.
* GLSL style maths class - no need for 3rd party libs like GLM.
* Coherent Object model with easy to use and extend serialization, including native binary and ascii file support for all scene graph objects.
* C++ classes that encapsulate Vulkan Graphics and Compute C API in robust and convenient form, with robust resource management, including serialization support. Complexities and verbose setup usually associated with Vulkan are all dealt with for you so you can concentrate on your compute and graphics tasks.
* Vulkan extensions for ray tracing and mesh shading.
* Built in GLSL and SPIR-V shaders for Physics Based Rendering. phong and flat shading and text rendering.
* GLSL shader compilation to SPIR-V, using compiled in [glslang](https://github.com/vsg-dev/glslang), so users don't need to convert offline and can leverage #pragma(tic) shader composition.
* Class design focused on performance of scene graph operations by minimizing CPU bottlenecks: optimizing data density, layout, cache coherency and minimizing branching leading to better utilization of modern CPU and memory architectures. Traversals through to IO operations can be up to 10 times faster than with the OpenSceneGraph.
* Optimized scene graph performance has been essential for making the most of the performance that Vulkan itself provides over OpenGL/DirectX, benchmarks on large databases show 3 to 20 X performance improvements over OpenSceneGraph/OpenGL.
* Support for Cascaded Shadow Maps.
* Rigid Body and Skinnning Animation.
* Multi-threading support at the viewer level, file loading and database paging.
* Flexible Viewer architecture built around Vulkan command recording and queue submission.
* Native windowing and event support under Windows, Linux, Android, macOS and iOS.
* Support for double matrices in Camera and Transform class providing support for large database coordinate systems such as whole earth/GIS rendering whilst minimizing precision issues.
* Modern CMake build system that provides config installation alongside binaries making it easier to find and use all the appropriate build options for using the VulkanSceneGraph in your own projects.
* Minimal and complete approach to design - the whole VulkanSceneGraph interface and implementation, providing all the above functionality, takes 60 thousand lines of C++ code, compared to over 58 thousand for GLM headers, or vulkan.hpp (C++ wrapper for Vulkan) at over 94 thousand lines of code.  The VulkanSceneGraph replaces both and provides much more functionality besides.
* Extensible instrumentation system that enalbes users to implement custom instrumentatiop of low level scene graph work, or leverage off the shelf implementations for annotating Vulkan command buffer submissions, useful for use with [RenderDoc](https://renderdoc.org/) and Vulkan API debug output, or integaration [Tracy](https://github.com/wolfpld/tracy) frame profiler.
