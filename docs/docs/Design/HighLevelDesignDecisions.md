---
layout: page
title: High Level Design Decisions
permalink: /documentation/docs/design/high_level_design_decisions
---

**Project name:** VulkanSceneGraph preferred, may need to use VkSceneGraph if permission from Khronos is not secured.

**Language:** C++17 minimum standard.

**Build tool:** lead choice CMake due to familiarity and market penetration.

**Source code control:** git hosted on github.

**Maths :** local GLSL style [maths](../../include/vsg/maths/) classes, inspired by GLSL, GLM and the Vulkan conventions.

**Windowing:** local native Windowing integrated with core VSG library, with ability to use 3rd party Windowing (short term use GLFW to get started quickly.)

**Vulkan integration:** Aim for coherent naming and granularity as in underlying Vulkan API

* lightweight [local C++ encapsulation](../../include/vsg/vk) of Vulkan objects, naming and style inspired by Vulkan C API.
* Provide convenient and robust setup and clean up of resources.
* Standard naming VkFeature -> vsg::Feature in include/vsg/vk/Feature
* Cmd naming vkCmdFeature -> vsg::Feature, sub-classed from [vsg::Command](../../include/vsg/vk/Command.h)
* State vkCmdFeature -> vsg::Feature, sub-classed from vsg::StateComponent and aggregated within a [vsg::StateGroup](../../include/vsg/nodes/StateGroup.h) node.


**Single library:** all core, maths, nodes, utilities, vulkan and viewer provided in libvsg library, can either be used as static or dynamic library.

**Namespace:** vsg used for all categories of functionality within the libvsg library.

**Headers:** .h used for public classes/functions

Categories of functionality placed in appropriately named subdirectories i.e.

* [include/vsg/core](../../include/vsg/core/)/Object.h
* [include/vsg/nodes/](../../include/vsg/nodes/)Group.h
* [include/vsg/vk/](../../include/vsg/vk/)Instance.h
For convenience, high level include/vsg/all.h header to include all of vsg/*/*.h

**Source:** .cpp extension used

Categories of functionality placed in appropriately named subdirectories i.e.

* [src/vsg/core/](../../src/vsg/core/)Visitor.cpp
* [src/vsg/app/](../../src/vsg/app/)Viewer.cpp


**Memory:** To address the main scene graph performance bottlenecks, have a general goal of improving cache coherency and lowering memory bandwidth load.

Intrusive reference counting twice as memory efficient as std::shared_ptr<>, and results in ~50% better traversals speeds. Use [vsg::ref_ptr<>](../../include/vsg/core/ref_ptr.h), [vsg::observer_ptr<>](../../include/vsg/core/observer_ptr.h) and vsg::Object.

Use std::atomic to provide efficient, thread safe reference counts.

To minimize the size of the majority of internal scene graph nodes and leaf nodes the auxiliary data that only a few objects require are moved out of the base vsg::Object/Node classes into a [vsg::Auxiliary](../../include/vsg/core/Auxiliary.h) object.

To enable greater control over memory management, provide [vsg::Allocator](../../include/vsg/core/Allocator.h) class to enable applications to control how the scene graph allocates and deletes memory.

**Unification:**
All vsg::Object support intrusive reference counting, meta data and type safe queries via [vsg::Visitor](../../include/vsg/core/Visitor.h) and [vsg::ConstVisitor](../../include/vsg/core/ConstVisitor.h).

All uniform and vertex array data can be handled via the [Data](../../include/vsg/core/Data.h) interface, single value data via the [vsg::Value](](../../include/vsg/core/Value.h)) template, Array data via the [vsg::Array](](../../include/vsg/core/Array.h)) template classes.

The main scene graph and the rendering back-end's command graph utilize the same scene graph hierarchy.

Vulkan [Compute](../../include/vsg/vk/ComputePipeline.h) and [Graphics](../../include/vsg/vk/GraphicsPipeline.h) to be supported with the same Vulkan wrappers, scene graph and command graph hierarchies.


**Usage models:** Application developers will be able to dispatch data directly to Vulkan using the VSG’s Vulkan wrappers in a form of an immediate mode, creating their own command graphs that use standard vsg command visitors or their own custom visitors, through to using visitor to cull the main scene graph down to a command graph each frame and dispatching this to vulkan.


**Introspection:** Not explored during Exploration Phase so will need to be addressed in future. Aim to provide introspection/reflection for all core scene graph objects to provide support for reading/writing scene graph objects and open the door to scripting.


**IO:** Support for loading 3rd party images and 3D models is currently deemed out of scope of the core libvsg library. The only IO supported will be via the native scene graph objects' support for reflection. This IO support will enable scene graphs, images and shaders to be read and written without any additional libraries.


Support for 3rd party images, 3D models and shaders will be provided by add
on libraries. To aid with porting of OpenSceneGraph applications an osg2vsg
library will be developed so that all loaders that the OpenSceneGraph has will
be available.  These 3rd party add on libraries providing images, 3D models and shaders will form an important part of testing of the VSG project as it evolves and are expected to develop in conjunction with the VSG project.
