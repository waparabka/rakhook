include(FetchContent)
include(GNUInstallDirs)

FetchContent_Declare(ktsignal GIT_REPOSITORY https://github.com/kin4stat/ktsignal.git GIT_TAG f08a19d9a00ad5284871bf44178d835da7b26ebf)
FetchContent_Declare(kthook GIT_REPOSITORY https://github.com/kin4stat/kthook.git GIT_TAG 21ca70481273d1efcc98ca49063178e46277009b)
FetchContent_Declare(xbyak GIT_REPOSITORY https://github.com/herumi/xbyak.git GIT_TAG 1c35e34abc359d14d7cba2505f2c851354298f5c)
FetchContent_MakeAvailable(ktsignal kthook xbyak)

add_library(rakhook STATIC)
add_library(rakhook::rakhook ALIAS rakhook)

target_include_directories(rakhook PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

target_compile_features(rakhook PUBLIC cxx_std_20)
target_link_libraries(rakhook PUBLIC ktsignal kthook xbyak)

target_sources(rakhook PRIVATE
    "RakHook/offsets.cpp"
    "RakHook/rakhook.cpp"
    "RakHook/samp.cpp"

    "RakNet/BitStream.cpp"
    "RakNet/DS_HuffmanEncodingTree.cpp"
    "RakNet/PluginInterface.cpp"
    "RakNet/StringCompressor.cpp"
)

set_property(TARGET rakhook PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
