lib_cython_tree = [fs.copyfile('__init__.py')]

# In scikit-learn this would actually use tempita on a .pyx.tp file, but
# simpler to reproduce with only copyfile
lib_pyx = fs.copyfile('lib.pyx.in', 'lib.pyx')

py.extension_module(
  'lib',
  lib_pyx,
  lib_cython_tree,
  root_cython_tree,
  utils_cython_tree,
  cython_args: cython_args,
  install: true,
  subdir: 'package/lib',
)
