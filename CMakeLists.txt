# Copyright (C) 2007-2009 LuaDist.
# Created by Peter Kapec
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.

PROJECT(luagraph C)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
INCLUDE(dist.cmake)

# Find Graphviz
FIND_PACKAGE(GraphViz REQUIRED)

# Build grah module
INCLUDE_DIRECTORIES(src src/compat-5.1r5)
ADD_DEFINITIONS(-DCOMPAT_H -DVERSION="1.0.3" -DGVVERSION="2.20" )

SET(SRC src/gr_edge.c src/gr_graph.c src/gr_node.c src/gr_util.c )

ADD_LUA_MODULE(core ${SRC})
TARGET_LINK_LIBRARIES(core ${GRAPHVIZ_LIBRARIES})

# Install all files and documentation
INSTALL(TARGETS core DESTINATION ${INSTALL_CMOD}/graph)
INSTALL(FILES graph51.lua DESTINATION ${INSTALL_LMOD}  RENAME graph.lua)

INSTALL(FILES COPYING LICENSE README DESTINATION ${INSTALL_DATA})
INSTALL(DIRECTORY doc/ DESTINATION ${INSTALL_DOC})

INSTALL(DIRECTORY examples/ DESTINATION ${INSTALL_EXAMPLE})
INSTALL(FILES test/test.lua test/ref.dot  test/test_dat1.dot test/test_dat2.dot DESTINATION ${INSTALL_TEST})
