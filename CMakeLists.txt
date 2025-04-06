# ECMWF Toolbox

cmake_minimum_required(VERSION 3.12 FATAL_ERROR)

project(ecmwf-toolbox VERSION 2099.00.0.0 LANGUAGES C CXX)

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
option(WITHOUT_FDB5 "")
option(WITHOUT_MARS_CLIENT "")
option(WITHOUT_METVIEW "")

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

if (NOT WITHOUT_ODB)
    #add_subdirectory(odb/odb)
endif()

if (NOT WITHOUT_ODB_TOOLS)
    #add_subdirectory(odb/odb-tools)
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

if (NOT WITHOUT_MAGICS)
    #add_subdirectory(mars/fdb5)
endif()

if (NOT WITHOUT_MAGICS)
    #add_subdirectory(mars/mars-client)
endif()

if (NOT WITHOUT_METVIEW)
    #add_subdirectory(metv/metview)
endif()

ecbuild_bundle_finalize()
