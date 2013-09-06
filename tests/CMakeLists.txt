# Include Eigen
IF (DEFINED ENV{EIGEN_INC})
    SET(EIGEN_BASE $ENV{EIGEN_INC}/eigen3)
ELSE (DEFINED ENV{EIGEN_INC})
    SET(EIGEN_BASE "/opt/local/include/eigen3")
ENDIF (DEFINED ENV{EIGEN_INC})
INCLUDE_DIRECTORIES("/opt/local/include")
INCLUDE_DIRECTORIES(${EIGEN_BASE})
INCLUDE_DIRECTORIES(${EIGEN_BASE}/Eigen)
INCLUDE_DIRECTORIES(${EIGEN_BASE}/unsupported)
ADD_DEFINITIONS(-DEIGEN_YES_I_KNOW_SPARSE_MODULE_IS_NOT_STABLE_YET)

# Enumerate source files
SET(SRC_FILES example.cpp)

# Include headers
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/src)

# Add executable and library
ADD_EXECUTABLE(example EXCLUDE_FROM_ALL ${SRC_FILES})
TARGET_LINK_LIBRARIES(example mesh)

# Bundle all target under the name test.
# To build all tests, just "make tests"
ADD_CUSTOM_TARGET(tests DEPENDS example)