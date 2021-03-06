if(NOT ENABLE_QT)
  message("Qt frontend is disabled, not building cmodview.")
  return()
endif()

if(APPLE AND EXISTS /usr/local/opt/qt5)
  # Homebrew installs Qt5 (up to at least 5.9.1) in
  # /usr/local/qt5, ensure it can be found by CMake since
  # it is not in the default /usr/local prefix.
  list(APPEND CMAKE_PREFIX_PATH "/usr/local/opt/qt5")
endif()

set(QT_LIBS Widgets OpenGL)
find_package(Qt5 COMPONENTS ${QT_LIBS} CONFIG REQUIRED)

# Instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)
# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

build_cmod_tool(cmodview WIN32 cmodview.cpp glframebuffer.cpp  glshader.cpp  mainwindow.cpp  materialwidget.cpp  modelviewwidget.cpp glsupport.cpp)
qt5_use_modules(cmodview ${QT_LIBS})
