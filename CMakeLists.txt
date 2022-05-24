cmake_minimum_required(VERSION 3.16)

project(Learning VERSION 0.1 LANGUAGES CXX)

enable_testing()

set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 20)

find_package(Qt6 6.2 COMPONENTS Quick REQUIRED)

qt_add_executable(appLearning
    main.cpp
)

qt_add_qml_module(appLearning
    URI Learning
    VERSION 1.0
    QML_FILES main.qml
    content/TestForm.qml content/Test.qml
    content/Test2.qml
)

set_target_properties(appLearning PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_compile_definitions(appLearning
    PRIVATE $<$<OR:$<CONFIG:Debug>,$<CONFIG:RelWithDebInfo>>:QT_QML_DEBUG>)
target_link_libraries(appLearning
    PRIVATE Qt6::Quick)
