cmake_minimum_required(VERSION 2.8.3)
project(asr_approx_mvbb)

add_definitions(-std=gnu++11)

find_package(catkin REQUIRED COMPONENTS)
find_package(cmake_modules REQUIRED)
find_package(Eigen3)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
)

include_directories(
  include
  ${EIGEN3_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
)

add_library(${PROJECT_NAME}
  src/ApproxMVBB/AABB.cpp
  src/ApproxMVBB/ConvexHull2D.cpp
  src/ApproxMVBB/MinAreaRectangle.cpp
  src/ApproxMVBB/OOBB.cpp
  src/ApproxMVBB/ProjectedPointSet.cpp
  src/ApproxMVBB/RandomGenerators.cpp
  src/ApproxMVBB/Common/MyMatrixTypeDefs.cpp
  src/Diameter/alloc.cpp
  src/Diameter/EstimateDiameter.cpp
  src/Diameter/rand.cpp
  src/Diameter/util.cpp
  src/GeometryPredicates/Predicates.cpp
  src/GeometryPredicates/PredicatesInit.cpp
)

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
)
