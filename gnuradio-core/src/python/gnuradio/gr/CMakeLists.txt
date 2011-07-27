# Copyright 2010-2011 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
INCLUDE(GrPython)

GR_PYTHON_INSTALL(FILES
    __init__.py
    exceptions.py
    gr_threading.py
    gr_threading_23.py
    gr_threading_24.py
    hier_block2.py
    prefs.py
    top_block.py
    pubsub.py
    DESTINATION ${GR_PYTHON_DIR}/gnuradio/gr
    COMPONENT "core_python"
)

########################################################################
# Handle the unit tests
########################################################################
IF(ENABLE_TESTING)
INCLUDE(GrTest)
FILE(GLOB py_qa_test_files "qa_*.py")
FOREACH(py_qa_test_file ${py_qa_test_files})
    GET_FILENAME_COMPONENT(py_qa_test_name ${py_qa_test_file} NAME_WE)
    SET(GR_TEST_PYTHON_DIRS
        ${CMAKE_BINARY_DIR}/gnuradio-core/src/python
        ${CMAKE_BINARY_DIR}/gnuradio-core/src/lib/swig
    )
    SET(GR_TEST_TARGET_DEPS gruel gnuradio-core)
    GR_ADD_TEST(${py_qa_test_name} ${PYTHON_EXECUTABLE} ${py_qa_test_file})
ENDFOREACH(py_qa_test_file)
ENDIF(ENABLE_TESTING)