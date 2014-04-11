project(MATLAB_CMAKE)
cmake_minimum_required(VERSION 2.8)

set(MATLAB_ROOT "/usr/local/MATLAB/MATLAB_Production_Server/R2013a"
    CACHE STRING "matlabroot")

# Get platform dependent mex-file extension
execute_process(COMMAND ${MATLAB_ROOT}/bin/mexext
                OUTPUT_VARIABLE MATLAB_MEX_EXT
                OUTPUT_STRIP_TRAILING_WHITESPACE)

macro(matlab_mex MEX_FCN_NAME MEX_SRC)
    get_filename_component(FILE_BASE_NAME ${MEX_SRC} NAME_WE)
    add_library(${FILE_BASE_NAME} SHARED ${MEX_SRC} ${ARGN})
    set_target_properties(${FILE_BASE_NAME} PROPERTIES
        COMPILE_DEFINITIONS MATLAB_MEX_FILE
        LIBRARY_OUTPUT_NAME ${FILE_BASE_NAME}.${MATLAB_MEX_EXT}
        PREFIX ""
        SUFFIX "")
    target_link_libraries(${FILE_BASE_NAME} mx mex mat)
endmacro(matlab_mex)

add_subdirectory(tests)
