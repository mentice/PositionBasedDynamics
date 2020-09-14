cmake_minimum_required(VERSION 3.15)

project(PositionBasedDynamics)

if (DEFINED PBD_EXTERNALINSTALLDIR)
	set(ExternalInstallDir "${PBD_EXTERNALINSTALLDIR}" CACHE INTERNAL "External install directory")
else()
	set(ExternalInstallDir "${PROJECT_BINARY_DIR}" CACHE INTERNAL "External install directory")
endif()

include(ExternalProject)

add_subdirectory(extern/Discregrid)
add_subdirectory(extern/GenericParameters)
add_subdirectory(PositionBasedDynamics)
add_subdirectory(Utils)
add_subdirectory(Simulation)
