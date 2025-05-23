cmake_minimum_required(VERSION 3.10...3.27)
project(MyProject)

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
add_subdirectory(hello_world_application)
add_subdirectory(solver_application)

# Настройка CPack для создания пакетов
include(InstallRequiredSystemLibraries)
set(CPACK_PACKAGE_NAME ${PROJECT_NAME})
set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "My Project")
set(CPACK_PACKAGE_VENDOR "Your Company")
set(CPACK_VERBATIM_VARIABLES YES)

# Установка генераторов пакетов
if(WIN32)
    set(CPACK_GENERATOR "WIX")
elseif(APPLE)
    set(CPACK_GENERATOR "DragNDrop")
else()
    set(CPACK_GENERATOR "DEB;RPM")
endif()

include(CPack)

