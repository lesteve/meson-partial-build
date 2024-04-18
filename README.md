Reproducer for https://github.com/scikit-learn/scikit-learn/issues/28837

```bash
meson setup build
ninja -C build
```

```bash
touch package/utils/utils.pxd
# This does not rebuild package/lib/lib shared library
ninja -C build -d explain -v
```

Output:
```
ninja: Entering directory `build'
ninja explain: output meson-test-prereq of phony edge with no inputs doesn't exist
ninja explain: meson-test-prereq is dirty
ninja explain: output meson-benchmark-prereq of phony edge with no inputs doesn't exist
ninja explain: meson-benchmark-prereq is dirty
ninja explain: restat of output package/utils/utils.pxd older than most recent input ../package/utils/utils.pxd (1713451993361700259 vs 1713452006018287455)
ninja explain: package/utils/utils.pxd is dirty
[1/1] /home/lesteve/micromamba/envs/scikit-learn-dev/bin/meson --internal copy ../package/utils/utils.pxd package/utils/utils.pxd
```

```bash
# The second time this builds package/lib/lib shared library
ninja -C build -d explain -v
```

Output:
```
ninja: Entering directory `build'
ninja explain: output meson-test-prereq of phony edge with no inputs doesn't exist
ninja explain: meson-test-prereq is dirty
ninja explain: output meson-benchmark-prereq of phony edge with no inputs doesn't exist
ninja explain: meson-benchmark-prereq is dirty
ninja explain: restat of output package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/package/lib/lib.pyx.c older than most recent input /home/lesteve/dev/meson-partial-build/build/package/utils/utils.pxd (1713452000454989082 vs 1713452006018287455)
ninja explain: package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/package/lib/lib.pyx.c is dirty
ninja explain: package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/package/lib/lib.pyx.c is dirty
ninja explain: package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/meson-generated_package_lib_lib.pyx.c.o is dirty
ninja explain: package/lib/lib.cpython-312-x86_64-linux-gnu.so is dirty
[1/3] cython -M --fast-fail -3 --include-dir /home/lesteve/dev/meson-partial-build/build package/lib/lib.pyx -o package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/package/lib/lib.pyx.c
[2/3] ccache cc -Ipackage/lib/lib.cpython-312-x86_64-linux-gnu.so.p -Ipackage/lib -I../package/lib -Ipackage -Ipackage/utils -I/home/lesteve/micromamba/envs/scikit-learn-dev/include/python3.12 -fvisibility=hidden -fdiagnostics-color=always -D_FILE_OFFSET_BITS=64 -Wall -Winvalid-pch -std=c99 -O2 -g -fPIC -MD -MQ package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/meson-generated_package_lib_lib.pyx.c.o -MF package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/meson-generated_package_lib_lib.pyx.c.o.d -o package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/meson-generated_package_lib_lib.pyx.c.o -c package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/package/lib/lib.pyx.c
[3/3] cc  -o package/lib/lib.cpython-312-x86_64-linux-gnu.so package/lib/lib.cpython-312-x86_64-linux-gnu.so.p/meson-generated_package_lib_lib.pyx.c.o -Wl,--as-needed -Wl,--allow-shlib-undefined -shared -fPIC
```
