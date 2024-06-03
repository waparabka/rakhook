cmake_minimum_required (VERSION 3.0)

project ("rakhook" VERSION 1.0)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

include(FetchContent)

FetchContent_Declare(ktsignal GIT_REPOSITORY https://github.com/kin4stat/ktsignal.git GIT_TAG f08a19d9a00ad5284871bf44178d835da7b26ebf)
FetchContent_Declare(kthook GIT_REPOSITORY https://github.com/kin4stat/kthook.git GIT_TAG 21ca70481273d1efcc98ca49063178e46277009b)
FetchContent_Declare(xbyak GIT_REPOSITORY https://github.com/herumi/xbyak.git GIT_TAG 1c35e34abc359d14d7cba2505f2c851354298f5c)
FetchContent_MakeAvailable(ktsignal kthook xbyak)

add_library(${PROJECT_NAME} STATIC)
add_library(rakhook::rakhook ALIAS rakhook)

target_link_libraries(${PROJECT_NAME} PUBLIC kthook xbyak)

target_sources(${PROJECT_NAME} PRIVATE
    "source/offsets.cpp"
    "source/rakhook.cpp"
    "source/samp.cpp"
    "source/BitStream.cpp"
    "source/DS_HuffmanEncodingTree.cpp"
    "source/PluginInterface.cpp"
    "source/StringCompressor.cpp"
)

set_property(TARGET ${PROJECT_NAME} PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_20)