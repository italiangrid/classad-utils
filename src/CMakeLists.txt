#
#  Copyright (c) Members of the EGEE Collaboration. 2010.
#  See http://www.eu-egee.org/partners/ for details on the copyright
#  holders.
#  
#  Licensed under the Apache License, Version 2.0 (the "License");
#  you may not use this file except in compliance with the License.
#  You may obtain a copy of the License at
#  
#     http://www.apache.org/licenses/LICENSE-2.0
#  
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
#  implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.
#  

set(CMAKE_CXX_FLAGS_DEBUG "-g -Wall")

find_package(GLiteClassAd REQUIRED)

if( ${CMAKE_VERSION} VERSION_LESS "2.8.2" )
    if( IS_DIRECTORY "/usr/lib64" )
        set(LIBSUBDIR "lib64")
    else( IS_DIRECTORY "/usr/lib64" )
        set(LIBSUBDIR "lib")
    endif( IS_DIRECTORY "/usr/lib64" )
else( ${CMAKE_VERSION} VERSION_LESS "2.8.2" )
    if( IS_DIRECTORY "/usr/lib64" AND NOT IS_SYMLINK "/usr/lib64" )
        set(LIBSUBDIR "lib64")
    else( IS_DIRECTORY "/usr/lib64" AND NOT IS_SYMLINK "/usr/lib64" )
        set(LIBSUBDIR "lib")
    endif( IS_DIRECTORY "/usr/lib64" AND NOT IS_SYMLINK "/usr/lib64" )
endif( ${CMAKE_VERSION} VERSION_LESS "2.8.2" )

link_directories(${ClassAd_LIBRARY})

include_directories(${ClassAd_INCLUDE_DIR}
                    ${PROJECT_SOURCE_DIR}/interface)

add_definitions( ${ClassAd_CXX_FLAGS} ${ClassAd_CPP_FLAGS} )

add_library(glite_wmsutils_classads SHARED classad_utils.cpp)

set_target_properties(glite_wmsutils_classads PROPERTIES VERSION 0.0.0 SOVERSION 0)

target_link_libraries(glite_wmsutils_classads ${ClassAd_LIBRARY})

install(TARGETS glite_wmsutils_classads
        LIBRARY DESTINATION usr/${LIBSUBDIR})


add_subdirectory(pkgconfig)

