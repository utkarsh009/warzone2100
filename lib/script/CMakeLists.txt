cmake_minimum_required (VERSION 3.5)
project (script CXX)

if(ENABLE_NLS)
	find_package (Intl REQUIRED)
endif()

file(GLOB HEADERS "*.h")
file(GLOB SRC "*.cpp")

add_library(script STATIC ${HEADERS} ${SRC})
target_link_libraries(script PRIVATE framework)
if(ENABLE_NLS)
	target_include_directories(script PRIVATE "${Intl_INCLUDE_DIRS}")
	target_link_libraries(script PRIVATE ${Intl_LIBRARIES})
endif()
target_compile_definitions(script PRIVATE "YY_NO_UNISTD_H")
