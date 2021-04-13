cmake_minimum_required(VERSION 3.20) # FetchContent is available in 3.11+

project(cggii VERSION 0.0.1)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

#set(CMAKE_GENERATOR_PLATFORM Win32)

set(CPP_INCLUDE_DIRS "")
set(CPP_SOURCES_FILES "")
set(CPP_HEADERS_FILES "")

if (NOT glfw_FOUND)
  include(FetchContent)
  FetchContent_Declare(
    glfw
    GIT_REPOSITORY https://github.com/glfw/glfw.git
    GIT_TAG 3.3.4
  )
  FetchContent_GetProperties(glfw)
  if (NOT glfw_POPULATED) # Have we downloaded glfw yet?
    set(FETCHCONTENT_QUIET NO)
    FetchContent_Populate(glfw)

    set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE) # don't build the supplied examples
    set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE) # don't build the tests
    set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE) # don't build the docs
    set(GLFW_INSTALL OFF CACHE INTERNAL "" FORCE)
    #include_directories(${glfw_SOURCE_DIR}/include)
    list(APPEND CPP_INCLUDE_DIRS ${glfw_SOURCE_DIR}/include)

    #add_subdirectory(${glfw_SOURCE_DIR})
    message("glfw_SOURCE_DIR " ${glfw_SOURCE_DIR})
    message("glfw_BINARY_DIR " ${glfw_BINARY_DIR})
    add_subdirectory(${glfw_SOURCE_DIR} ${glfw_BINARY_DIR})

  endif()
endif()

if (NOT imgui_FOUND)
  include(FetchContent)
  FetchContent_Declare(
    imgui
    GIT_REPOSITORY https://github.com/ocornut/imgui.git
    GIT_TAG v1.82
  )
  FetchContent_GetProperties(imgui)
  if (NOT imgui_POPULATED) # Have we downloaded glfw yet?
    set(FETCHCONTENT_QUIET NO)
    FetchContent_Populate(imgui)
    #message("imgui_SOURCE_DIR " ${imgui_SOURCE_DIR})
    #include_directories(${imgui_SOURCE_DIR} ${imgui_SOURCE_DIR}/backends)
    list(APPEND CPP_SOURCES_FILES ${imgui_SOURCE_DIR}/imgui.cpp)
    list(APPEND CPP_SOURCES_FILES ${imgui_SOURCE_DIR}/imgui_demo.cpp)
    list(APPEND CPP_SOURCES_FILES ${imgui_SOURCE_DIR}/imgui_draw.cpp)
    list(APPEND CPP_SOURCES_FILES ${imgui_SOURCE_DIR}/imgui_tables.cpp)
    list(APPEND CPP_SOURCES_FILES ${imgui_SOURCE_DIR}/imgui_widgets.cpp)
    list(APPEND CPP_SOURCES_FILES ${imgui_SOURCE_DIR}/backends/imgui_impl_glfw.cpp)
    list(APPEND CPP_SOURCES_FILES ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp)

    list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/imgui.h)
    #list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/imconfig.h)
    #list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/imgui_internal.h)
    #list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/imstb_rectpack.h)
    #list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/imstb_textedit.h)
    #list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/imstb_truetype.h)
    list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/backends/imgui_impl_glfw.h)
    list(APPEND CPP_HEADERS_FILES ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.h)

    list(APPEND CPP_INCLUDE_DIRS ${imgui_SOURCE_DIR})
    list(APPEND CPP_INCLUDE_DIRS ${imgui_SOURCE_DIR}/backends)

  endif()
endif()

#look for lib file
find_library(glfw3_LIB NAMES glfw3 HINTS ${glfw_BINARY_DIR}/src/Debug) #lib search
include_directories(${CPP_INCLUDE_DIRS}) #need to be added in else error

#================================================
# EXECUTE APP
#add_executable(${PROJECT_NAME} main.cpp)
add_executable(${PROJECT_NAME} 
  #glad1glfw3.cpp #this will fail for testing for glad 1.0
  #glad2glfw3.cpp #pass since this glad 2.0.0
  #glfw_opengl3_imgui.cpp 
  src/cggii.cpp 
  ${CPP_SOURCES_FILES}
  ${CPP_HEADERS_FILES}
)

# GLAD 2.0
set(GLAD_DIR ${PROJECT_SOURCE_DIR}/glad)
add_library(glad ${GLAD_DIR}/src/gl.c)
target_include_directories(glad PRIVATE ${GLAD_DIR}/include)
target_include_directories(${PROJECT_NAME} PRIVATE ${GLAD_DIR}/include)
#target_link_libraries(${PROJECT_NAME} PUBLIC glad ${CMAKE_DL_LIBS} PRIVATE ${glfw3_LIB}) #pass
target_link_libraries(${PROJECT_NAME} PRIVATE ${glfw3_LIB} glad ${CMAKE_DL_LIBS})