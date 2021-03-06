from os.path import basename

def extract(rule, path): 
  name = 'extract-' + rule + '-' + path.replace('.', '-')
  out = basename(path)
  genrule(
    name = name, 
    out = out, 
    cmd = 'cp $(location :' + rule + ')/' + path + ' $OUT', 
  )
  return ':' + name

IPPICV_COMMIT = 'bdb7bb85f34a8cb0d35e40a81f58da431aa1557a'

http_archive(
  name = 'ippicv-archive-macos-x86-64', 
  urls = [
    'https://raw.githubusercontent.com/opencv/opencv_3rdparty/' + IPPICV_COMMIT + '/ippicv/ippicv_2017u3_mac_intel64_general_20180518.tgz', 
  ], 
  type = 'tar.gz', 
  sha256 = '7d2898317d5b3b0d2ec3d3d3c3ab6bb646cb24b528f12b250e818e60f3608c30', 
)

http_archive(
  name = 'ippicv-archive-macos-ia32', 
  urls = [
    'https://raw.githubusercontent.com/opencv/opencv_3rdparty/' + IPPICV_COMMIT + '/ippicv/ippicv_2017u3_mac_ia32_general_20180518.tgz', 
  ], 
  type = 'tar.gz', 
  sha256 = '55aa344a5138b4b15bcf309868e0c744b2c6d6fc439e8df9d239226c6f43955d', 
)

http_archive(
  name = 'ippicv-archive-linux-x86-64', 
  urls = [
    'https://raw.githubusercontent.com/opencv/opencv_3rdparty/' + IPPICV_COMMIT + '/ippicv/ippicv_2017u3_lnx_intel64_general_20180518.tgz', 
  ], 
  type = 'tar.gz', 
  sha256 = '7ff6a1ece3c2a41b0d39ff8e543dbf141615e631e8e6f98dbccde7d4b44eb59f', 
)

ippicv_headers = [
  'ippicv.h', 
  'ippicv_defs_l.h', 
  'ippicv_types.h', 
  'ippicv_base.h', 
  'ippicv_l.h', 
  'ippicv_types_l.h', 
  'ippicv_defs.h', 
  'ippicv_redefs.h', 
  'ippversion.h', 
]

prebuilt_cxx_library(
  name = 'ippicv', 
  header_namespace = '', 
  exported_platform_headers = [
    ('^macos.*', [ extract('ippicv-archive-macos-x86-64', 'ippicv_mac/include/' + x) for x in ippicv_headers ]), 
    ('^linux.*', [ extract('ippicv-archive-linux-x86-64', 'ippicv_lnx/include/' + x) for x in ippicv_headers ]), 
  ], 
  platform_static_lib = [
    ('^macos.*', extract('ippicv-archive-macos-x86-64', 'ippicv_mac/lib/intel64/libippicv.a')), 
    ('^linux.*', extract('ippicv-archive-linux-x86-64', 'ippicv_lnx/lib/intel64/libippicv.a')), 
  ], 
  visibility = [
    'PUBLIC', 
  ], 
)

ippiw_headers = [
  'iw_own.h', 
  'iw_config.h', 
  'iw_owni.h', 
  'iw/iw.h', 
  'iw/iw_image.h', 
  'iw/iw_ll.h', 
  'iw/iw_image_op.h', 
  'iw/iw_version.h', 
  'iw/iw_image_filter.h', 
  'iw/iw_image_color.h', 
  'iw/iw_image_transform.h', 
  'iw/iw_core.h', 
  'iw++/iw_image_op.hpp', 
  'iw++/iw_image.hpp', 
  'iw++/iw_image_transform.hpp', 
  'iw++/iw_core.hpp', 
  'iw++/iw.hpp', 
  'iw++/iw_image_filter.hpp', 
  'iw++/iw_image_color.hpp', 
]

ippiw_srcs = [
  'iw_core.c', 
  'iw_own.c', 
  'iw_image.c', 
  'iw_image_color_convert_rgbs.c', 
  'iw_image_filter_laplacian.c', 
  'iw_image_transform_resize.c', 
  'iw_image_filter_canny.c', 
  'iw_image_filter_bilateral.c', 
  'iw_image_transform_rotate.c', 
  'iw_image_op_copy_channel.c', 
  'iw_image_op_copy_split.c', 
  'iw_image_filter_box.c', 
  'iw_image_transform_warpaffine.c', 
  'iw_image_op_scale.c', 
  'iw_image_op_set_channel.c', 
  'iw_image_filter_general.c', 
  'iw_image_transform_mirror.c', 
  'iw_image_filter_sobel.c', 
  'iw_image_op_copy.c', 
  'iw_image_op_copy_merge.c', 
  'iw_image_op_swap_channels.c', 
  'iw_image_op_set.c', 
  'iw_image_color_convert_all.c', 
  'iw_image_filter_gaussian.c', 
  'iw_image_op_copy_make_border.c', 
  'iw_image_filter_scharr.c', 
  'iw_image_filter_morphology.c', 
]

cxx_library(
  name = 'ippiw', 
  header_namespace = '', 
  exported_platform_headers = [
    ('^macos.*', dict([ (x, extract('ippicv-archive-macos-x86-64', 'ippiw_mac/include/' + x)) for x in ippiw_headers ])), 
    ('^linux.*', dict([ (x, extract('ippicv-archive-linux-x86-64', 'ippiw_lnx/include/' + x)) for x in ippiw_headers ])), 
  ], 
  platform_srcs = [
    ('^macos.*', [ extract('ippicv-archive-macos-x86-64', 'ippiw_mac/src/' + x) for x in ippiw_srcs ]), 
    ('^linux.*', [ extract('ippicv-archive-linux-x86-64', 'ippiw_lnx/src/' + x) for x in ippiw_srcs ]), 
  ], 
  compiler_flags = [
    '-fsigned-char', 
    '-fdiagnostics-show-option', 
    '-fomit-frame-pointer', 
    '-ffunction-sections', 
    '-fdata-sections', 
    '-fvisibility=hidden', 
    '-fPIC', 
    '-msse', 
    '-msse2', 
    '-msse3', 
  ],
  preprocessor_flags = [
    '-DICV_BASE', 
    '-DIW_build=macos', 
    '-DIW_BUILD=1', 
    '-DNDEBUG', 
  ],
  platform_preprocessor_flags = [
    ('^macos.*', [ '-DIW_build=macos' ]), 
  ], 
  deps = [
    ':ippicv', 
  ], 
  visibility = [
    'PUBLIC', 
  ], 
)
