cmake_minimum_required(VERSION 3.5)

project(libbase VERSION 0.1 LANGUAGES CXX)

include(GNUInstallDirs)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_FILES
    chrono_utils.cpp    
    hex.cpp
    mapped_file.cpp
    parsebool.cpp
    parsenetaddress.cpp
    posix_strerror_r.cpp
    stringprintf.cpp
    strings.cpp
    threads.cpp
    utf8.cpp
)

include_directories(include)

add_library(${PROJECT_NAME} STATIC ${SRC_FILES})

if(MSVC)
    target_compile_definitions(${PROJECT_NAME} PRIVATE _CRT_SECURE_NO_WARNINGS)
endif()


install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}Targets ${INSTALL_DESTINATION_DEFAULT}
    INCLUDES DESTINATION include)
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(EXPORT ${PROJECT_NAME}Targets
    FILE ${PROJECT_NAME}Config.cmake
    NAMESPACE ${PROJECT_NAME}::
    DESTINATION lib/cmake/${PROJECT_NAME})

