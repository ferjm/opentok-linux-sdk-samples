PROJECT(custom_video_capturer)

SET(CMAKE_VERBOSE_MAKEFILE ON)

CMAKE_MINIMUM_REQUIRED(VERSION 3.5)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -stdlib=libc++")

# Remove the commented out line below to enable OpenTok debug traces.
# SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DCONSOLE_LOGGING")

INCLUDE(FindPkgConfig)
PKG_SEARCH_MODULE(LIBSDL2 REQUIRED sdl2)
PKG_SEARCH_MODULE(LIBOPENTOK REQUIRED libopentok)

FIND_PACKAGE(Threads)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../common/src ${LIBSDL2_INCLUDE_DIRS} ${LIBOPENTOK_INCLUDE_DIRS})
LINK_DIRECTORIES(${LIBSDL2_LIBRARY_DIRS} ${LIBOPENTOK_LIBRARY_DIRS})

ADD_EXECUTABLE(${PROJECT_NAME} main.cpp ${CMAKE_CURRENT_SOURCE_DIR}/../common/src/otk_thread.c ${CMAKE_CURRENT_SOURCE_DIR}/../common/src/renderer.cpp)
TARGET_LINK_LIBRARIES(${PROJECT_NAME} pthread ${LIBSDL2_LIBRARIES} ${LIBOPENTOK_LIBRARIES})
