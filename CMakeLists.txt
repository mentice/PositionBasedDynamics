cmake_minimum_required(VERSION 3.15)

project(PositionBasedDynamics)

if (DEFINED PBD_EXTERNALINSTALLDIR)
	set(ExternalInstallDir "${PBD_EXTERNALINSTALLDIR}" CACHE INTERNAL "External install directory")
else()
	set(ExternalInstallDir "${PROJECT_BINARY_DIR}" CACHE INTERNAL "External install directory")
endif()

include(ExternalProject)

## Discregrid
if ((DEFINED Discregrid_INCLUDE_DIR) AND (DEFINED Discregrid_DEBUG_LIB) AND (DEFINED Discregrid_LIB))
	message(STATUS "Using ${Discregrid_INCLUDE_DIR}")
	set(Discregrid_LIBRARIES optimized ${Discregrid_LIB} debug ${Discregrid_DEBUG_LIB})
else()
	ExternalProject_Add(
	   Ext_Discregrid
	   PREFIX "${ExternalInstallDir}/Discregrid"
	   GIT_REPOSITORY https://github.com/InteractiveComputerGraphics/Discregrid.git
	   GIT_TAG "0b69062ff9c56fbb6dcecd296652028bedbacf0e"
	   INSTALL_DIR ${ExternalInstallDir}/Discregrid
	   CMAKE_ARGS -DCMAKE_BUILD_TYPE:STRING=${EXT_CMAKE_BUILD_TYPE} -DCMAKE_INSTALL_PREFIX:PATH=${ExternalInstallDir}/Discregrid
	   -DBUILD_AS_SHARED_LIBS:BOOL=0
	   -DBUILD_CMD_EXECUTABLE:BOOL=0 -DEIGEN3_INCLUDE_DIR:PATH=${EIGEN3_INCLUDE_DIR}
	)
	ExternalProject_Get_Property(Ext_Discregrid INSTALL_DIR)
	set(Discregrid_INCLUDE_DIR ${INSTALL_DIR}/include)
	set(Discregrid_LIBRARIES optimized ${INSTALL_DIR}/lib/${CMAKE_STATIC_LIBRARY_PREFIX}Discregrid${CMAKE_STATIC_LIBRARY_SUFFIX}
							 debug ${INSTALL_DIR}/lib/${CMAKE_STATIC_LIBRARY_PREFIX}Discregrid_d${CMAKE_STATIC_LIBRARY_SUFFIX})
	unset(INSTALL_DIR)
	message(STATUS "Building ${Discregrid_INCLUDE_DIR}")
endif()


if (DEFINED GenericParameters_INCLUDE_DIR)
	message(STATUS "Using ${GenericParameters_INCLUDE_DIR}")
else()
	## GenericParameters
	ExternalProject_Add(
	   Ext_GenericParameters
	   PREFIX "${ExternalInstallDir}/GenericParameters"
	   GIT_REPOSITORY https://github.com/InteractiveComputerGraphics/GenericParameters.git
	   GIT_TAG "b1ad669fac8d106515f6aa8514a03598d5766a36"
	   INSTALL_DIR ${ExternalInstallDir}/GenericParameters
	   CMAKE_ARGS -DCMAKE_BUILD_TYPE=${EXT_CMAKE_BUILD_TYPE} -DCMAKE_INSTALL_PREFIX:PATH=${ExternalInstallDir}/GenericParameters -DGENERICPARAMETERS_NO_TESTS:BOOL=1
	)
	ExternalProject_Get_Property(Ext_GenericParameters INSTALL_DIR)
	set(GenericParameters_INCLUDE_DIR ${INSTALL_DIR}/include)
	unset(INSTALL_DIR)
endif()

add_subdirectory(PositionBasedDynamics)
add_subdirectory(Utils)
add_subdirectory(Simulation)
