# Easy clang toolchain guide for stm32 cube project

### STEP 1
Edit `custom-clang.cmake`
```cmake
set(PATH_TO_COMPILER /opt/LLVM-ET-Arm-19.1.5-Linux-x86_64/bin/) # SET PATH HERE
set(LDSCRIPT         STM32F401XX_FLASH.ld)                  # SET FILENAME HERE
set(MCPU             cortex-m4)                             # SET MCPU HERE
set(MFPU             fpv4-sp-d16)                           # SEt MFPU HERE
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
