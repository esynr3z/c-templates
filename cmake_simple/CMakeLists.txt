#-- Service --------------------------------------------------------------------
CMAKE_MINIMUM_REQUIRED(VERSION 3.8.0)

#-- Project config -------------------------------------------------------------
PROJECT(c_simple_template)

#-- Project paths --------------------------------------------------------------
SET(APP_PATH ./src)

#-- Include dirs ---------------------------------------------------------------
INCLUDE_DIRECTORIES(${APP_PATH})

#-- Sources list ---------------------------------------------------------------
FILE(GLOB_RECURSE APP_SRC ${APP_PATH}/*.c)

#-- Options --------------------------------------------------------------------
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99")

#-- Project linking ------------------------------------------------------------
ADD_EXECUTABLE(${PROJECT_NAME} ${APP_SRC})
