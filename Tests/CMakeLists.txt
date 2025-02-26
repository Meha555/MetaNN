# find_package(MetaNN CONFIG REQUIRED)

if(MetaNN_FOUND)
    message("MetaNN_DIR: ${MetaNN_DIR}")
    message("MetaNN_INCLUDE_DIR: ${MetaNN_INCLUDE_DIR}")
endif()

add_subdirectory(DataOpTest)
add_subdirectory(LayerTest)
add_subdirectory(OtherTests)