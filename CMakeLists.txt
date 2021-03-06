# Deep Learning for Robust Normal Estimation in Unstructured Point Clouds
# Copyright (c) 2016 Alexande Boulch and Renaud Marlet
#
# This program is free software; you can redistribute it and/or modify it under the
# terms of the GNU General Public License as published by the Free Software
# Foundation; either version 3 of the License, or any later version.
# This program is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
# FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.
# You should have received a copy of the GNU General Public License along with this
# program; if not, write to the Free Software Foundation, Inc., 51 Franklin Street,
# Fifth Floor, Boston, MA 02110-1301  USA
#
# PLEASE ACKNOWLEDGE THE ORIGINAL AUTHORS AND PUBLICATION:
# "Deep Learning for Robust Normal Estimation in Unstructured Point Clouds "
# by Alexandre Boulch and Renaud Marlet, Symposium of Geometry Processing 2016,
# Computer Graphics Forum

cmake_minimum_required(VERSION 2.6 FATAL_ERROR)
project(HoughCNN_project)

SET(CMAKE_BUILD_TYPE Release)

set( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin )
set( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib )

set(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} "/usr/lib/x86_64-linux-gnu/")


############################
## OPENMP
if(UNIX)
	#use openMP
	find_package( OpenMP REQUIRED)
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
	set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif(UNIX)

include_directories("include")


# Make the scripts available in the 'cmake' directory available for the
# 'include()' command, 'find_package()' command.
set( CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_LIST_DIR}/cmake )

# Include the CMake script UseCython.cmake.  This defines add_cython_module().
# Instruction for use can be found at the top of cmake/UseCython.cmake.
include( UseCython )

include_directories("python")

### build the libraies in the package directory
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/python")

add_subdirectory(src)
