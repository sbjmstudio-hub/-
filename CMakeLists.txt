cmake_minimum_required(VERSION 3.24)
project(Wirza_Cliant_Native VERSION 3.4.0)

if(NOT WIN32)
  message(FATAL_ERROR "Wirza_Cliant Native is Windows-only.")
endif()
if(NOT CMAKE_SIZEOF_VOID_P EQUAL 8)
  message(FATAL_ERROR "Build x64 only.")
endif()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
foreach(_cfg Debug Release RelWithDebInfo MinSizeRel)
  string(TOUPPER "${_cfg}" _cfg_upper)
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${_cfg_upper} "${CMAKE_BINARY_DIR}/bin")
  set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${_cfg_upper} "${CMAKE_BINARY_DIR}/bin")
  set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${_cfg_upper} "${CMAKE_BINARY_DIR}/lib")
endforeach()

include(FetchContent)
set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)

# Official MinHook repository, pinned to a release tag.
FetchContent_Declare(
  minhook
  GIT_REPOSITORY https://github.com/TsudaKageyu/minhook.git
  GIT_TAG v1.3.4
  GIT_SHALLOW TRUE
)
FetchContent_MakeAvailable(minhook)

# Official Dear ImGui repository. 1.90.9 is pinned because its DX12 backend API
# is stable and intentionally used by this Phase 1 implementation.
FetchContent_Declare(
  imgui_src
  GIT_REPOSITORY https://github.com/ocornut/imgui.git
  GIT_TAG v1.90.9
  GIT_SHALLOW TRUE
)
FetchContent_GetProperties(imgui_src)
if(NOT imgui_src_POPULATED)
  FetchContent_Populate(imgui_src)
endif()

add_library(wirza_imgui STATIC
  ${imgui_src_SOURCE_DIR}/imgui.cpp
  ${imgui_src_SOURCE_DIR}/imgui_draw.cpp
  ${imgui_src_SOURCE_DIR}/imgui_tables.cpp
  ${imgui_src_SOURCE_DIR}/imgui_widgets.cpp
  ${imgui_src_SOURCE_DIR}/backends/imgui_impl_win32.cpp
  ${imgui_src_SOURCE_DIR}/backends/imgui_impl_dx12.cpp
)
target_include_directories(wirza_imgui PUBLIC
  ${imgui_src_SOURCE_DIR}
  ${imgui_src_SOURCE_DIR}/backends
)
target_compile_definitions(wirza_imgui PRIVATE WIN32_LEAN_AND_MEAN NOMINMAX)
target_link_libraries(wirza_imgui PUBLIC d3d12 dxgi)

FetchContent_Declare(
  entt
  GIT_REPOSITORY https://github.com/skypjack/entt.git
  GIT_TAG fe8d7d78c4823e8a66a050bf86f5c6318cf76ce7
  GIT_SHALLOW FALSE
)
FetchContent_MakeAvailable(entt)

add_subdirectory(src/client)
add_subdirectory(src/launcher)

