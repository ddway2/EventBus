# http://www.levelofindirection.com/journal/2010/12/28/unit-testing-in-c-and-objective-c-just-got-easier.html
# Thanks for CATCH!

ADD_EXECUTABLE(EventBusTest
		eventbus/EventCollectorTest.cpp
		eventbus/NotifierTest.cpp
		)

SET_TARGET_PROPERTIES(EventBusTest PROPERTIES
		CXX_STANDARD 14
		CXX_STANDARD_REQUIRED YES
		)

TARGET_COMPILE_OPTIONS(EventBusTest PUBLIC
		-Wall -pedantic
		-Wno-unused-private-field
		-Wnon-virtual-dtor
		-Wno-gnu
		-Werror
		)

SET(EVENTBUS_DEBUG_FLAGS
		-O0 -fno-inline
		-DDEBUG
		-D_GLIBCXX_DEBUG -D_GLIBCXX_DEBUG_PEDANTIC
		)

SET(EVENTBUS_RELEASE_FLAGS
		-DNDEBUG
		)

TARGET_COMPILE_OPTIONS(EventBusTest PUBLIC "$<$<CONFIG:DEBUG>:${EVENTBUS_DEBUG_FLAGS}>")
TARGET_COMPILE_OPTIONS(EventBusTest PUBLIC "$<$<CONFIG:RELEASE>:${EVENTBUS_RELEASE_FLAGS}>")


TARGET_INCLUDE_DIRECTORIES(EventBusTest PUBLIC Catch/single_include/)
TARGET_LINK_LIBRARIES(EventBusTest PUBLIC Dexode::EventBus)

