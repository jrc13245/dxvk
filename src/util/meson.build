util_src = files([
  'util_env.cpp',
  'util_string.cpp',
  'util_fps_limiter.cpp',
  'util_flush.cpp',
  'util_gdi.cpp',
  'util_luid.cpp',
  'util_matrix.cpp',
  'util_shared_res.cpp',
  'util_sleep.cpp',

  'thread.cpp',

  'com/com_destruction_notifier.cpp',
  'com/com_guid.cpp',
  'com/com_private_data.cpp',

  'config/config.cpp',

  'log/log.cpp',
  'log/log_debug.cpp',

  'hqx/hq2x.cpp',
  'hqx/hq3x.cpp',
  'hqx/hq4x.cpp',
  'hqx/hqx_init.cpp',
  
  'stb/stb_image.cpp',

  'metrohash/metrohash64.cpp',

  'sha1/sha1.c',
  'sha1/sha1_util.cpp',

  'sync/sync_recursive.cpp',
])

util_lib = static_library('util', util_src,
  include_directories : [ dxvk_include_path ],
)

util_dep = declare_dependency(
  link_with           : [ util_lib ],
)
