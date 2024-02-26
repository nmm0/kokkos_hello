## Environment

- You'll need something approximately like this to build and link Kokkos:

```
$ module list

Currently Loaded Modules:
  1) sems-python/3.8.6   2) sems-git/2.37.0   3) cmake/3.25.2   4) sems-gcc/10.1.0   5) cuda/12.0

```

## Clone Kokkos

```
git clone https://github.com/kokkos/kokkos.git

```

## Adjust Makefile
- Minimally, you'll need to set varialbes flagged with "#TODO":

```
# TODO:
KOKKOS_PATH = ${HOME}/bio_kokkos/kokkos
# TODO:
#KOKKOS_DEVICES = "Serial"
#KOKKOS_DEVICES = "OpenMP"
KOKKOS_DEVICES = "Cuda"
# TODO:
EXE_NAME = "view_check_print_exe"



```


## Build, Install Kokkos

- Use `do_cmake` script (taking care to adjust relevant variables, i.e.,
  $INSTALL_DIR, desired backend, etc.)

```
cd kokkos
cp do_cmake kokkos (i.e., project root)
mkdir build
cd build
../do_cmake
make -j
make install
```


