project('pffft', 'c', version: '0.0.1')
ver = meson.project_version()

pkgconfig = import('pkgconfig')

cc = meson.get_compiler('c')
math_dep = cc.find_library('m', required : false)


# Define the static and shared libraries for fftpack
libfftpack_static = static_library('fftpack', 'fftpack.c',
    dependencies: [math_dep],  # Link against the math library
    install: true,
)

libfftpack_shared = shared_library('fftpack', 'fftpack.c',
    version: ver,  # Set version for shared library
    dependencies: [math_dep],  # Link against the math library
    install: true,
)

# Define the static and shared libraries for pffft
libpffft_static = static_library('pffft', 'pffft.c',
    dependencies: [math_dep],  # Link against the math library
    install: true,
)

libpffft_shared = shared_library('pffft', 'pffft.c',
    version: ver,  # Set version for shared library
    dependencies: [math_dep],  # Link against the math library
    install: true,
)

# Define pkg-config files for the shared libraries
pkgconfig.generate(
    name: 'fftpack',
    description: 'FFT Pack Library',
    version: ver,
    libraries: [libfftpack_shared],
)

pkgconfig.generate(
    name: 'pffft',
    description: 'PFFFT Library',
    version: ver,
    libraries: [libpffft_shared],
)

# Install header files in the same directory as meson.build
install_headers('fftpack.h')
install_headers('pffft.h')

# Define the test executable
test_executable = executable(
    'test_pffft', 'test_pffft.c',
    dependencies: [math_dep],  # Link against the math library
    link_with: [libfftpack_shared, libpffft_shared]  # Link against the libraries for the test
)

# Add the test
test('Test', test_executable)
