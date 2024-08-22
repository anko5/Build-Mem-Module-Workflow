name: Kernel Build

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout kernel source
      uses: actions/checkout@v4

    - name: Set up MemKernel as a module (M-OUT) with specified name
      run: |
        curl -LSs "https://raw.githubusercontent.com/aiichi/MemKernel/main/kernel/setup.sh" | bash -s M dogi

    - name: Android kernel build
      uses: lemniskett/android-kernel-actions@master
      id: build
      env:
        NAME: Loganysl
      with:
        arch: arm64/arm32
        compiler: compiler_version
        defconfig: your_defconfig
        image: Image.gz-dtb

    - name: Upload Kernel and Module
      uses: actions/upload-artifact@v4
      with:
        name: module
        path: |
          ${{ steps.build.outputs.outfile }}
          ./out/drivers/memkernel/memkernel.ko
