message(STATUS "CMAKE_CURRENT_SOURCE_DIR = ${CMAKE_CURRENT_SOURCE_DIR}" )
message(STATUS "CMAKE_CURRENT_BINARY_DIR = ${CMAKE_CURRENT_BINARY_DIR}" )
message(STATUS "CMAKE_INSTALL_INCLUDEDIR = ${CMAKE_INSTALL_INCLUDEDIR}" )
message(STATUS "CMAKE_INSTALL_DATAROOTDIR = ${CMAKE_INSTALL_DATAROOTDIR}" )
message(STATUS "CMAKE_INSTALL_LIBDIR = ${CMAKE_INSTALL_LIBDIR}" )
message(STATUS "CMAKE_INSTALL_BINDIR = ${CMAKE_INSTALL_BINDIR}" )

file(GLOB_RECURSE HEADERS
    "data/*.h"
    "data/facilities/*.h"
    "data_copy/*.h"
    "evaluate/*.h"
    "facilities/*.h"
    "facilities/cont_metafuns/*.h"
    "layers/*.h"
    "layers/composite/*.h"
    "layers/principal/nn/*.h"
    "layers/principal/others/*.h"
    "layers/principal/tensor/*.h"
    "layers/principal/math/*.h"
    "layers/facilities/*.h"
    "layers/recurrent/*.h"
    "operation/*.h"
    "operation/others/*.h"
    "operation/nn/*.h"
    "operation/nn/facilities/*.h"
    "operation/tensor/*.h"
    "operation/math/*.h"
    "operation/facilities/*.h"
    "policies/*.h"
    "model/*.h"
    "model/param_initializer/*.h"
    "model/param_initializer/facilities/*.h"
    "model/weight_cont/*.h"
    "model/facilities/*.h"
    "meta_nn.h"
)

# head-only library
set(lib_name MetaNN)

add_library(${lib_name} INTERFACE)

target_compile_features(${lib_name} INTERFACE cxx_std_17)

target_include_directories(
    ${lib_name}
    INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

# install the target and create export-set
install(TARGETS ${lib_name}
        EXPORT ${lib_name}_Targets
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

# install header file
install(DIRECTORY ${PROJECT_SOURCE_DIR}/MetaNN
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${lib_name}
)

# generate and install export file
install(EXPORT ${lib_name}_Targets
        FILE ${lib_name}Targets.cmake
        NAMESPACE ${lib_name}::
        DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/cmake/${lib_name}
)

include(CMakePackageConfigHelpers)
# generate the version file for the config file
write_basic_package_version_file(
  "${lib_name}ConfigVersion.cmake"
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)

if(NOT INCLUDE_INSTALL_DIR)
  set(INCLUDE_INSTALL_DIR include)
endif()

# create config file
configure_package_config_file(
  "${PROJECT_SOURCE_DIR}/cmake/${lib_name}Config.cmake.in"
  "${PROJECT_BINARY_DIR}/${lib_name}Config.cmake"
  INSTALL_DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/cmake/${lib_name}
  PATH_VARS INCLUDE_INSTALL_DIR
)

# install config files
install(FILES "${PROJECT_BINARY_DIR}/${lib_name}Config.cmake"
              "${PROJECT_BINARY_DIR}/${lib_name}ConfigVersion.cmake"
        DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/cmake/${lib_name}
)

# generate the export targets for the build tree
export(EXPORT ${lib_name}_Targets
       FILE "${CMAKE_CURRENT_BINARY_DIR}/cmake/${lib_name}Targets.cmake"
       NAMESPACE ${lib_name}::
)