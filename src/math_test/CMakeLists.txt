set(MATH_TEST_SOURCES
  mathtest.F90
  robertsonMod.F90
  robertson.F90
  )

include_directories(${CMAKE_BINARY_DIR}/src/shr)
include_directories(${CMAKE_BINARY_DIR}/src/io_util)
include_directories(${CMAKE_BINARY_DIR}/src/betr/betr_util)
include_directories(${CMAKE_BINARY_DIR}/src/betr/betr_math)


include(add_betr_library)
add_betr_library(math_test ${MATH_TEST_SOURCES})

#set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -w")

set(BETR_LIBRARIES math_test;${BETR_LIBRARIES} PARENT_SCOPE)
set(BETR_LIBRARIES math_test;${BETR_LIBRARIES})

link_libraries(${BETR_LIBRARIES};${BETR_TPLS})
include(add_betr_executable)
add_betr_executable(mathtest mathtest.F90)
add_betr_executable(robertson robertson.F90)
#X#add_subdirectory(tests)

if (NOT CMAKE_INSTALL_PREFIX STREQUAL "INSTALL_DISABLED")
  install(TARGETS mathtest DESTINATION bin)
  install(TARGETS robertson DESTINATION bin)
  file(GLOB HEADERS *.mod)
  install(FILES ${HEADERS} DESTINATION include/math_test)
endif()
