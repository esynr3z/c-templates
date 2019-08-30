#-- Service --------------------------------------------------------------------
cmake_minimum_required(VERSION 3.8.0)

#-- Project config -------------------------------------------------------------
project(cmake_module_check)

#-- Project paths --------------------------------------------------------------
set(APP_PATH .)
set(TESTS_PATH tests)
set(MODULE_SRC_PATH ./src)
set(MODULE_INC_PATH ./inc)

#-- Include dirs ---------------------------------------------------------------
include_directories(${APP_PATH})
include_directories(${MODULE_INC_PATH})

#-- Sources list ---------------------------------------------------------------
file(GLOB APP_SRC ${APP_PATH}/*.c)

#-- Libs -----------------------------------------------------------------------
file(GLOB_RECURSE MODULE_SRC ${MODULE_SRC_PATH}/*.c)
add_library(module ${MODULE_SRC})

#-- Options --------------------------------------------------------------------
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -pedantic -std=c99")

#-- Project linking ------------------------------------------------------------
add_executable(${PROJECT_NAME} ${APP_SRC})
target_link_libraries(${PROJECT_NAME} module)

#-- Tests ----------------------------------------------------------------------
enable_testing()
# Check framwork
find_package(PkgConfig)
pkg_check_modules(CHECK REQUIRED check)
include_directories(${CHECK_INCLUDE_DIRS})
link_directories(${CHECK_LIBRARY_DIRS})
# Add tests
file(GLOB TESTS ${TESTS_PATH}/test_*.c)
foreach(T_FILE ${TESTS})
    get_filename_component(T_NAME ${T_FILE} NAME_WE)
    add_executable(${T_NAME} ${T_FILE})
    target_link_libraries(${T_NAME} ${CHECK_LIBRARIES} module)
    add_test(NAME ${T_NAME} COMMAND ${T_NAME})
endforeach(T_FILE ${TESTS})
