set(bin_name OtherTests)

file(GLOB_RECURSE SOURCES
    "model/param_initializer/*.cpp"
    "facilities/*.cpp"
    "policies/*.cpp"
    "main.cpp"
)

include_directories(
    "."
    ".."
    "../.."
)

add_executable(${bin_name} ${SOURCES})
# target_link_libraries(${bin_name} PRIVATE MetaNN::MetaNN)