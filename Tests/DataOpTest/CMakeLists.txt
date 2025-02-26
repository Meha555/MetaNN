set(bin_name DataOpTest)

file(GLOB_RECURSE SOURCES
    "operation/others/*.cpp"
    "operation/nn/*.cpp"
    "operation/tensor/*.cpp"
    "operation/math/*.cpp"
    "data/*.cpp"
    "data/facilities/*.cpp"
    "main.cpp"
)

include_directories(
    "."
    ".."
    "../.."
)

add_executable(${bin_name} ${SOURCES})
# target_link_libraries(${bin_name} PRIVATE MetaNN::MetaNN)