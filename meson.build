project(
  'test-meson',
  'c', 'cython',
  license: 'BSD-3',
  meson_version: '>= 1.1.0',
  default_options: [
    'buildtype=debugoptimized',
    'c_std=c99',
    'cpp_std=c++14',
  ],
)

fs = import('fs')

py = import('python').find_installation(pure: false)

cython_args = ['--include-dir', meson.global_build_root()]

tempita = files('tempita.py')

subdir('package')
