add_library(PositionBasedDynamics
		SHARED
		${PROJECT_SOURCE_DIR}/Common/Common.h

		DirectPositionBasedSolverForStiffRodsInterface.h
		MathFunctions.cpp
		MathFunctions.h
		PositionBasedDynamics.cpp
		PositionBasedDynamics.h
		PositionBasedElasticRods.cpp
		PositionBasedElasticRods.h
		PositionBasedFluids.cpp
		PositionBasedFluids.h
		PositionBasedRigidBodyDynamics.cpp
		PositionBasedRigidBodyDynamics.h
		PositionBasedGenericConstraints.h
		SPHKernels.cpp
		SPHKernels.h
		TimeIntegration.cpp
		TimeIntegration.h
)

find_package(Eigen3 REQUIRED)

target_include_directories(PositionBasedDynamics
	PUBLIC
		${PROJECT_SOURCE_DIR}
)
target_link_libraries(PositionBasedDynamics
	PUBLIC
		Eigen3::Eigen
)




