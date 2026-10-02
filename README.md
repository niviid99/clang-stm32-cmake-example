# Easy clang toolchain guide for stm32 cube project

### STEP 1
Edit path to clang compiler in `custom-clang.cmake`
```cmake
set(CMAKE_SYSTEM_NAME               Generic)
set(CMAKE_SYSTEM_PROCESSOR          arm)

set(CMAKE_C_COMPILER_ID Clang)
set(CMAKE_CXX_COMPILER_ID Clang)

set(TOOLCHAIN_PREFIX                /opt/LLVM-ET-Arm-19.1.5-Linux-x86_64/bin/) # SET PATH HERE

set(CMAKE_C_COMPILER                ${TOOLCHAIN_PREFIX}clang)
set(CMAKE_ASM_COMPILER              ${CMAKE_C_COMPILER})
set(CMAKE_CXX_COMPILER              ${TOOLCHAIN_PREFIX}clang++)
set(CMAKE_LINKER                    ${TOOLCHAIN_PREFIX}clang)
set(CMAKE_OBJCOPY                   ${TOOLCHAIN_PREFIX}llvm-objcopy)
set(CMAKE_SIZE                      ${TOOLCHAIN_PREFIX}llvm-size)
```

### STEP 2
edit ld script generated from stm32cubeMX and remove all `(READONLY)`
```bash
$ sed -i "s/(READONLY)//g" [filename].ld
```

### STEP3 
generate makefile (or ninja) and compile it
```bash
$ cmake -B build # -G Ninja
$ cmake --build build -- -j$(nproc)
```
