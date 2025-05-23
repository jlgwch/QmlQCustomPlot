cmake_minimum_required(VERSION 3.14)

project(QmlCustomPlot VERSION 0.1 LANGUAGES CXX C)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_definitions(
    -DQCUSTOMPLOT_USE_OPENGL
)

link_directories(
    thirdparty/fftw/lib
)

link_libraries(
    libfftw3-3
    libfftw3f-3
    libfftw3l-3
)

set(PROJECT_SOURCES
    main.cpp
    thirdparty/qcustomplot/qcustomplot.h
    thirdparty/qcustomplot/qcustomplot.cpp
    thirdparty/fftw/include/fftw3.h
    qquickitem/timedomainplot.cpp
    qquickitem/timedomainplot.h
    qquickitem/audiowaveform.cpp
    qquickitem/audiowaveform.h
    qquickitem/spectrum.cpp
    qquickitem/spectrum.h
    qquickitem/qabstractplot.h
    qquickitem/qabstractplot.cpp
    qquickitem/spectrumplot.h
    qquickitem/spectrumplot.cpp
    qquickitem/waveformplot.h
    qquickitem/waveformplot.cpp
)

set(PROJECT_RESOURCES
    resources/qml.qrc
    resources/audio.qrc
    resources/conf.qrc
    resources/other.qrc
)

link_libraries(
    opengl32
    glu32
)

add_executable(QmlCustomPlot
    ${PROJECT_SOURCES}
    ${PROJECT_RESOURCES}
)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core Quick Widgets PrintSupport OpenGL Multimedia)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Quick Widgets PrintSupport OpenGL Multimedia)

target_link_libraries(QmlCustomPlot
    PRIVATE
    Qt${QT_VERSION_MAJOR}::Core
    Qt${QT_VERSION_MAJOR}::Quick
    Qt${QT_VERSION_MAJOR}::Widgets
    Qt${QT_VERSION_MAJOR}::PrintSupport
    Qt${QT_VERSION_MAJOR}::OpenGL ${OPENGL_gl_LIBRARY}
    Qt${QT_VERSION_MAJOR}::Multimedia
)

set_target_properties(QmlCustomPlot PROPERTIES
    WIN32_EXECUTABLE TRUE
)
