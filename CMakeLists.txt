cmake_minimum_required(VERSION 3.16)
project(bpf_asm C)

find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)

bison_target(bpf_exp_y src/bpf_exp.y ${CMAKE_CURRENT_BINARY_DIR}/bpf_exp.y.c DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/bpf_exp.y.h)
flex_target(bpf_exp_l src/bpf_exp.l ${CMAKE_CURRENT_BINARY_DIR}/bpf_exp.l.c)
add_flex_bison_dependency(bpf_exp_l bpf_exp_y)

add_executable(bpf_asm src/bpf_asm.c ${CMAKE_CURRENT_BINARY_DIR}/bpf_exp.y.c ${CMAKE_CURRENT_BINARY_DIR}/bpf_exp.l.c)
target_include_directories(bpf_asm PRIVATE src ${CMAKE_CURRENT_BINARY_DIR})
