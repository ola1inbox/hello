cmake_minimum_required(VERSION 3.16)

if(NOT DEFINED PATCH_VERSION)
  set(PATCH_VERSION "0")
endif()

set(PROJECT_VERSION 0.0.${PATCH_VERSION})

project(hello VERSION ${PROJECT_VERSION})

configure_file(version.h.in version.h)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core)

add_executable(hello_cli
  main.cpp
)
target_link_libraries(hello_cli Qt${QT_VERSION_MAJOR}::Core)
target_include_directories(hello_cli
    PRIVATE "${CMAKE_BINARY_DIR}"
)

include(GNUInstallDirs)
install(TARGETS hello_cli RUNTIME DESTINATION bin)

# --- Настройки CPack ---

set(CPACK_GENERATOR "DEB")
set(CPACK_PACKAGE_NAME ${PROJECT_NAME})
set(CPACK_PACKAGE_VENDOR "My Company")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Olga Resh <ola1@inbox.ru>")

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT "ola1@inbox.ru")

include(CPack)
