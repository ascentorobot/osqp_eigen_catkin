cmake_minimum_required(VERSION 3.5)
project(osqp_eigen_catkin)

# Enable C++14
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED 11)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

set(${PROJECT_NAME}_src
  src/Data.cpp
  src/Settings.cpp
  src/Solver.cpp)

set(${PROJECT_NAME}_header
  include/OsqpEigen/OsqpEigen.h
  include/OsqpEigen/Constants.hpp
  include/OsqpEigen/SparseMatrixHelper.hpp
  include/OsqpEigen/SparseMatrixHelper.tpp
  include/OsqpEigen/Data.hpp
  include/OsqpEigen/Data.tpp
  include/OsqpEigen/Settings.hpp
  include/OsqpEigen/Solver.hpp
  include/OsqpEigen/Solver.tpp)

cs_add_library(${PROJECT_NAME} ${${PROJECT_NAME}_src} ${${PROJECT_NAME}_header})

## Testing
option(BUILD_TESTING "Create tests using CMake" OFF)
option(RUN_VALGRIND_TESTS "Run tests with Valgrind" FALSE)
mark_as_advanced(RUN_VALGRIND_TESTS)
include(CTest)
if(BUILD_TESTING)
  add_subdirectory(tests)
endif()


cs_install()
cs_export()
