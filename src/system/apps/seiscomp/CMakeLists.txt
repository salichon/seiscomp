INSTALL(PROGRAMS seiscomp-control.py DESTINATION ${SC3_PACKAGE_BIN_DIR})

# create wrapper scripts
EXECUTE_PROCESS(
	COMMAND ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/py-wrapper ${PYTHON_EXECUTABLE} ${CMAKE_INSTALL_PREFIX}
	WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)
INSTALL(
	FILES
		${CMAKE_CURRENT_BINARY_DIR}/seiscomp
		${CMAKE_CURRENT_BINARY_DIR}/seiscomp-python
	DESTINATION bin
	PERMISSIONS
		OWNER_EXECUTE OWNER_READ OWNER_WRITE
		GROUP_EXECUTE GROUP_READ
		WORLD_EXECUTE WORLD_READ
)

SC_INSTALL_INIT(kernel kernel.py)

INSTALL(DIRECTORY share/deps DESTINATION ${SC3_PACKAGE_SHARE_DIR}
        PATTERN ".svn" EXCLUDE
        PATTERN "CMakeLists.txt" EXCLUDE)
INSTALL(DIRECTORY share/shell-completion DESTINATION ${SC3_PACKAGE_SHARE_DIR}
        PATTERN ".svn" EXCLUDE
        PATTERN "CMakeLists.txt" EXCLUDE)

