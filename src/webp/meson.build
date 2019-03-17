
src_webp = []

config = configuration_data()

ftest_args = cc.get_supported_arguments('-Werror=implicit-function-declaration')

config.set('HAVE_BUILTIN_BSWAP16', cc.links('int main() { return __builtin_bswap16(42); }', name : '__builtin_bswap16 test', args : ftest_args))
config.set('HAVE_BUILTIN_BSWAP32', cc.links('int main() { return __builtin_bswap32(42); }', name : '__builtin_bswap32 test', args : ftest_args))
config.set('HAVE_BUILTIN_BSWAP64', cc.links('int main() { return __builtin_bswap64(42); }', name : '__builtin_bswap64 test', args : ftest_args))

check_headers = [
    'cpu-features.h',
    'inttypes.h',
    'memory.h',
    'stdint.h',
    'stdlib.h',
    'string.h',
    'strings.h',
    'sys/stat.h',
    'sys/types.h',
    'unistd.h',
]

foreach header : check_headers
    upper = header.to_upper().underscorify()
    config.set('HAVE_@0@'.format(upper), cc.has_header(header))
endforeach

use_simd = get_option('enable_simd')
use_neon_rtcd = use_simd and get_option('enable_neon_rtcd')

config.set('WEBP_HAVE_NEON', use_simd and cc.get_define('__NEON__') != ' ')
config.set('WEBP_HAVE_NEON_RTCD', use_neon_rtcd)
config.set('WEBP_HAVE_SSE2', use_simd and cc.get_define('__SSE2__') != ' ')
config.set('WEBP_HAVE_SSE41', use_simd and cc.get_define('__SSE4_1__') != ' ')

src_webp += configure_file(
    input : 'config.h.meson.in',
    output : 'config.h',
    configuration : config,
)
