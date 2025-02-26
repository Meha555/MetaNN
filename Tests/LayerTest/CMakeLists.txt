set(bin_name LayerTest)

file(GLOB_RECURSE SOURCES
    "composite/*.cpp"
    "principal/nn/*.cpp"
    "principal/others/*.cpp"
    "principal/tensor/*.cpp"
    "principal/math/*.cpp"
    "recurrent/*.cpp"
    "main.cpp"
)

include_directories(
    "."
    ".."
    "../.."
)

add_definitions(-DMETANN_CHECKSHAPE)

add_executable(${bin_name} ${SOURCES})
# target_link_libraries(${bin_name} PRIVATE MetaNN::MetaNN)