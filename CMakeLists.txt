# ECMWF Toolbox

cmake_minimum_required(VERSION 3.12 FATAL_ERROR)

project(ecmwf-toolbox VERSION 2099.00.0.0 LANGUAGES C CXX)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/ecbuild/cmake")
include(ecbuild_system)

set(CMAKE_CXX_STANDARD 17)

set(ENABLE_ECKIT_GEO               ON  CACHE BOOL "" FORCE)
set(ENABLE_ECKIT_SQL               ON  CACHE BOOL "" FORCE)
set(ECCODES_ENABLE_ECCODES_THREADS ON  CACHE BOOL "" FORCE)
set(ECCODES_INSTALL_EXTRA_TOOLS    ON  CACHE BOOL "" FORCE)
set(ECCODES_ENABLE_MEMFS           ON  CACHE BOOL "" FORCE)
set(ODB_ENABLE_BUILD_TOOLS         OFF CACHE BOOL "" FORCE)
set(MIR_ENABLE_BUILD_TOOLS         ON  CACHE BOOL "" FORCE)
set(FDB5_ENABLE_BUILD_TOOLS        OFF CACHE BOOL "" FORCE)
set(MARS_CLIENT_ENABLE_BUILD_TOOLS OFF CACHE BOOL "" FORCE)
set(ENABLE_FDB5                    ON  CACHE BOOL "" FORCE)
set(ECMWF                          ON  CACHE BOOL "" FORCE)
set(ENABLE_CODES_UI                ON  CACHE BOOL "" FORCE)
set(MV_BUNDLE_CONTAINS_METVIEW     1   CACHE BOOL "" FORCE)
set(MV_BUNDLE_CONTAINS_MAGICS      1   CACHE BOOL "" FORCE)
set(MV_BUNDLE_CONTAINS_ECCODES     1   CACHE BOOL "" FORCE)
set(ENABLE_EXPOSE_SUBPACKAGES      ON  CACHE BOOL "" FORCE)
set(ENABLE_METVIEW_FORTRAN         ON  CACHE BOOL "" FORCE)

set(ENABLE_METVIEW INTERNAL CACHE BOOL "" FORCE)

option(WITHOUT_ECKIT "")
option(WITHOUT_ECCODES "")
option(WITHOUT_ODC "")
option(WITHOUT_METKIT "")
option(WITHOUT_ODB "")
option(WITHOUT_ODB_TOOLS "")
option(WITHOUT_ATLAS "")
option(WITHOUT_ATLAS_ORCA "")
option(WITHOUT_MIR "")
option(WITHOUT_MAGICS "")
option(WITHOUT_FDB "")
option(WITHOUT_MARS_CLIENT "")
option(WITHOUT_METVIEW "")

option(INTERNAL "")
if (INTERNAL)
    set(ecbuild_DIR ${CMAKE_SOURCE_DIR}/ecbuild/cmake)
    include(FetchContent)
endif()

ecbuild_bundle_initialize()

if (NOT WITHOUT_ECKIT)
    add_subdirectory(eckit)
endif()

if (NOT WITHOUT_ECCODES)
    add_subdirectory(eccodes)
endif()

if (NOT WITHOUT_ODC)
    add_subdirectory(odc)
endif()

if (NOT WITHOUT_METKIT)
    add_subdirectory(metkit)
endif()

if (INTERNAL AND NOT WITHOUT_ODB)
    FetchContent_Declare(odb GIT_REPOSITORY ssh://git@git.ecmwf.int/odb/odb.git GIT_TAG develop)
    FetchContent_MakeAvailable(odb)
endif()

if (INTERNAL AND NOT WITHOUT_ODB_TOOLS)
    FetchContent_Declare(odb-tools GIT_REPOSITORY ssh://git@git.ecmwf.int/odb/odb-tools.git GIT_TAG develop)
    FetchContent_MakeAvailable(odb-tools)
endif()

if (NOT WITHOUT_ATLAS)
    add_subdirectory(atlas)
endif()

if (NOT WITHOUT_ATLAS_ORCA)
    add_subdirectory(atlas-orca)
endif()

if (NOT WITHOUT_MIR)
    add_subdirectory(mir)
endif()

if (NOT WITHOUT_MAGICS)
    add_subdirectory(magics)
endif()

if (NOT WITHOUT_FDB)
    add_subdirectory(fdb)
endif()

if (INTERNAL AND NOT WITHOUT_MARS_CLIENT)
    FetchContent_Declare(mars-client GIT_REPOSITORY git@github.com:ecmwf/mars-client.git GIT_TAG develop)
    FetchContent_MakeAvailable(mars-client)
endif()

if (INTERNAL AND NOT WITHOUT_METVIEW)
    FetchContent_Declare(metview GIT_REPOSITORY git@github.com:ecmwf/metview.git GIT_TAG develop)
    FetchContent_MakeAvailable(metview)
endif()

ecbuild_bundle_finalize()
