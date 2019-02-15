# teensy-meson-sample

Sample test repository for meson support with Teensy boards.

### Build instructions

```
git submodule update --init --recursive

mkdir build
cd build

meson .. --cross-file ../subprojects/cores/teensy-3.2-cross.txt
ninja
ninja flash
```

##### Dependencies:
  - arm-none-eabi-gcc (`sudo pacman -S arm-none-eabi-gcc`)
  - teensy-loader-cli (`sudo pacman -S teensy-loader-cli`)
