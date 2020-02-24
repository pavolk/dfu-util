
set(TARGET dfu)
file(GLOB SOURCES RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "*.c")
list(REMOVE_ITEM SOURCES main.c prefix.c suffix.c)
set(INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(DEPS CONAN_PKG::libusb)

add_library(${TARGET} STATIC ${SOURCES})
target_include_directories(${TARGET} PUBLIC
                       $<BUILD_INTERFACE:${INCLUDE_DIR}>
                       $<INSTALL_INTERFACE:include>
)
if (MSVC)
	target_compile_options(${TARGET} PUBLIC /wd4200 /wd4127
									 PRIVATE /wd4702 /wd4996)
	target_compile_definitions(${TARGET} PUBLIC HAVE_WINDOWS_H _CRT_SECURE_NO_WARNINGS _OFF_T_DEFINED)
endif()
target_link_libraries(${TARGET} PRIVATE ${DEPS})

add_executable(dfu-util main.c)
target_compile_options(dfu-util PRIVATE /wd4996)
target_link_libraries(dfu-util dfu wingetopt CONAN_PKG::libusb)
