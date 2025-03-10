cmake_minimum_required(VERSION 2.8.12)
if (POLICY CMP0048)
  cmake_policy(SET CMP0048 NEW)
endif (POLICY CMP0048)
project(qshellwidget)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Qt
set(CMAKE_AUTOMOC ON)
find_package(Qt${QT_VERSION_MAJOR}Widgets REQUIRED)
if(ENABLE_TESTS)
	find_package(Qt${QT_VERSION_MAJOR}Test REQUIRED)
endif()

if (WIN32 AND USE_STATIC_QT)
	add_definitions(-DUSE_STATIC_QT)
endif ()

set(SOURCES
  cell.cpp
  cursor.cpp
  highlight.cpp
  helpers.cpp
  konsole_wcwidth.cpp
  shellcontents.cpp
  shellwidget.cpp
  compat_shellwidget_qt${QT_VERSION_MAJOR}.cpp)

add_library(qshellwidget STATIC ${SOURCES})
target_link_libraries(qshellwidget Qt${QT_VERSION_MAJOR}::Widgets compat)

add_executable(example EXCLUDE_FROM_ALL example.cpp)
target_link_libraries(example qshellwidget )
add_executable(example2 EXCLUDE_FROM_ALL example2.cpp)
target_link_libraries(example2 qshellwidget )
add_executable(example3 EXCLUDE_FROM_ALL example3.cpp)
target_link_libraries(example3 qshellwidget )

add_executable(fontinfo EXCLUDE_FROM_ALL fontinfo.cpp)
target_link_libraries(fontinfo Qt${QT_VERSION_MAJOR}::Widgets )
