cmake_minimum_required(VERSION 2.8)
project(object_recognition_household)

find_package(catkin REQUIRED ecto cmake_modules household_objects_database object_recognition_core
                             pluginlib sql_database tf)
catkin_package(INCLUDE_DIRS include)

set(CMAKE_INCLUDE_DIRECTORIES_PROJECT_BEFORE 1)

# include some directories
include_directories(${catkin_INCLUDE_DIRS}
  include
)

add_subdirectory(src)

# add the tests
add_subdirectory(test)

# add the docs
catkin_doxygen(object_recognition_household-doxygen ${CMAKE_CURRENT_SOURCE_DIR}/include)
ecto_sphinx(${CMAKE_CURRENT_SOURCE_DIR}/doc/source doc)

# install the configuration files
install(DIRECTORY ${PROJECT_SOURCE_DIR}/conf
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

# install the include folder
install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/object_recognition_tabletop/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

# install the plugin file
install(FILES ${PROJECT_SOURCE_DIR}/db_plugin.xml
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
