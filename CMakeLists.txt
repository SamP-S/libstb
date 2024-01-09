cmake_minimum_required(VERSION 3.9)

project(libstb  VERSION 1.0.0 
                DESCRIPTION "set of single file C/C++ libraries"
                LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD          17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS        OFF)

set(STB_TARGETS "stb_image;stb_image_write;stb_image_resize;stb_perlin;stb_truetype")
set(STB_FILES "stb_image.h;stb_image_write.h;stb_image_resize2.h;stb_perlin.h;stb_truetype.h")
set(STB_DEFINES "STB_IMAGE_IMPLEMENTATION;STB_IMAGE_WRITE_IMPLEMENTATION;STB_IMAGE_RESIZE_IMPLEMENTATION;STB_PERLIN_IMPLEMENTATION;STB_TRUETYPE_IMPLEMENTATION")
list(LENGTH STB_TARGETS STB_COUNT)
math(EXPR STB_COUNT "${STB_COUNT} - 1")

foreach(I RANGE 0 ${STB_COUNT})
    list(GET STB_TARGETS ${I} STB_TARGET)
    list(GET STB_FILES ${I} STB_FILE)
    list(GET STB_DEFINES ${I} STB_DEFINE)

    add_library(${STB_TARGET} STATIC ${STB_FILE})
    target_include_directories(${STB_TARGET} PUBLIC "./")
    set_target_properties(${STB_TARGET} PROPERTIES LINKER_LANGUAGE CXX)
    target_compile_definitions(${STB_TARGET} PUBLIC ${STB_DEFINE})
    target_link_libraries(${STB_TARGET} m)     # link math.h
endforeach()