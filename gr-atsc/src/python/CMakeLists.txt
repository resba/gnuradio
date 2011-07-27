# Copyright 2011 Free Software Foundation, Inc.
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
# Install python examples
########################################################################
INCLUDE(GrPython)

GR_PYTHON_INSTALL(
    PROGRAMS
    btl-fsd.py
    fpll.py
    interp.py
    xlate.py
    viterbi-out.py
    DESTINATION ${GR_PKG_DATA_DIR}/examples/atsc
    COMPONENT "atsc_examples"
)

INSTALL(
    FILES README
    DESTINATION ${GR_PKG_DATA_DIR}/examples/atsc
    COMPONENT "atsc_examples"
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
        ${CMAKE_BINARY_DIR}/gr-atsc/src/lib
    )
    SET(GR_TEST_TARGET_DEPS gruel gnuradio-core gnuradio-atsc)
    GR_ADD_TEST(${py_qa_test_name} ${PYTHON_EXECUTABLE} ${py_qa_test_file})
ENDFOREACH(py_qa_test_file)
ENDIF(ENABLE_TESTING)