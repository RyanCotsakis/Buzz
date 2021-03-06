#
# Test programs
#

add_executable(testbuzzdarray testbuzzdarray.c)
target_link_libraries(testbuzzdarray buzz)

add_executable(testbuzzdict testbuzzdict.c)
target_link_libraries(testbuzzdict buzz)

add_executable(testbuzzset testbuzzset.c)
target_link_libraries(testbuzzset buzz)

add_executable(testbuzzlex ../buzz/buzzlex.h ../buzz/buzzlex.c testbuzzlex.c)
target_link_libraries(testbuzzlex buzz)

add_executable(testbuzzstrman testbuzzstrman.c)
target_link_libraries(testbuzzstrman buzz)

#
# Test scripts
#

if(NOT CMAKE_CROSSCOMPILING)
  # Make sure only the locally compiled tools are used
  set(BUZZ_COMPILER ${CMAKE_BINARY_DIR}/utility/bzzc)
  set(BUZZ_PARSER ${CMAKE_BINARY_DIR}/buzz/bzzparse)
  set(BUZZ_ASSEMBLER ${CMAKE_BINARY_DIR}/buzz/bzzasm)
  set(BUZZ_BZZ_INCLUDE_DIR
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR})
  # Initialize Buzz CMake stuff
  set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/utility)
  include(UseBuzz)

  buzz_make(test_takeoff_divide_flock.bzz)
  buzz_make(testempty.bzz)
  buzz_make(testif.bzz)
  buzz_make(testdebug.bzz)
  buzz_make(testbehavior.bzz)
  buzz_make(testclosure.bzz)
  buzz_make(testhexagon.bzz)
  buzz_make(testsquare.bzz)
  buzz_make(testgradient.bzz)
  buzz_make(testinclude1.bzz INCLUDES testinclude2.bzz)
  buzz_make(testio.bzz)
  buzz_make(testleds.bzz)
  buzz_make(testmath.bzz)
  buzz_make(testexpressions.bzz)
  buzz_make(testmsg.bzz)
  buzz_make(testneighbors.bzz)
  buzz_make(testparsing.bzz)
  buzz_make(teststigmergy.bzz)
  buzz_make(teststring.bzz INCLUDES ${CMAKE_SOURCE_DIR}/include/string.bzz)
  buzz_make(testswarm.bzz)
  buzz_make(testtable.bzz)
  buzz_make(testvec2.bzz INCLUDES ${CMAKE_SOURCE_DIR}/include/vec2.bzz)
  buzz_make(testwhile.bzz)
  buzz_make(testfor.bzz)
  buzz_make(testmobilecode.bzz)
  buzz_make(testbattery.bzz)
  buzz_make(testtablelib.bzz INCLUDES ${CMAKE_SOURCE_DIR}/include/table.bzz)
endif(NOT CMAKE_CROSSCOMPILING)
