# The name of the project to build
PROJECT(MMFF94)

# Set BALL specific includes and compilerflags
ADD_DEFINITIONS(${BALL_ADD_CXXFLAGS})

# add MMFF94 targets
SET(MMFF94_EXECUTABLES
        compareForces
        readMMFF94TestFile
        splitMMFFTestSuiteMolFiles
        splitMMFFTestSuiteOptiFiles
        testKekulizer
)

FOREACH(i ${MMFF94_EXECUTABLES})
        ADD_EXECUTABLE(${i} ${i}.C)
        TARGET_LINK_LIBRARIES(${i} BALL Qt5::Core)
        SET_PROPERTY(TARGET ${i} PROPERTY FOLDER UTILITIES)
        SET_TARGET_PROPERTIES(${i} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/MMFF94")
ENDFOREACH(i)

### add filenames to Visual Studio solution
SET(MMFF94_SOURCES)
FOREACH(i ${MMFF94_EXECUTABLES})
	LIST(APPEND MMFF94_SOURCES "${i}")
ENDFOREACH(i)
SOURCE_GROUP("" FILES ${MMFF94_SOURCES})
