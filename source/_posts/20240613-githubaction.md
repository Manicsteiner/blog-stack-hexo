---
title: 在 github action 中使用 nmake
date: 2024-06-13 18:52:02
tags:
---
在 github action 中使用 nmake  
```
      - name: Add msbuild to PATH
        uses: microsoft/setup-msbuild@v2

      # Build libwebp
      - name: Checkout libwebp
        shell: cmd
        run: |
          mkdir libwebp\\${{ matrix.msbuild_target }}build
          git clone -b 1.4.0 https://github.com/webmproject/libwebp.git libwebp-140
          cd libwebp-140
          call "C:\Program Files\Microsoft Visual Studio\2022\Enterprise\VC\Auxiliary\Build\vcvarsall.bat" ${{ matrix.crossbuild_target }}
          nmake /f Makefile.vc CFG=release-dynamic RTLIBCFG=dynamic ARCH=${{ matrix.lowercase_target }} OBJDIR=output
          cp output/release-dynamic/${{ matrix.lowercase_target }}/bin/*.dll ../libwebp/${{ matrix.msbuild_target }}build/
```
解析：  
nmake 是VS提供的一个构建工具，在本地只能在“Developer Command Prompt for VS 2022”中调用。  
如果想要在 github action 中调用，需要先启用这个工具。必须在cmd环境下，用call调用。  
位置是由 microsoft/setup-msbuild@v2 展示的路径，目前是写死的，将来可能会变动，应当改进。  
然后在bat调用时传入一个架构信息，可以使nmake进行跨平台构建。  
然后就是比较正常的nmake指令。  
