# Easy clang toolchain guide for stm32 cube project

### STEP 1
Edit path to clang compiler in `custom-clang.cmake`
```cmake
#...

set(TOOLCHAIN_PREFIX                /opt/LLVM-ET-Arm-19.1.5-Linux-x86_64/bin/) # SET PATH HERE

set(CMAKE_C_COMPILER                ${TOOLCHAIN_PREFIX}clang)
set(CMAKE_ASM_COMPILER              ${CMAKE_C_COMPILER})
#...
```

### STEP 2
edit ld script generated from stm32cubeMX and remove all `(READONLY)`
```bash
$ sed -i "s/(READONLY)//g" [filename].ld
```

### STEP3 
generate makefile (or ninja) and compile it
```bash
$ cmake -B build -DCMAKE_TOOLCHAIN_FILE=path/to/toolchain/file # -DCMAKE_BUILD_TYPE=Release -G Ninja
$ cmake --build build -- -j$(nproc)
```
