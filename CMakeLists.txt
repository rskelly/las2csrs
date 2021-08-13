cmake_minimum_required(VERSION 3.12)

project (las2csrs)

enable_language(C)
enable_language(CXX)
set (CMAKE_CXX_STANDARD 17)
set (CMAKE_CXX_STANDARD_REQUIRED ON)
set (CMAKE_CXX_EXTENSIONS OFF)
set (CMAKE_POSITION_INDEPENDENT_CODE ON)
set (CMAKE_INCLUDE_DIRECTORIES_BEFORE ON)

set (CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set (CMAKE_INSTALL_RPATH "/usr/local/lib")
set (CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
set (CMAKE_CXX_COMPILER_LAUNCHER ccache)
set (CMAKE_CXX_FLAGS "-Wall -Wextra -Wno-unknown-pragmas -fopenmp -frounding-math -D_GLIBCXX_PARALLEL" CACHE STRING "compile flags" FORCE)
set (CMAKE_CXX_FLAGS_DEBUG "-g -O0" CACHE STRING "compile flags" FORCE)
set (CMAKE_CXX_FLAGS_RELEASE "-O3" CACHE STRING "compile flags" FORCE)
set (FS_LIB stdc++fs) # For filesystem features in c++17.

find_package (GDAL 2 REQUIRED)
find_package (Boost COMPONENTS system filesystem REQUIRED)
find_package (libLAS REQUIRED)
find_library (PROJ_LIBRARY proj)

# Configure directories###################################################################################

include_directories(
	include
	./liblas/include
	${GDAL_INCLUDE_DIR}
	${Boost_INCLUDE_DIRS}
)
	 
link_directories(
	./build/lib 
	./build/bin 
	${GDAL_LIBRARYDIR} 
	${Boost_LIBRARY_DIRS}
)

# Applications ##################################################################################################

add_executable (las2csrs src/las2csrs.cpp)	
target_link_libraries (las2csrs ${GDAL_LIBRARY} ${PROJ_LIBRARY} ${Boost_FILESYSTEM_LIBRARY} las_c)

install(TARGETS las2csrs RUNTIME DESTINATION bin LIBRARY DESTINATION lib) 
	
