# Copyright (C) 2007-2012 LuaDist.
# Created by Peter Kapec
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.

project ( luagraph C )
cmake_minimum_required ( VERSION 2.8 )
include ( cmake/dist.cmake )
include ( lua )

# Find Graphviz
find_package ( GraphViz REQUIRED )

# Build grah module
include_directories ( src src/compat-5.1r5 )
add_definitions ( -DCOMPAT_H -DVERSION="1.0.3" -DGVVERSION="2.20" )

set ( SRC src/gr_edge.c src/gr_graph.c src/gr_node.c src/gr_util.c )

install_lua_module ( core ${SRC} LINK ${GRAPHVIZ_LIBRARIES} )
install_lua_module ( graph graph51.lua )

install_data ( COPYING LICENSE README )
install_doc ( doc/ )
install_example ( examples/ )
install_test ( test/test.lua test/ref.dot test/test_dat1.dot test/test_dat2.dot )
