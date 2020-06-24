if (POLICY CMP0048)
  cmake_policy(SET CMP0048 NEW)
endif (POLICY CMP0048)

project(SMTPEmail VERSION 1.1.0 LANGUAGES CXX)

cmake_minimum_required(VERSION 3.16.0)
SET(CMAKE_COLOR_MAKEFILE ON)
#SET(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_AUTOMOC ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)


find_package( Qt5 REQUIRED COMPONENTS Core Network )


include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
    ${Boost_INCLUDE_DIRS}
)

set(HEADERS
    src/emailaddress.h
    src/mimeattachment.h
    src/mimefile.h
    src/mimehtml.h
    src/mimeinlinefile.h
    src/mimemessage.h
    src/mimepart.h
    src/mimetext.h
    src/smtpclient.h
    src/SmtpMime
    src/quotedprintable.h
    src/mimemultipart.h
    src/mimecontentformatter.h
    src/smtpexports.h
)

set(SOURCES
    src/emailaddress.cpp
    src/mimeattachment.cpp
    src/mimefile.cpp
    src/mimehtml.cpp
    src/mimeinlinefile.cpp
    src/mimemessage.cpp
    src/mimepart.cpp
    src/mimetext.cpp
    src/smtpclient.cpp
    src/quotedprintable.cpp
    src/mimemultipart.cpp
    src/mimecontentformatter.cpp
)


add_definitions(
	-DSMTP_BUILD
)

add_library(${PROJECT_NAME} SHARED ${SOURCES} ${HEADERS})
target_link_libraries(${PROJECT_NAME}
	 PUBLIC Qt5::Core Qt5::Network)

set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER Libraries/QtC5Extended)

target_include_directories(${PROJECT_NAME} PUBLIC src)

include(CMakePackageConfigHelpers)
write_basic_package_version_file( ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake VERSION ${PROJECT_VERSION} COMPATIBILITY SameMajorVersion)
