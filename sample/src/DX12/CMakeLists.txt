# CAS Sample
#
# Copyright (c) 2019 Advanced Micro Devices, Inc. All rights reserved.
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
# THE SOFTWARE.

project (CAS_Sample_DX12)

include(${CMAKE_CURRENT_SOURCE_DIR}/../../common.cmake)

set(sources
    CAS_CS.cpp
    CAS_CS.h
    CAS_Sample.cpp
    CAS_Sample.h
    CAS_Renderer.cpp
    CAS_Renderer.h
    stdafx.cpp
    stdafx.h)

set(Shaders_src
    ${CMAKE_CURRENT_SOURCE_DIR}/CAS_Shader.hlsl
    ${CMAKE_CURRENT_SOURCE_DIR}/CAS_RenderPS.hlsl
    ${CMAKE_CURRENT_SOURCE_DIR}/../../../ffx-cas/ffx_a.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../../../ffx-cas/ffx_cas.h)

source_group("sources" FILES ${sources})
source_group("shaders" FILES ${Shaders_src})

copyCommand("${Shaders_src}" ${CMAKE_HOME_DIRECTORY}/bin/ShaderLibDX)

add_executable(${PROJECT_NAME} WIN32 ${sources} ${Shaders_src})
target_link_libraries (${PROJECT_NAME} LINK_PUBLIC Cauldron_DX12 ImGUI amd_ags DXC d3dcompiler D3D12)
target_include_directories (${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../../../ffx-cas)

set_target_properties(${PROJECT_NAME} PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_HOME_DIRECTORY}/bin")
set_source_files_properties(${Shaders_src} PROPERTIES VS_TOOL_OVERRIDE "Text")
addManifest(${PROJECT_NAME})

