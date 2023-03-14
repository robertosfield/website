cmake_minimum_required(VERSION 3.14)

project(vsg-dev)

set(DOXYGEN_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/docs/ref/VulkanSceneGraph)
add_subdirectory(VulkanSceneGraph)

set(DOXYGEN_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/docs/ref/vsgXchange)
add_subdirectory(vsgXchange)

set(DOXYGEN_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/docs/ref/vsgImGui)
add_subdirectory(vsgImGui)

#set(DOXYGEN_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/ref/vsgQt)
#add_subdirectory(vsgQt)

set(DOXYGEN_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/docs/ref/vsgExamples)
add_subdirectory(vsgExamples)
