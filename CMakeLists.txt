cmake_minimum_required(VERSION 3.10...3.27)
project(MyProject VERSION 1.0.0 LANGUAGES CXX)

# Общие настройки CPack
set(CPACK_PACKAGE_NAME "solver")
set(CPACK_PACKAGE_VENDOR "YourCompany")
set(CPACK_PACKAGE_CONTACT "contact@yourcompany.com")
set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/License.rtf")
set(CPACK_VERBATIM_VARIABLES YES)

# Обязательные базовые настройки
set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
set(CPACK_PROJECT_DESCRIPTION "Solver application")
set(CPACK_PROJECT_HOMEPAGE_URL "https://yourproject.org")

# Настройки для Linux
if(UNIX AND NOT APPLE)
    set(CPACK_GENERATOR "DEB;RPM")
    set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Maintainer <maintainer@example.com>")
    set(CPACK_DEBIAN_PACKAGE_DEPENDS "libfmt-dev")
    set(CPACK_RPM_PACKAGE_REQUIRES "libfmt-devel")
endif()

# Настройки для Windows
if(WIN32)
    set(CPACK_GENERATOR "WIX")
    string(UUID CPACK_WIX_PRODUCT_GUID NAMESPACE "00000000-0000-0000-0000-000000000000" NAME "solver" TYPE SHA1)
    string(UUID CPACK_WIX_UPGRADE_GUID NAMESPACE "${CPACK_WIX_PRODUCT_GUID}" NAME "upgrade" TYPE SHA1)
    set(CPACK_WIX_LICENSE_RTF "${CMAKE_CURRENT_SOURCE_DIR}/License.rtf")
    set(CPACK_WIX_CULTURES "en-US;ru-RU")
    set(CPACK_WIX_ARCHITECTURE "x64")
    set(CPACK_WIX_TEMPLATE "${CMAKE_CURRENT_SOURCE_DIR}/WixCultureFix.wxs")
endif()

# Настройки для macOS
if(APPLE)
    set(CPACK_GENERATOR "DragNDrop")
    set(CPACK_DMG_VOLUME_NAME "Solver")
endif()

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
add_subdirectory(hello_world_application)
add_subdirectory(solver_application)

include(CPack)
