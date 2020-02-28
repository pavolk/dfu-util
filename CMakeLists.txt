cmake_minimum_required(VERSION 3.1.0)

project(dfu-util VERSION 0.9)

if (NOT CONAN_DEPENDENCIES)
    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    conan_basic_setup(TARGETS)
endif ()

set(CMAKE_INSTALL_BINDIR bin)
set(CMAKE_INSTALL_LIBDIR lib)
set(CMAKE_INSTALL_INCLUDEDIR include)
if (WIN32)
	set(CMAKE_INSTALL_DATADIR data)
	set(CMAKE_INSTALL_DOCDIR doc/${PROJECT_NAME}-${PROJECT_VERSION})
else ()
	set(CMAKE_INSTALL_DATADIR share/${PROJECT_NAME}-${PROJECT_VERSION})
	set(CMAKE_INSTALL_DOCDIR share/doc/${PROJECT_NAME}-${PROJECT_VERSION})
endif()

add_subdirectory(src)

install(FILES COPYING AUTHORS README ChangeLog DESTINATION ${CMAKE_INSTALL_DOCDIR})
