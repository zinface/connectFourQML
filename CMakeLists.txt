cmake_minimum_required(VERSION 3.5.1)

project(connectFourQML LANGUAGES CXX VERSION 0.0.1)

include(cmake/SparkWithGit.cmake)

spark_initialize_modules()

spark_add_links_qt5(Qml Quick WebEngine)

# 资源文件路径
set(QRC_SOURCES "startup.qrc")

spark_add_executable_path(${PROJECT_NAME} .
    ${QRC_SOURCES}
)
target_link_qt(${PROJECT_NAME})
target_link_qt_qml(${PROJECT_NAME})
target_link_qt_quick(${PROJECT_NAME})

# include(cmake/SparkBuildGraphviz.cmake)


# include(cmake/SparkDesktopMacros.cmake)
# # 内容默认应用名称: Name= 应与项目名称相同
spark_desktop_macros(
    # 应用名称: Name=
    ${PROJECT_NAME}
    # 应用名称: Name[zh_CN]=
    "四连棋"
    # 应用说明: Comment=
    ""
    # 应用类型: Type=
    "Application"
    # 执行程序: Exec=
    "/usr/bin/${PROJECT_NAME}"
    # 图标路径: Icon=
    "connectFourQML"
    # 应用分类: Category=
    "Utility"
)

# # install, 
install(TARGETS ${PROJECT_NAME}
    DESTINATION /usr/bin)

install(FILES ${SPARK_DESKTOP_FILE}
    DESTINATION /usr/share/applications)

install(FILES icon.png
    DESTINATION /usr/share/icons/hicolor/512x512/apps
    RENAME connectFourQML.png)


# include(cmake/SparkBuildGraphviz.cmake)

# find_package(DebPackage PATHS ${CMAKE_SOURCE_DIR})
set(CPACK_DEBIAN_PACKAGE_SHLIBDEPS ON)
add_package_descript(cmake/spark-deb-package.descript)