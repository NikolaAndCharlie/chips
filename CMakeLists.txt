cmake_minimum_required(VERSION 3.24)
project(chip LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
if(NOT DEFINED INSTALL_EXAMPLESDIR)
	set(INSTALL_EXAMPLESDIR "examples")
endif()

set(INSTALL_EXAMPLEDIR "${INSTALL_EXAMPLESDIR}/bin")


find_package(Qt6
	REQUIRED COMPONENTS Core Gui Widgets
	OPTIONAL_COMPONENTS PrintSupport
)

set(RC rc/images.qrc)
qt_add_executable(chip WIN32 ${RC})

file(GLOB SRC src/*.cpp)
file(GLOB HDR src/*.h)
target_sources(chip
  PRIVATE
  ${SRC}
  ${HDR}
)

target_link_libraries(chip
	PRIVATE
	Qt6::Core
	Qt6::Gui
	Qt6::Widgets
)

if(TARGET Qt6::PrintSupport)
	target_link_libraries(chip PRIVATE Qt6::PrintSupport)
endif()
