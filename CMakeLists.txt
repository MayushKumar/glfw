project(GLFW)

set(SrcFiles
  "include/GLFW/glfw3.h"
  "include/GLFW/glfw3native.h"
  "src/glfw_config.h"
  "src/context.c"
  "src/init.c"
  "src/input.c"
  "src/monitor.c"
  "src/vulkan.c"
  "src/window.c"
  )

if (WIN32)
  #TODO: Make sure that the latest SDK is used.
  list(APPEND SrcFiles
	"src/win32_init.c"
	"src/win32_joystick.c"
	"src/win32_monitor.c"
	"src/win32_thread.c"
	"src/win32_time.c"
	"src/win32_window.c"
	"src/wgl_context.c"
	"src/egl_context.c"
	"src/osmesa_context.c"
	)

  add_definitions(
	-D_GLFW_WIN32
	)
endif()

if (UNIX)
  list(APPEND SrcFiles
	"src/x11_init.c"
	"src/linux_joystick.c"
	"src/x11_monitor.c"
	"src/x11_window.c"
	"src/xkb_unicode.c"
	"src/posix_time.c"
	"src/posix_thread.c"
	"src/glx_context.c"
	"src/egl_context.c"
	"src/osmesa_context.c"
	)
  add_definitions(
	-D_GLFW_X11
	)
endif()

add_library(GLFW
  ${SrcFiles}
  )

set_target_properties(GLFW PROPERTIES LINKER_LANGUAGE CXX)

 add_definitions(
   -D_CRT_SECURE_NO_WARNINGS
  )
