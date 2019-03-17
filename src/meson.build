
subdir('dec')
subdir('demux')
subdir('dsp')
subdir('utils')
subdir('webp')

libwebpdecoder = library('webpdecoder',
    src_dec,
    src_demux,
    src_dsp,
    src_dsp_dec,
    src_utils,
    src_webp,

    install : false,
    build_by_default : false,

    include_directories : [include_root, webp_includes],
    implicit_include_directories : false,
)

webpdecoder_dep = declare_dependency(
    link_with : libwebpdecoder,
    include_directories : webp_includes,
    version : meson.project_version(),
)
