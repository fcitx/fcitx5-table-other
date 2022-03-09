cmake_minimum_required(VERSION 3.8)
project(fcitx-table-other VERSION 5.0.8)

find_package(ECM 1.0 REQUIRED)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

include(FeatureSummary)
include(GNUInstallDirs)
include(ECMUninstallTarget)

find_package(Gettext REQUIRED)
find_package(LibIMETable REQUIRED)
find_package(Fcitx5Utils REQUIRED)

option(ENABLE_DEPRECATED Off "Enable deprecated table")

add_subdirectory(icons)
add_subdirectory(tables)

fcitx5_translate_desktop_file(org.fcitx.Fcitx5.Addon.TableOther.metainfo.xml.in
    org.fcitx.Fcitx5.Addon.TableOther.metainfo.xml XML)

install(FILES "${CMAKE_CURRENT_BINARY_DIR}/org.fcitx.Fcitx5.Addon.TableOther.metainfo.xml" DESTINATION ${CMAKE_INSTALL_DATADIR}/metainfo)

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)
