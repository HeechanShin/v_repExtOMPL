Building the OMPL plugin:
=========================

What you need:
    - C++ compiler
    - v_repStubsGen (available from https://github.com/fferri/v_repStubsGen)
        - Python interpreter (2.7 or greater)
        - lxml package for Python
        - tempita package for Python
    - An XSLT Processor, such as SAXON (needed for generate documentation)

Build steps:

    1) obtain v_repStubsGen:

        > mkdir external
        > cd external
        > git clone https://github.com/fferri/v_repStubsGen.git
        > export PYTHONPATH=$PYTHONPATH:$PWD

    2) Generate stubs for Lua callbacks:

        > python -m v_repStubsGen -H stubs.h -C stubs.cpp callbacks.xml

    3) Compile stubs.cpp and v_repExtOMPL.cpp into the dll/dylib/so library

    4) (optional) generate documentation with an XSLT processor:

        > saxon -s:callbacks.xml -a:on -o:reference.html


Minor revision for DubinsStateSpace:
====================================
- The only changes are done in v_repExtOMPL.cpp

- TurningRadius and symmetricity of Dubins Curve should
  be hardcoded due to the lack of parameter for simExtOMPL_createStateSpace
  (Line number 513: in v_repExtOMPL.cpp)

- If you have some problem related to 'boost::assign::listof' during compilation with -std=c++0x, 
  replace 'boost::assign::listof(1)(2)(3)' with std::vector<float>{1,2,3}'
