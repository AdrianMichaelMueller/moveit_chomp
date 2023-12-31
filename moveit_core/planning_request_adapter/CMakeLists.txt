set(MOVEIT_LIB_NAME moveit_planning_request_adapter)

add_library(${MOVEIT_LIB_NAME} src/planning_request_adapter.cpp)
set_target_properties(${MOVEIT_LIB_NAME} PROPERTIES VERSION "${${PROJECT_NAME}_VERSION}")

target_link_libraries(${MOVEIT_LIB_NAME} moveit_planning_scene ${catkin_LIBRARIES} ${urdfdom_LIBRARIES} ${urdfdom_headers_LIBRARIES} ${Boost_LIBRARIES})
add_dependencies(${MOVEIT_LIB_NAME} ${catkin_EXPORTED_TARGETS})

install(TARGETS ${MOVEIT_LIB_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION})

install(DIRECTORY include/ DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION})

if(CATKIN_ENABLE_TESTING)
    catkin_add_gtest(test_planning_request_adapter_chain test/test_planning_request_adapter_chain.cpp)
    target_link_libraries(test_planning_request_adapter_chain
        moveit_test_utils
        moveit_planning_interface
        ${MOVEIT_LIB_NAME})
endif()
