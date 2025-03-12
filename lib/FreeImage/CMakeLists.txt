include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/CMakeHelper.cmake)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -fPIC -fexceptions -fvisibility=hidden -Wno-ctor-dtor-privacy")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3 -fPIC -fexceptions -fvisibility=hidden")

# OpenJPEG
add_definitions("-DOPJ_STATIC")

# LibRaw
add_definitions("-DNO_LCMS")

# LibJXR
add_definitions("-D__ANSI__")
add_definitions("-DDISABLE_PERF_MEASUREMENT")

# LibPNG
add_definitions("-DPNG_ARM_NEON_OPT=0")

file(GLOB_RECURSE HEADER_LIST LIST_DIRECTORIES TRUE *.hpp *.h)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${HEADER_LIST})

COLMAP_ADD_LIBRARY(FreeImage
    ${SOURCE_LIST}
)
target_include_directories(FreeImage PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/lib>
    $<INSTALL_INTERFACE:include/colmap/lib>
)
