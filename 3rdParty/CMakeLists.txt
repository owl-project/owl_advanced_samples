# ======================================================================== #
# Copyright 2021-2025 Ingo Wald                                            #
#                                                                          #
# Licensed under the Apache License, Version 2.0 (the "License");          #
# you may not use this file except in compliance with the License.         #
# You may obtain a copy of the License at                                  #
#                                                                          #
#     http://www.apache.org/licenses/LICENSE-2.0                           #
#                                                                          #
# Unless required by applicable law or agreed to in writing, software      #
# distributed under the License is distributed on an "AS IS" BASIS,        #
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. #
# See the License for the specific language governing permissions and      #
# limitations under the License.                                           #
# ======================================================================== #

if (NOT (TARGET stb_image))
  add_subdirectory(stb_image)
endif()

find_package(glfw3 QUIET COMPONENTS glfw)
if (TARGET glfw)
  message("glfw found installed on system, using it")
else()
  if (WIN32)
    # for windows, downloading and installing glfw can be a pain, so
    # let's just build it.
    set(OpenGL_GL_PREFERENCE "LEGACY")
    add_subdirectory(glfw-3.4)
  else()
    # for linux, it's easier to just install glfw, so ask user to do
    # so
    message(FATAL_ERROR "Could not find GLFW; please install via apt/yum/etc, or build and install locally")
  endif()
endif()
