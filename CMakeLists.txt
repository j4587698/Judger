cmake_minimum_required(VERSION 2.8)
project(judger C)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/output)

set(CMAKE_C_FLAGS "-g -Wall -Werror -O3 -std=c99 -fPIC -fvisibility=default")

# 创建共享库的正确方式
file(GLOB SOURCE "src/*.c" "src/rules/*.c")
add_library(judger SHARED ${SOURCE})
target_link_libraries(judger pthread seccomp)

# 设置正确的共享库命名
set_target_properties(judger PROPERTIES OUTPUT_NAME "judger")

# 安装配置
install(TARGETS judger
        LIBRARY
        PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
        DESTINATION /usr/lib/judger)
