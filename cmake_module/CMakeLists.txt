#-- Service --------------------------------------------------------------------
CMAKE_MINIMUM_REQUIRED(VERSION 3.8.0)

#-- Project config -------------------------------------------------------------
PROJECT(c_module_template)

#-- Project paths --------------------------------------------------------------
SET(APP_PATH .)
SET(MODULE_SRC_PATH ./src)
SET(MODULE_INC_PATH ./inc)

#-- Include dirs ---------------------------------------------------------------
INCLUDE_DIRECTORIES(${APP_PATH})
INCLUDE_DIRECTORIES(${MODULE_INC_PATH})

#-- Sources list ---------------------------------------------------------------
FILE(GLOB APP_SRC ${APP_PATH}/*.c)

#-- Libs -----------------------------------------------------------------------
FILE(GLOB_RECURSE MODULE_SRC ${MODULE_SRC_PATH}/*.c)
ADD_LIBRARY(MODULE ${MODULE_SRC})

#-- Options --------------------------------------------------------------------
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99")

#-- Project linking ------------------------------------------------------------
ADD_EXECUTABLE(${PROJECT_NAME} ${APP_SRC})
TARGET_LINK_LIBRARIES(${PROJECT_NAME} MODULE)
