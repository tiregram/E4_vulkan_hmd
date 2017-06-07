cmake_minimum_required (VERSION 2.6)
project(VULKAN_HMD)

set (PROJECT_SOURCE_DIR src)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)



find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)
if(GLFW_FOUND)
  include_directories(${GLFW_INCLUDE_DIRS})
else()
    message(ERROR " GLFW not found!")
endif()



find_package(Vulkan REQUIRED)
if(Vulkan_FOUND)
    include_directories(${Vulkan_INCLUDE_DIRS})
else()
    message(ERROR " Vulkan not found!")
endif()

include_directories ("${PROJECT_SOURCE_DIR}/include")
file(GLOB_RECURSE project_file_cpp ${PROJECT_SOURCE_DIR}/*.cpp)


add_executable(run_vulkan_hmd ${project_file_cpp})


if(Vulkan_FOUND)
  target_link_libraries(run_vulkan_hmd ${Vulkan_LIBRARIES})
else()
    message(ERROR " vulkan not found!")
endif()




if(GLFW_FOUND)
  target_link_libraries(run_vulkan_hmd ${GLFW_LIBRARIES})
  target_link_libraries(run_vulkan_hmd ${GLFW_STATIC_LIBRARIES})
else()
    message(ERROR " glfw3 not found!")
endif()


