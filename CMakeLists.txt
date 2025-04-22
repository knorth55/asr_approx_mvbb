cmake_minimum_required(VERSION 2.8.3)
project(asr_approx_mvbb)

add_definitions(-std=gnu++11)


find_package(catkin REQUIRED COMPONENTS)
find_package(cmake_modules REQUIRED)

#find Eigen (depends on ros distro):
find_package(Eigen3)
if(NOT EIGEN3_FOUND)
  find_package(Eigen REQUIRED)
  set(EIGEN3_INCLUDE_DIRS ${EIGEN_INCLUDE_DIRS})
  set(EIGEN3_LIBRARIES ${EIGEN_LIBRARIES}) 
else()
  set(EIGEN3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})
endif()

catkin_package(
  INCLUDE_DIRS include external/Diameter/include external/GeometryPredicates/include ${EIGEN3_INCLUDE_DIRS}
  LIBRARIES ApproxMVBB
)


include_directories(
  include
  ${EIGEN3_INCLUDE_DIRS}
  external/Diameter/include
  external/GeometryPredicates/include
  ${catkin_INCLUDE_DIRS}
)


 add_library(ApproxMVBB
#   src/${PROJECT_NAME}/ComputeApproxMVBB.cpp
   src/ApproxMVBB/AABB.cpp
   src/ApproxMVBB/ConvexHull2D.cpp
   src/ApproxMVBB/MinAreaRectangle.cpp
   src/ApproxMVBB/OOBB.cpp
   src/ApproxMVBB/ProjectedPointSet.cpp
   src/ApproxMVBB/RandomGenerators.cpp
   src/ApproxMVBB/Common/MyMatrixTypeDefs.cpp
   external/Diameter/src/alloc.cpp
   external/Diameter/src/EstimateDiameter.cpp
   external/Diameter/src/rand.cpp
   external/Diameter/src/util.cpp
   external/GeometryPredicates/src/Predicates.cpp
   external/GeometryPredicates/src/PredicatesInit.cpp
 )



 install(TARGETS ApproxMVBB #ApproxMVBB_node
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
 )


 install(DIRECTORY include/ApproxMVBB/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.hpp"

 )

