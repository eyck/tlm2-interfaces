# Copyright 2020 Arteris IP
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.13)
if(POLICY CMP0048)
	cmake_policy(SET CMP0048 NEW)
endif()

project (tlm-interfaces LANGUAGES CXX VERSION 1.0.0)

find_package(SystemCLanguage CONFIG REQUIRED)
set (CMAKE_CXX_STANDARD ${SystemC_CXX_STANDARD})

set(LIB_SOURCES chi/chi_tlm.cpp axi/axi_tlm.cpp)

add_library(tlm-interfaces ${LIB_SOURCES})
target_include_directories (tlm-interfaces PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(tlm-interfaces SystemC::systemc)

set_target_properties(tlm-interfaces PROPERTIES
	  VERSION ${PROJECT_VERSION}
	  FRAMEWORK FALSE
)

install(TARGETS tlm-interfaces
        LIBRARY       DESTINATION lib
        ARCHIVE       DESTINATION lib/static
        PUBLIC_HEADER DESTINATION include/tlm)
