cmake_minimum_required (VERSION 2.6) 
project(BOSClass)

#set(LIBRARY_OUTPUT_PATH "${CMAKE_BINARY_DIR}/lib")

set(CMAKE_CXX_FLAGS "-g -Wall")

# ROOT libraries
include(FindROOT.cmake)
set(INCLUDE_DIRECTORIES ${ROOT_INCLUDE_DIR})
include_directories(${INCLUDE_DIRECTORIES})
set(LINK_DIRECTORIES ${ROOT_LIBRARY_DIR})
link_directories(${LINK_DIRECTORIES})

set(HEAD_SRCS HEAD.cxx)
set(HEAD_HEADERS HEAD.h)
set(HEAD_LINKDEF HEADLinkDef.h)
set(HEAD_DICTIONARY ${CMAKE_CURRENT_BINARY_DIR}/HEADDict.cxx)
ROOT_GENERATE_DICTIONARY("${HEAD_HEADERS}" "${HEAD_LINKDEF}" "${HEAD_DICTIONARY}" "${INCLUDE_DIRECTORIES}")
SET(HEAD_SRCS ${HEAD_SRCS} ${HEAD_DICTIONARY})


set(TAGR_SRCS TAGR.cxx)
set(TAGR_HEADERS TAGR.h)
set(TAGR_LINKDEF TAGRLinkDef.h)
set(TAGR_DICTIONARY ${CMAKE_CURRENT_BINARY_DIR}/TAGRDict.cxx)
ROOT_GENERATE_DICTIONARY("${TAGR_HEADERS}" "${TAGR_LINKDEF}" "${TAGR_DICTIONARY}" "${INCLUDE_DIRECTORIES}")
SET(TAGR_SRCS ${TAGR_SRCS} ${TAGR_DICTIONARY})


set(MCTK_SRCS MCTK.cxx)
set(MCTK_HEADERS MCTK.h)
set(MCTK_LINKDEF MCTKLinkDef.h)
set(MCTK_DICTIONARY ${CMAKE_CURRENT_BINARY_DIR}/MCTKDict.cxx)
ROOT_GENERATE_DICTIONARY("${MCTK_HEADERS}" "${MCTK_LINKDEF}" "${MCTK_DICTIONARY}" "${INCLUDE_DIRECTORIES}")
SET(MCTK_SRCS ${MCTK_SRCS} ${MCTK_DICTIONARY})


set(MCVX_SRCS MCVX.cxx)
set(MCVX_HEADERS MCVX.h)
set(MCVX_LINKDEF MCVXLinkDef.h)
set(MCVX_DICTIONARY ${CMAKE_CURRENT_BINARY_DIR}/MCVXDict.cxx)
ROOT_GENERATE_DICTIONARY("${MCVX_HEADERS}" "${MCVX_LINKDEF}" "${MCVX_DICTIONARY}" "${INCLUDE_DIRECTORIES}")
SET(MCVX_SRCS ${MCVX_SRCS} ${MCVX_DICTIONARY})

add_library(BOSClass SHARED ${HEAD_SRCS} ${TAGR_SRCS} ${MCTK_SRCS} ${MCVX_SRCS})
target_link_libraries(BOSClass ${ROOT_LIBRARIES})


# to build static library uncomment the following 3 lines
#SET_TARGET_PROPERTIES(BOSClass-static PROPERTIES OUTPUT_NAME "BOSClass")
#SET_TARGET_PROPERTIES(BOSClass-static PROPERTIES PREFIX "lib")
#add_library(BOSClass-static STATIC ${HEAD_SRCS} ${TAGR_SRCS} ${MCTK_SRCS} ${MCVX_SRCS})
