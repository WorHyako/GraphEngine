cmake_minimum_required(VERSION 3.24)

project(diNgine)

set(CMAKE_CXX_STANDARD 17)

#############################################
### Option to control third party modules ###
#############################################
option(USE_ASSIMP "Assimp" ON)
option(USE_EASY_PROFILER "Easy profiler" ON)
option(USE_GLAD "Glad" ON)
option(USE_GLFW "Glfw" ON)
option(USE_GLM "Glm" ON)
option(USE_GLI "Gli" ON)
option(USE_GLSLANG "Glslang" ON)
option(USE_IMGUI "ImGui" ON)
option(USE_MINI "mINI" ON)
option(USE_OPTICK "Optick" OFF)
option(USE_STB "Stb" ON)
option(USE_TASK_FLOW "Task flow" ON)
option(USE_TRACY "Tracy" ON)
option(USE_VOLK "Volk" ON)
option(LOG_ALL "Log all results" OFF)
option(USE_VULKAN "Vulkan" OFF)

##################################
### Additional cmake utilities ###
##################################
include(CmakeUtils/SourceGrouping.cmake)
include(CmakeUtils/LibrarySorter.cmake)

###################
### Third party ###
###################
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Src/ThirdParty)
sort_library(${ThirdParty_Libs})

################
### Executer ###
################
add_executable(${PROJECT_NAME})

target_sources(${PROJECT_NAME}
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp
        PRIVATE ${Shared_Sources}
        PRIVATE ${Platform_Sources}
        PRIVATE ${Rhi_Sources})

target_include_directories(${PROJECT_NAME}
        PRIVATE ${ThirdParty_Include_Dirs})

target_link_libraries(${PROJECT_NAME}
        PRIVATE ${ThirdParty_Libs})
