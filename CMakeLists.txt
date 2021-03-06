cmake_minimum_required(VERSION 2.8)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")
set(CMAKE_INSTALL_PREFIX "/usr")
FIND_PACKAGE( Boost 1.40 COMPONENTS program_options serialization REQUIRED )
FIND_PACKAGE( pcap REQUIRED )
FIND_PACKAGE( openssl REQUIRED)
INCLUDE_DIRECTORIES( ${pcap_INCLUDE_DIRS} )
INCLUDE_DIRECTORIES( ${Boost_INCLUDE_DIR} )
INCLUDE_DIRECTORIES( ${OpenSSL_INCLUDE_DIR} )

ADD_EXECUTABLE( btfinder  driver.cpp )
ADD_SUBDIRECTORY(pcap_parser)
ADD_SUBDIRECTORY(file_reconstituter)
TARGET_LINK_LIBRARIES( btfinder ${Boost_LIBRARIES} pcap_parser file_reconstituter ${PCAP_LIBRARIES} ${OpenSSL_LIBRARIES})

INSTALL(TARGETS btfinder DESTINATION bin)

