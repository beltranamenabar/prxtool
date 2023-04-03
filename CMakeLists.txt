cmake_minimum_required(VERSION 3.12..3.26)

project(prxtool
    VERSION 1.1
    DESCRIPTION "A tool for manipulating PRX files"
    LANGUAGES CXX
)

add_subdirectory(tinyxml2)
find_package(tinyxml2 REQUIRED)

set(prxtool_SOURCES
    main.C
    ProcessElf.C
    ProcessPrx.C
    NidMgr.C
    VirtualMem.C
    output.C
    SerializePrx.C
    SerializePrxToIdc.C
    SerializePrxToXml.C
    SerializePrxToMap.C
    pspkerror.C
    disasm.C
    getargs.C
)

# append src/ to the source files
list(TRANSFORM prxtool_SOURCES PREPEND src/)

add_executable(${PROJECT_NAME} ${prxtool_SOURCES})
# add the version as a PRXTOOL_VERSION macro
target_compile_definitions(${PROJECT_NAME} PRIVATE PRXTOOL_VERSION="${CMAKE_PROJECT_VERSION}")
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(${PROJECT_NAME} PRIVATE tinyxml2::tinyxml2)

