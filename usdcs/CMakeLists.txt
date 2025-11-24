cmake_minimum_required(VERSION 3.20)
project(UsdCs LANGUAGES CXX)

# Path to your USD install root
set(USD_ROOT "../../Usd-23.02-win64")

# Source files from Unity's UsdCs folder
add_library(UsdCs SHARED
    usdCs_wrap.cpp
    diagnosticHandler.cpp
    dll_main.cpp
)

target_compile_features(UsdCs PRIVATE cxx_std_17)

target_compile_definitions(UsdCs PRIVATE
    PXR_PYTHON_SUPPORT_DISABLED=1
    NOMINMAX
    WIN32_LEAN_AND_MEAN
)

target_include_directories(UsdCs PRIVATE
    ${USD_ROOT}/include
    ${USD_ROOT}/include/boost-1_78
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_directories(UsdCs PRIVATE
    ${USD_ROOT}/lib
)

# Start minimal; add more libs if you get unresolved symbols
target_link_libraries(UsdCs PRIVATE
    usd_ms
    tf
    vt
    gf
    sdf
    arch
    plug
    usdGeom
    usdShade
    usdLux
    usdUtils
    tbb
)
