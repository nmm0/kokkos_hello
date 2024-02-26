# Kokkos Example

## Build Commands

### OpenMP/Serial/etc

```sh
cmake -DCMAKE_CXX_STANDARD="17" -DKokkos_ROOT="<path_to_kokkos_install>" ..
```

### CUDA


```sh
cmake -DCMAKE_CXX_COMPILER="/home/nmmoral/code/kokkos/bin/nvcc_wrapper" -DCMAKE_CXX_STANDARD="17" -DKokkos_ROOT="<path_to_kokkos_install>" ..
```
