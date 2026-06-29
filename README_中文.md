# Android arm64 单文件 libcurl 构建仓库

这个仓库用于在 GitHub Actions 上编译一个适合月虹模块云端下载使用的 `libcurl.so`。

目标产物：

```text
libcurl-arm64-v8a-single.so
```

目标特性：

```text
Android arm64-v8a
HTTPS 可用
OpenSSL 静态打进 libcurl.so
zlib 静态打进 libcurl.so
不依赖 libssl.so
不依赖 libcrypto.so
不依赖 libz.so
不依赖 libnghttp2.so
不依赖 brotli/zstd/idn2/psl/cares
```

合格检查：

```bash
readelf -d libcurl-arm64-v8a-single.so | grep NEEDED
```

允许出现：

```text
liblog.so
libdl.so
libm.so
libc.so
```

不允许出现：

```text
libssl.so
libcrypto.so
libz.so
libnghttp2.so
libbrotlidec.so
libzstd.so
libidn2.so
libpsl.so
```

## 使用方法

进入 GitHub 仓库页面：

```text
Actions → Build Android arm64 single libcurl → Run workflow
```

默认版本：

```text
curl: 8.10.1
OpenSSL: 3.3.2
zlib: 1.3.1
Android API: 23
NDK: r26d
```

编译完成后，在 workflow 页面下载 artifact：

```text
libcurl-arm64-v8a-single
```

里面会包含：

```text
libcurl-arm64-v8a-single.so
NEEDED.txt
ELF_HEADER.txt
```

把 `libcurl-arm64-v8a-single.so` 上传到你的云端直链，然后让模块 JSON 指向它即可。
