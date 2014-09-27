# Create a library for household db interfaces
add_library(ork_household_db db_sql_household.cpp
                        db_mesh.cpp
)

target_link_libraries(ork_household_db ${catkin_LIBRARIES})

install(TARGETS ork_household_db
        DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

# create a Python module to wrap the DB functionalities
find_package(PythonLibs)
include_directories(SYSTEM ${PYTHON_INCLUDE_PATH})
add_library(ork_household_db_interface module_python.cpp
                                  wrap_object_db.cpp
)
target_link_libraries(ork_household_db_interface household_db ${catkin_LIBRARIES})

set_target_properties(ork_household_db_interface PROPERTIES
                      LIBRARY_OUTPUT_DIRECTORY ${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_PYTHON_DESTINATION}
                      OUTPUT_NAME db_interface
                      PREFIX ""
)

install(TARGETS ork_household_db_interface
        DESTINATION ${CATKIN_PACKAGE_PYTHON_DESTINATION}
)
