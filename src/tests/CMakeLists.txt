foreach(test_name
  dependency-tree
  ordered-compute
  independent-tasks
)
  if(barename MATCHES caf)
    set(launch_command "cafrun" "-n" "2")
  else()
    set(launch_command "")
  endif()

  add_subdirectory(${test_name})

  add_test(NAME "${test_name}"
    COMMAND ${launch_command} "$<TARGET_FILE:test-${test_name}>"
    WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/${test_name}"
  )
  set_tests_properties(${test_name}
     PROPERTIES PASS_REGULAR_EXPRESSION "Test passed."
  )
endforeach()
