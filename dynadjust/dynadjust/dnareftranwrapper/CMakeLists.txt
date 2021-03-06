# <dnareftranwrapper/...> build rules
project (dnareftranwrapper)

# build dnareftran library first
add_subdirectory (${CMAKE_SOURCE_DIR}/dynadjust/dnareftran ${CMAKE_BINARY_DIR}/dynadjust/dnareftran)

add_definitions (-DBUILD_REFTRAN_EXE)

set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -ggdb -Wall -O0")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O2")

include_directories (${PROJECT_SOURCE_DIR})

add_executable (${PROJECT_NAME}
                ${CMAKE_SOURCE_DIR}/include/config/dnaprojectfile.cpp
                ${CMAKE_SOURCE_DIR}/include/functions/dnastringfuncs.cpp
                dnareftranwrapper.cpp)

target_link_libraries (${PROJECT_NAME} dnareftran ${DNA_LIBRARIES})

set_target_properties (${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${DNA_PROGRAM_PREFIX}reftran")

install (TARGETS ${PROJECT_NAME} DESTINATION bin)
