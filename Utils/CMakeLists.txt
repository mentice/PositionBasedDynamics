
add_library(Utils
		FileSystem.h
		Hashmap.h
		IndexedFaceMesh.cpp
		IndexedFaceMesh.h
		IndexedTetMesh.cpp
		IndexedTetMesh.h
		Logger.h
		OBJLoader.h
		SceneLoader.cpp
		SceneLoader.h
		StringTools.h
		SystemInfo.h
		TetGenLoader.cpp
		TetGenLoader.h
		Timing.h
		Version.h
		VolumeIntegration.cpp
		VolumeIntegration.h

		CMakeLists.txt
)

target_include_directories(Utils
	PUBLIC
		${GenericParameters_INCLUDE_DIR}
)

find_package( Eigen3 REQUIRED )

target_link_libraries(Utils
	PUBLIC
		PositionBasedDynamics
		Eigen3::Eigen
		GenericParameters
)

install(TARGETS Utils
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)

install(DIRECTORY .
DESTINATION include/Utils
FILES_MATCHING PATTERN "*.h")




