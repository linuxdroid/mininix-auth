cmake_minimum_required(VERSION 3.2)
project(mininix-auth VERSION 0.1)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")
include_directories(${PROJECT_SOURCE_DIR})

find_library(LIB_CRYPTO crypto)

add_library(mininix-auth SHARED mininix-auth.c)
target_link_libraries(mininix-auth ${LIB_CRYPTO})
install(TARGETS mininix-auth DESTINATION lib)
install(FILES ${PROJECT_SOURCE_DIR}/mininix-auth.h DESTINATION include)

add_executable(passwd passwd.c)
target_link_libraries(passwd mininix-auth)
install(TARGETS passwd DESTINATION bin)

add_executable(testauth testauth.c)
target_link_libraries(testauth mininix-auth)
