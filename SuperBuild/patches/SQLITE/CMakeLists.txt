cmake_minimum_required(VERSION 2.8.3)

project(sqlite)

set(BUILD_SHARED_LIBS ON)

include_directories("${CMAKE_SOURCE_DIR}")
add_definitions(-DSQLITE_ENABLE_COLUMN_METADATA=1)
add_definitions(-DSQLITE_ENABLE_RTREE=1)
add_definitions(-DSQLITE_OMIT_LOAD_EXTENSION=1)
add_definitions(-DSQLITE_THREADSAFE=1)
add_library(sqlite3 sqlite3_win.c)
if(UNIX)
  set(CMAKE_C_FLAGS "-pthread")
endif()  
install(TARGETS sqlite3
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib)
  
file(GLOB SQLITE_HEADERS "${CMAKE_SOURCE_DIR}/sqlite*.h")
install(FILES ${SQLITE_HEADERS}
  DESTINATION include)

