project(ZAVTVimbaCamera LANGUAGES CXX)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${Z3D_OUTPUT_DIRECTORY}/plugins/cameraacquisition)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${Z3D_OUTPUT_DIRECTORY}/plugins/cameraacquisition)

find_package(Qt5 COMPONENTS Core REQUIRED)
find_package(OpenCV REQUIRED)
find_package(Vimba REQUIRED)

file(GLOB HEADER_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/*.h)

file(GLOB SRC_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

file(GLOB METADATA_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/*.json)

add_library(${PROJECT_NAME} SHARED
    ${HEADER_FILES}
    ${SRC_FILES}
    ${METADATA_FILES}
)

target_include_directories(${PROJECT_NAME} PRIVATE ${VIMBA_INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME}
    PRIVATE
        Qt5::Core
        ${OpenCV_LIBS}
        ${VIMBA_LIBRARIES}
        ZCameraAcquisition
)
