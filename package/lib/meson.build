lib_cython_tree = [fs.copyfile('__init__.py')]

lib_pyx = custom_target(
  'lib.pyx',
  output: 'lib.pyx',
  input: 'lib.pyx.in',
  command: [py, tempita, '@INPUT@', '-o', '@OUTDIR@'],
  depends: [lib_cython_tree, root_cython_tree, utils_cython_tree]
)

py.extension_module(
  'lib',
  lib_pyx,
  cython_args: cython_args,
  install: true,
  subdir: 'package/lib',
)
