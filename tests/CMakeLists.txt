include_directories("${MATLAB_ROOT}/extern/include")
link_directories(${MATLAB_ROOT}/bin/glnxa64)

matlab_mex(hello hello.c)
matlab_mex(hellocpp hellocpp.cpp)
matlab_mex(explore explore.c)
