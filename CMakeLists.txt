cmake_minimum_required( VERSION 3.5 )

project( mongoApp )
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
aux_source_directory(. DIR_SOURCE)

#find_package(libbsoncxx-static REQUIRED)
#message("Found bsoncxx include: 1+++++++++++++${LIBBSONCXX_STATIC_INCLUDE_DIRS}")
#message("Found bsoncxx include: 2+++++++++++++${LIBBSONCXX_STATIC_LIBRARIES}")
#include_directories(${LIBBSONCXX_STATIC_INCLUDE_DIRS})
#link_directories(${LIBBSONCXX_STATIC_LIBRARIES})


#find_package(libbsoncxx-static REQUIRED)

message("Found mongocxx inclue: 1-------------${LIBBSONCXX_STATIC_INCLUDE_DIRS}")
message("Found msoncxx include: 2-------------${LIBBSONCXX_STATIC_LIBRARIES}")
#include_directories(${LIBBSONCXX_STATIC_INCLUDE_DIRS})
#link_directories(${LIBMONGOCXX_LIBRARIES})

add_executable(mongo_db_plugin ${DIR_SOURCE})

#target_include_directories(mongoApp PRIVATE ${LIBMONGOCXX_STATIC_INCLUDE_DIRS} ${LIBBSONCXX_STATIC_INCLUDE_DIRS})
#target_compile_definitions(mongoApp PRIVATE ${LIBMONGOCXX_STATIC_DEFINITIONS} ${LIBBSONCXX_STATIC_DEFINITIONS})
#target_link_libraries(mongo_db_plugin PUBLIC ${EOS_LIBMONGOCXX} ${EOS_LIBBSONCXX})
#find_package(libmongoc-1.0 1.8)

find_package(libbsoncxx-static REQUIRED)
message(STATUS "Found bsoncxx headers: ${LIBBSONCXX_STATIC_INCLUDE_DIRS}")

# mongo-cxx-driver 3.2 release altered LIBBSONCXX_LIBRARIES semantics. Instead of library names,
#  it now hold library paths.
#if((LIBBSONCXX_STATIC_VERSION_MAJOR LESS 3) OR ((LIBBSONCXX_STATIC_VERSION_MAJOR EQUAL 3) AND (LIBBSONCXX_STATIC_VERSION_MINOR LESS 2)))
 # find_library(EOS_LIBBSONCXX ${LIBBSONCXX_STATIC_LIBRARIES}
  #  PATHS ${LIBBSONCXX_STATIC_LIBRARY_DIRS} NO_DEFAULT_PATH)
#else()
set(EOS_LIBBSONCXX ${LIBBSONCXX_STATIC_LIBRARIES})
#endif()

message(STATUS "Found bsoncxx library: ${EOS_LIBBSONCXX}")

find_package(libmongocxx-static REQUIRED)
message(STATUS "Found mongocxx headers: ${LIBMONGOCXX_STATIC_INCLUDE_DIRS}")

# mongo-cxx-driver 3.2 release altered LIBBSONCXX_LIBRARIES semantics. Instead of library names,
#  it now hold library paths.
#if((LIBMONGOCXX_STATIC_VERSION_MAJOR LESS 3) OR ((LIBMONGOCXX_STATIC_VERSION_MAJOR EQUAL 3) AND (LIBMONGOCXX_STATIC_VERSION_MINOR LESS 2)))
 # find_library(EOS_LIBMONGOCXX ${LIBMONGOCXX_STATIC_LIBRARIES}
  #  PATHS ${LIBMONGOCXX_STATIC_LIBRARY_DIRS} NO_DEFAULT_PATH)
#else()
set(EOS_LIBMONGOCXX ${LIBMONGOCXX_STATIC_LIBRARIES})
#endif()

message(STATUS "Found mongocxx library: ${EOS_LIBMONGOCXX}")
  
target_include_directories(mongo_db_plugin
          PRIVATE ${LIBMONGOCXX_STATIC_INCLUDE_DIRS} ${LIBBSONCXX_STATIC_INCLUDE_DIRS}
          )
          #PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include"

#target_compile_definitions(mongo_db_plugin
 #   PRIVATE ${LIBMONGOCXX_STATIC_DEFINITIONS} ${LIBBSONCXX_STATIC_DEFINITIONS}
  #  )

target_link_libraries(mongo_db_plugin
PRIVATE ${EOS_LIBMONGOCXX} ${EOS_LIBBSONCXX}
          )
          #PUBLIC ${EOS_LIBMONGOCXX} ${EOS_LIBBSONCXX}




