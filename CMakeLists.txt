cmake_minimum_required(VERSION 3.10...3.27)
project(MyProject VERSION 1.0.0 LANGUAGES CXX)

# Настройки CPack
include(InstallRequiredSystemLibraries)
set(CPACK_PACKAGE_NAME "solver")
set(CPACK_PACKAGE_VENDOR "YourCompany")
set(CPACK_PACKAGE_CONTACT "contact@yourcompany.com")
set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/License.rtf")
set(CPACK_VERBATIM_VARIABLES YES)

# Общие настройки для всех платформ
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Equation solver application")
set(CPACK_PACKAGE_DESCRIPTION "A powerful equation solver application")
set(CPACK_PACKAGE_FILE_NAME "${CPACK_PACKAGE_NAME}-${CPACK_PACKAGE_VERSION}-${CMAKE_SYSTEM_NAME}")

# Настройки для Linux (DEB/RPM)
if(UNIX AND NOT APPLE)
    set(CPACK_GENERATOR "DEB;RPM")
    set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Your Name <contact@yourcompany.com>")
    set(CPACK_DEBIAN_PACKAGE_DEPENDS "libfmt-dev")
    set(CPACK_RPM_PACKAGE_REQUIRES "libfmt-devel")
    set(CPACK_DEBIAN_FILE_NAME DEB-DEFAULT)
    set(CPACK_RPM_FILE_NAME RPM-DEFAULT)
endif()

# Настройки для Windows (WIX)
if(WIN32)
    set(CPACK_GENERATOR "WIX")
    # Генерируйте новые GUID для каждого проекта!
    set(CPACK_WIX_PRODUCT_GUID "D9FD9F0A-0D7B-4B1F-8E7A-1A3F4B2C5D6E")
    set(CPACK_WIX_UPGRADE_GUID "3A4B5C6D-7E8F-9A0B-1C2D-3E4F5A6B7C8D")
    set(CPACK_WIX_LICENSE_RTF "${CMAKE_CURRENT_SOURCE_DIR}/License.rtf")
    set(CPACK_WIX_CULTURES "en-US")
    set(CPACK_WIX_PRODUCT_ICON "${CMAKE_CURRENT_SOURCE_DIR}/assets/icon.ico")
    set(CPACK_WIX_UI_BANNER "${CMAKE_CURRENT_SOURCE_DIR}/assets/banner.bmp")
    set(CPACK_WIX_UI_DIALOG "${CMAKE_CURRENT_SOURCE_DIR}/assets/dialog.bmp")
    set(CPACK_WIX_TEMPLATE "${CMAKE_CURRENT_SOURCE_DIR}/WixTemplate.wxs")
    set(CPACK_WIX_PROGRAM_MENU_FOLDER "MyProject")
endif()

# Настройки для macOS
if(APPLE)
    set(CPACK_GENERATOR "DragNDrop")
    set(CPACK_DMG_VOLUME_NAME "Solver")
    set(CPACK_DMG_FORMAT "UDBZ")
    set(CPACK_DMG_BACKGROUND_IMAGE "${CMAKE_CURRENT_SOURCE_DIR}/assets/background.png")
endif()

# Подпроекты
add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
add_subdirectory(hello_world_application)
add_subdirectory(solver_application)

# Включение CPack должен быть ПОСЛЕ всех add_subdirectory
include(CPack)
