############################################################################
########################### Project Setup ##################################
############################################################################

# Setting CMake version properly to ensure correct policies behavior
cmake_minimum_required(VERSION 3.14...3.16)
# Setting up OpenDB project
project(odb VERSION 0.0.1
  LANGUAGES CXX)

# Configure build version
configure_file (
    "${PROJECT_SOURCE_DIR}/include/odb/version.hh.in"
    "${PROJECT_BINARY_DIR}/include/odb/version.hh"
)

############################################################################
################################# Targets ##################################
############################################################################

add_subdirectory(src/db)
add_subdirectory(src/defin)
add_subdirectory(src/defout)
add_subdirectory(src/lef)
add_subdirectory(src/lefin)
add_subdirectory(src/lefout)
add_subdirectory(src/def)
add_subdirectory(src/zutil)
add_subdirectory(src/cdl)

if(ENABLE_TESTS)
  add_subdirectory(test)
endif()

add_library(odb INTERFACE)
target_link_libraries(odb
  INTERFACE
    db
    cdl
    defin
    defout
    lefin
    lefout
    zutil
    utl_lib
    ${TCL_LIBRARY}
)

############################################################################
################################# SWIG #####################################
############################################################################

include(${SWIG_USE_FILE})

add_subdirectory(src/swig/common)
if (Python3_FOUND AND BUILD_PYTHON)
  add_subdirectory(src/swig/python)
endif()
add_subdirectory(src/swig/tcl)

############################################################################
############################### DOXYGEN ####################################
############################################################################
find_package(Doxygen)

if (DOXYGEN_FOUND)
  set(DOXYGEN_EXTRACT_STATIC YES)
  set(DOXYGEN_REFERENCED_BY_RELATION YES)
  set(DOXYGEN_REFERENCES_RELATION YES)

  doxygen_add_docs(docs include)
endif()

############################################################
# Unit testing
############################################################
if(ENABLE_TESTS)
  enable_testing()

  add_executable(parseTest
    ${PROJECT_SOURCE_DIR}/test/parseTest.cpp
  )

  target_link_libraries(parseTest
    odb
  )
endif()
