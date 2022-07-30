# `theos/vendor/lib`
Libraries included with Theos for easy compilation of most projects out of the box.

This repo uses **.tbd** files, a plain text format that contains the minimum information needed for linking. These are supported as of clang 700 (Xcode 7) and are used in iOS 9.0 and newer SDKs.

TBDs can be generated using either clang’s own [`tapi`](https://github.com/tpoechtrager/apple-libtapi#readme) tool, or the community-developed [`tbd`](https://github.com/inoahdev/tbd).

## Contributions are welcome!
Please contribute any libraries that would be useful to the wider community – whether your own library, or someone else’s. Make sure you follow the code rules below.

## Code rules
* When a library is distributed as a .framework, it should have a file structure similar to the following:
  ```
  Awesome.framework/
  ├ Awesome.tbd
  ├ Headers/
  │ ├ Awesome.h
  │ └ AWAwesomeClass.h
  ├ Modules/
  │ ├ module.modulemap
  │ ├ Awesome.swiftmodule/ (if written in Swift)
  │ │ ├ arm64-apple-ios.swiftdoc
  │ │ ├ arm64-apple-ios.swiftinterface
  │ │ ├ arm64-apple-ios.module
  ╵ ╵ └ etc.
  ```
* When a library is distributed as a loose .dylib and .h header files, contribute the .tbd of the .dylib to this repo, and contribute the headers to [theos/headers](https://github.com/theos/headers). We’ll merge both pull requests at the same time.
* Since binaries are unnecessary for linking, and since it’s difficult for us to review binary contributions anyway, we don’t distribute binaries on this repo – only .tbd files. Use `tbd` or `tapi` to generate a .tbd.
* We prefer tbds that are generated against v1 of the file format, as this guarantees widest compatibility. However, newer versions of the tbd format can be used where it makes sense to.

  Example usage of `tapi` (supports formats v2 and up):

  ```bash
  xcrun tapi stubify --filetype=tbd-v4 --delete-input-file Awesome.framework/Awesome
  ```

  Example usage of `tbd` (supports formats v1 through v4):

  ```
  tbd -p -v1 Awesome.framework/Awesome -o Awesome.framework/Awesome.tbd
  rm Awesome.framework/Awesome
  ```
* When including headers inside .frameworks, follow the [code rules](https://github.com/theos/headers/blob/master/README.md) defined by the theos/headers repo.
* Avoid including headers in both theos/lib and theos/headers. With some unique exceptions where both distribution modes are in widespread use (for instance, Cydia Substrate), headers should either be self-contained in a Headers/ subdirectory in a .framework, or loose in theos/headers.
* Libraries found in SDKs shouldn’t go here – they should already be part of [theos/sdks](https://github.com/theos/sdks). If not, please [file an issue](https://github.com/theos/sdks/issues) on that repo. Thanks!
* Any libraries under an [OSI-approved license](https://opensource.org/licenses) can be included here. Please add its license to [LICENSE.md](LICENSE.md).
