---
title: Setup and Building
source_url: https://devguide.python.org/getting-started/setup-building/
source_type: official_documentation
mirrored_at: 2026-10-02T05:37:05+00:00
package: docs.python-devguide
---

# Setup and Building

Source: <https://devguide.python.org/getting-started/setup-building/>

Build CPython locally.

#Setup and building¶ (https://devguide.python.org/getting-started/setup-building/#setup-and-building)

These instructions cover how to get a working copy of the source code and a compiled version of the CPython interpreter (CPython is the version of Python available from https://www.python.org/ (https://www.python.org/)). It also gives an overview of the directory structure of the CPython source code.

Alternatively, if you have Docker (https://www.docker.com/) installed you might want to use our official images (https://gitlab.com/python-devs/ci-images/blob/main/README.md). These contain the latest releases of several Python versions, along with Git head, and are provided for development and testing purposes only.

See also

The Quick reference (https://devguide.python.org/getting-started/quick-reference/#quick-reference) gives brief summary of the process from installing Git to submitting a pull request.

Install Git¶ (https://devguide.python.org/getting-started/setup-building/#install-git)

CPython is developed using Git (https://git-scm.com) for version control. The Git command line program is named `git`; this is also used to refer to Git itself. Git is easily available for all common operating systems.

**Install**

As the CPython repo is hosted on GitHub, please refer to either the GitHub setup instructions (https://docs.github.com/en/get-started/getting-started-with-git/set-up-git) or the Git project instructions (https://git-scm.com) for step-by-step installation directions. You may also want to consider a graphical client such as TortoiseGit (https://tortoisegit.org/) or GitHub Desktop (https://github.com/apps/desktop).

**Configure**

Configure your name and email (https://devguide.python.org/getting-started/git-boot-camp/#set-up-name-email) and create an SSH key (https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) as this will allow you to interact with GitHub without typing a username and password each time you execute a command, such as `gitpull`, `gitpush`, or `gitfetch`. On Windows, you should also enable autocrlf (https://devguide.python.org/getting-started/git-boot-camp/#autocrlf).

Get the source code¶ (https://devguide.python.org/getting-started/setup-building/#get-the-source-code)

The CPython repo is hosted on GitHub. To get a copy of the source code you should fork the Python repository on GitHub (https://devguide.python.org/getting-started/git-boot-camp/#fork-cpython), create a local clone of your personal fork, and configure the remotes (https://devguide.python.org/getting-started/git-boot-camp/#clone-your-fork).

You will only need to execute these steps once per machine:

Go to https://github.com/python/cpython (https://github.com/python/cpython).

Press Fork on the top right.

When asked where to fork the repository, choose to fork it to your username.

Your fork will be created at `https://github.com/*username*/cpython`.

Clone your GitHub fork (replace `username` with your username):

$ git clone git@github.com:username/cpython.git

```

(You can use both SSH-based or HTTPS-based URLs.)

Add an `upstream` remote, then configure `git` to pull `main` from `upstream` and always push to `origin`:

$ cd cpython
$ git remote add upstream https://github.com/python/cpython
$ git config --local branch.main.remote upstream
$ git remote set-url --push upstream git@github.com:your-username/cpython.git

```

Verify that your setup is correct:

$ git remote -v
origin  git@github.com:your-username/cpython.git (fetch)
origin  git@github.com:your-username/cpython.git (push)
upstream        https://github.com/python/cpython (fetch)
upstream        git@github.com:your-username/cpython.git (push)
$ git config branch.main.remote
upstream

```

For more information about these commands see Git Bootcamp and Cheat Sheet (https://devguide.python.org/getting-started/git-boot-camp/#git-boot-camp).

If you did everything correctly, you should now have a copy of the code in the `cpython` directory and two remotes that refer to your own GitHub fork (`origin`) and the official CPython repository (`upstream`).

If you want a working copy of an already-released version of Python, that is, a version in maintenance mode (https://devguide.python.org/developer-workflow/development-cycle/#maintbranch), you can checkout a release branch. For instance, to checkout a working copy of Python 3.13, do `gitswitch3.13`.

You will need to re-compile CPython when you do such an update.

Do note that CPython will notice that it is being run from a working copy. This means that if you edit CPython’s source code in your working copy, changes to Python code will be picked up by the interpreter for immediate use and testing. (If you change C code, you will need to recompile the affected files as described below.)

Changes for the documentation can be made from the same repository; see Getting started (https://devguide.python.org/documentation/start-documenting/#documenting).

Install pre-commit as a Git hook¶ (https://devguide.python.org/getting-started/setup-building/#install-pre-commit-as-a-git-hook)

To make sure your code is linted correctly, we recommend setting up pre-commit (https://pre-commit.com#installation) as a Git hook:

$ pre-commit install --allow-missing-config
pre-commit installed at .git/hooks/pre-commit

```

Now pre-commit will run automatically on `gitcommit`.

Compile and build¶ (https://devguide.python.org/getting-started/setup-building/#compile-and-build)

CPython provides several compilation flags which help with debugging various things. While all of the known flags can be found in the `Misc/SpecialBuilds.txt` file, the most critical one is the `Py_DEBUG` flag which creates what is known as a “pydebug” build. This flag turns on various extra sanity checks which help catch common issues. The use of the flag is so common that turning on the flag is a basic compile option.

You should always develop under a pydebug build of CPython (the only instance of when you shouldn’t is if you are taking performance measurements). Even when working only on pure Python code the pydebug build provides several useful checks that one should not skip.

See also

The effects of various configure and build flags are documented in the Python configure docs (https://docs.python.org/dev/using/configure.html).

Unix¶ (https://devguide.python.org/getting-started/setup-building/#unix)

The core CPython interpreter only needs a C compiler to be built, however, some of the extension modules will need development headers for additional libraries (such as the `zlib` library for compression). Depending on what you intend to work on, you might need to install these additional requirements so that the compiled interpreter supports the desired features.

If you want to install these optional dependencies, consult the Install dependencies (https://devguide.python.org/getting-started/setup-building/#build-dependencies) section below.

If you don’t need to install them, the basic steps for building Python for development is to configure it and then compile it.

Configuration is typically:

$ ./configure --with-pydebug

```

More flags are available to `configure`, but this is the minimum you should do to get a pydebug build of CPython.

Tip

To speed up repeated `configure` runs, use `--config-cache` (equivalent to `--cache-file=config.cache`, short: `-C`):

$ ./configure --config-cache --with-pydebug

```

This caches results in a `config.cache` file. If you switch compilers or significantly change your build environment, delete `config.cache` before re-running `configure`.

Note

You might need to run `makeclean` before or after re-running `configure` in a particular build directory.

Once `configure` is done, you can then compile CPython with:

$ make -s -j $(nproc)

```

This will build CPython with only warnings and errors being printed to stderr. The `-j` argument means that **make** will concurrently run tasks, limiting the number of parallel jobs to the number of CPU cores in your computer. You can adjust the number passed to the `-j` flag to change the limit on parallel jobs, which can trade RAM usage versus compilation time.

At the end of the build you should see a success message, followed by a list of extension modules that haven’t been built because their dependencies were missing:

The necessary bits to build these optional modules were not found:
_gdbm
To find the necessary bits, look in configure.ac and config.log.

Checked 106 modules (31 built-in, 74 shared, 0 n/a on macosx-13.4-arm64, 0 disabled, 1 missing, 0 failed on import)

```

If the build failed and you are using a C89 or C99-compliant compiler, please open a bug report on the issue tracker (https://github.com/python/cpython/issues).

If you decide to Install dependencies (https://devguide.python.org/getting-started/setup-building/#build-dependencies), you will need to re-run both `configure` and `make`.

Once CPython is done building you will then have a working build that can be run in-place; `./python` on most machines (and what is used in all examples), `./python.exe` wherever a case-insensitive filesystem is used (for example, on macOS by default), in order to avoid conflicts with the `Python` directory. There is normally no need to install your built copy of Python! The interpreter will realize where it is being run from and thus use the files found in the working copy. If you are worried you might accidentally install your working copy build, you can add `--prefix=/tmp/python` to the configuration step. When running from your working directory, it is best to avoid using the `--enable-shared` flag to `configure`; unless you are very careful, you may accidentally run with code from an older, installed shared Python library rather than from the interpreter you just built.

Clang¶ (https://devguide.python.org/getting-started/setup-building/#clang)

If you are using clang (https://clang.llvm.org/) to build CPython, some flags you might want to set to quiet some standard warnings which are specifically superfluous to CPython are `-Wno-unused-value-Wno-empty-body-Qunused-arguments`. You can set your `CFLAGS` environment variable to these flags when running `configure`.

If you are using clang (https://clang.llvm.org/) with ccache (https://ccache.dev/), turn off the noisy `parentheses-equality` warnings with the `-Wno-parentheses-equality` flag. These warnings are caused by clang not having enough information to detect that extraneous parentheses in expanded macros are valid, because the preprocessing is done separately by ccache.

If you are using LLVM 2.8, also use the `-no-integrated-as` flag in order to build the `ctypes` (https://docs.python.org/3/library/ctypes.html#module-ctypes) module (without the flag the rest of CPython will still build properly).

Optimization¶ (https://devguide.python.org/getting-started/setup-building/#optimization)

If you are trying to improve CPython’s performance, you will probably want to use an optimized build of CPython. It can take a lot longer to build CPython with optimizations enabled, and it’s usually not necessary to do so. However, it’s essential if you want accurate benchmark results for a proposed performance optimization.

For an optimized build of Python, use `configure--enable-optimizations--with-lto`. This sets the default make targets up to enable Profile Guided Optimization (PGO) and may be used to auto-enable Link Time Optimization (LTO) on some platforms. See `--enable-optimizations` (https://docs.python.org/3/using/configure.html#cmdoption-enable-optimizations) and `--with-lto` (https://docs.python.org/3/using/configure.html#cmdoption-with-lto) to learn more about these options.

$ ./configure --enable-optimizations --with-lto

```

Windows¶ (https://devguide.python.org/getting-started/setup-building/#windows)

Note

If you are using the Windows Subsystem for Linux (WSL), clone the repository (https://devguide.python.org/getting-started/setup-building/#checkout) from a native Windows shell program like PowerShell or the `cmd.exe` command prompt, and use a build of Git targeted for Windows, for example, the Git for Windows download from the official Git website (https://git-scm.com/download/win). Otherwise, Visual Studio will not be able to find all the project’s files and will fail the build.

For a concise step by step summary of building Python on Windows, you can read Victor Stinner’s guide (https://web.archive.org/web/20220907075854/https://cpython-core-tutorial.readthedocs.io/en/latest/build_cpython_windows.html).

All supported versions of Python can be built using Microsoft Visual Studio 2017 or later. You can download and use any of the free or paid versions of Visual Studio (https://visualstudio.microsoft.com/).

When installing it, select the Python development workload and the optional Python native development tools component to obtain all of the necessary build tools. You can find Git for Windows on the Individual components tab if you don’t already have it installed.

Note

If you want to build MSI installers, be aware that the build toolchain for them has a dependency on the Microsoft .NET Framework Version 3.5 (which may not be included on recent versions of Windows, such as Windows 10). If you are building on a recent Windows version, use the Control Panel (Programs ‣ Programs and Features ‣ Turn Windows Features on or off) and ensure that the entry .NET Framework 3.5 (includes .NET 2.0 and 3.0) is enabled.

Your first build should use the command line to ensure any external dependencies are downloaded:

PCbuild\build.bat -c Debug

```

The above command line build uses the `-cDebug` argument to build in the `Debug` configuration, which enables checks and assertions helpful for developing Python. By default, it builds in the `Release` configuration and for the 64-bit `x64` platform rather than 32-bit `Win32`; use `-c` and `-p` to control build config and platform, respectively.

After this build succeeds, you can open the `PCbuild\pcbuild.sln` solution in the Visual Studio IDE to continue development, if you prefer. When building in Visual Studio, make sure to select build settings that match what you used with the script (the Debug configuration and the x64 platform) from the dropdown menus in the toolbar.

Note

If you need to change the build configuration or platform, build once with the `build.bat` script set to those options first before building with them in VS to ensure all files are rebuilt properly, or you may encounter errors when loading modules that were not rebuilt.

Avoid selecting the `PGInstrument` and `PGUpdate` configurations, as these are intended for PGO builds and not for normal development.

You can run the build of Python you’ve compiled with:

PCbuild\amd64\python_d.exe

```

See the PCBuild readme (https://github.com/python/cpython/blob/main/PCbuild/readme.txt) for more details on what other software is necessary and how to build.

WASI¶ (https://devguide.python.org/getting-started/setup-building/#wasi)

WASI (https://wasi.dev) is a system interface standard for WebAssembly (https://webassembly.org). Through a combination of C compilers that can target WebAssembly and wasi-libc (https://github.com/WebAssembly/wasi-libc) providing POSIX-compatible shims for WASI, it’s possible for CPython to run on a WASI host/runtime as a *guest*.

Note

The instructions below assume a Unix-based OS due to cross-compilation for CPython being designed for `./configure` / `make`.

To build for WASI, you will need to cross-compile CPython. This requires a C compiler just like building for Unix (https://devguide.python.org/getting-started/setup-building/#unix-compiling) as well as:

A C compiler that can target WebAssembly (for example, WASI SDK (https://github.com/WebAssembly/wasi-sdk))

A WASI host/runtime (for example, Wasmtime (https://wasmtime.dev))

A system install of Python 3.11 or newer to run the build scripts

All of this is provided in the WASI dev container (https://devguide.python.org/getting-started/setup-building/#using-a-container) (which you can select as an alternative container when using a codespace (https://devguide.python.org/getting-started/setup-building/#codespaces-whats-codespaces)). You can also use what’s installed in the container as a reference of what versions of these tools are known to work.

Note

CPython has only been verified with the certain tools for WASI. Using other compilers, hosts, or WASI versions *should* work, but the tools and their versions specified in the container and build scripts are tested via a buildbot (https://devguide.python.org/testing/buildbots/#buildbots).

Building for WASI requires doing a cross-build where you have a *build* Python to help produce a WASI build of CPython (technically it’s a “host x host” cross-build because the build Python is also the target Python while the host build is the WASI build). This means you effectively build CPython twice: once to have a version of Python for the build system to use and another that’s the build you ultimately care about (that is, the build Python is not meant for use by you directly, only the build system).

The easiest way to get a debug build of CPython for WASI is to run the following command:

Python 3.15+

python Platforms/WASI build --quiet -- --config-cache --with-pydebug

```

Python 3.14

python Tools/wasm/wasi build --quiet -- --config-cache --with-pydebug

```

Python 3.13

python Tools/wasm/wasi.py build --quiet -- --config-cache --with-pydebug

```

That single command will configure and build both the build Python and the WASI build in the `cross-build/` directory.

You can also do each configuration and build step separately; the command above is a convenience wrapper around the following commands:

Python 3.15+

$ python Platforms/WASI configure-build-python --quiet -- --config-cache --with-pydebug
$ python Platforms/WASI make-build-python --quiet
$ python Platforms/WASI configure-host --quiet -- --config-cache
$ python Platforms/WASI make-host --quiet

```

Python 3.14

$ python Tools/wasm/wasi configure-build-python --quiet -- --config-cache --with-pydebug
$ python Tools/wasm/wasi make-build-python --quiet
$ python Tools/wasm/wasi configure-host --quiet -- --config-cache
$ python Tools/wasm/wasi make-host --quiet

```

Python 3.13

$ python Tools/wasm/wasi.py configure-build-python --quiet -- --config-cache --with-pydebug
$ python Tools/wasm/wasi.py make-build-python --quiet
$ python Tools/wasm/wasi.py configure-host --quiet -- --config-cache
$ python Tools/wasm/wasi.py make-host --quiet

```

Note

The `configure-host` command infers the use of `--with-pydebug` from the build Python.

Running the separate commands after `build` is useful if you, for example, only want to run the `make-host` step after making code changes.

Once everything is complete, there will be a `cross-build/wasm32-wasip1/python.sh` helper file which you can use to run the `python.wasm` file (see the output from the `configure-host` subcommand):

cross-build/wasm32-wasip1/python.sh --version

```

You can also use `Makefile` targets and they will work as expected thanks to the `HOSTRUNNER` environment variable having been set to a similar value as used in `python.sh`:

make -C cross-build/wasm32-wasip1 test

```

Note

WASI uses a *capability-based* security model. This means that the WASI host does not give full access to your machine unless you tell it to. This also means things like files can end up being mapped to a different path inside the WASI host. So, if you try passing a file path to `python.wasm`/ `python.sh`, it needs to match the path **inside** the WASI host, not the path on your machine (much like using a container).

Emscripten¶ (https://devguide.python.org/getting-started/setup-building/#emscripten)

Emscripten (https://emscripten.org/) is a complete open-source compiler toolchain. It compiles C/C++ code into WebAssembly (https://webassembly.org)/JavaScript executables, for use in JavaScript runtimes, including browsers and Node.js.

Note

The instructions below assume a Unix-based OS due to cross-compilation for CPython being designed for `./configure` / `make`.

To build for Emscripten, you will need to cross-compile CPython. This requires a C compiler just like building for Unix (https://devguide.python.org/getting-started/setup-building/#unix-compiling). The Node Version Manager (`nvm`) must also be on your path.

Building for Emscripten requires doing a cross-build where you have a *build* Python to help produce an Emscripten build of CPython. This means you build CPython twice: once to have a version of Python for the build system to use and another that’s the build you ultimately care about (that is, the build Python is not meant for use by you directly, only the build system).

The simplest way to build Emscripten is to run:

export EMSDK_CACHE=$PWD/cross-build/emsdk
python3 Platforms/emscripten install-emscripten
python3 Platforms/emscripten build all

```

`install-emscripten` downloads and installs the version of the Emscripten SDK required, placing it in the `EMSDK_CACHE` directory. `buildall` will:

Build a copy of Python that can run on the host machine (the “build” python);

Use nvm (https://github.com/nvm-sh/nvm#intro) to ensure that the needed version of Node is installed;

Download the code for all the binary dependencies of Python (such as `libffi` and `mpdecimal`), and compile them for Emscripten; and

Build a copy of Python that can run on Emscripten (the “host” python).

The built binary dependencies are cached inside the Emscripten cache directory. Once built for a given Emscripten version, they will not be rebuilt on subsequent runs unless there is a change in the version or build script for the dependency.

It is assumed that nvm (https://github.com/nvm-sh/nvm#intro) is installed in `${HOME}/.nvm`. If you don’t have nvm installed or don’t want to use it, you can pass `--host-runnernode` to the `build` command. The argument should either be the name of an executable that can be found on the `PATH` or a relative or absolute path to an executable.

If you omit the `EMSDK_CACHE` environment variable, the build script will assume that the current environment has the Emscripten tools available. You are responsible for downloading and activating those tools in your environment. The version of Emscripten and Node that is required to build Python is defined in the Platforms/emscripten/config.toml (https://github.com/python/cpython/blob/main/Platforms/emscripten/config.toml) configuration file.

There are two environment variables that can be used to control the operation of the `Platforms/emscripten` build script:

`EMSDK_CACHE` (or the `--emsdk-cache` flag) controls the location of the Emscripten SDK cache directory. You can use this environment variable instead of passing the `--emsdk-cache` flag. When set, the build script will validate that the required Emscripten version is present in the cache and will exit with an error if it is not; run `install-emscripten` to populate the cache.

`CROSS_BUILD_DIR` (or the `--cross-build-dir` flag) defines the location of the `cross-build` directory that will be used for builds. This can be useful if you need to maintain builds of multiple versions of Python side by side.

It is possible (but not necessary) to enable `ccache` for Emscripten builds by setting the `EM_COMPILER_WRAPPER` environment variable:

export EM_COMPILER_WRAPPER=ccache

```

To get a debug build of CPython for Emscripten, use:

python3 Platforms/emscripten build all -- --with-pydebug

```

That single command will configure and build both the build Python and the Emscripten build in `cross-build/build` and `cross-build/wasm32-emscripten/build/python/`, respectively.

The `Platforms/emscripten` script has a number of other entry points that allow for fine-grained execution of each part of an Emscripten build; run `python3Platforms/emscripten--help` for more details.

Once the build is complete, you can run Python code using:

python3 Platforms/emscripten run ./path/to/script.py

```

You can run the CPython test suite using:

python3 Platforms/emscripten run --test

```

Additional instructions for running the resulting builds (through Node.js and/or through web browsers) are available in the CPython repository at Platforms/emscripten/README.md (https://github.com/python/cpython/blob/main/Platforms/emscripten/README.md).

Android¶ (https://devguide.python.org/getting-started/setup-building/#android)

Build and test instructions for Android are maintained in the CPython repository at Platforms/Android/README.md (https://github.com/python/cpython/blob/main/Platforms/Android/README.md).

iOS¶ (https://devguide.python.org/getting-started/setup-building/#ios)

Compiling Python for iOS requires a macOS machine, on a recent version of macOS, running a recent version of Xcode. Apple expects developers to keep their operating systems and tools up-to-date; if your macOS version is more than one major release out of date, or your Xcode version is more than a couple of minor versions out of date, you’ll likely encounter difficulties. It is not possible to compile for iOS using Windows or Linux as a build machine.

A complete build for Python on iOS requires compiling CPython four times: once for macOS; then once for each of the three underlying platforms used by iOS:

An ARM64 device (an iPhone or iPad);

An ARM64 simulator running on a recent macOS machine; and

An x86_64 simulator running on older macOS machine.

You will need an existing Python 3 interpreter to build Python. From the root of a CPython code checkout, run the following:

Python 3.15+

$ python3 Platforms/Apple build iOS all

```

Python 3.14

$ python3 Apple build iOS all

```

Python 3.13

Python 3.13 requires explicitly invoking `configure` and `make` for each platform. For example, to build for the ARM64 simulator, run:

$ export PATH="$(pwd)/iOS/Resources/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin"
$ ./configure \
      LIBLZMA_CFLAGS="-Ipath/to/xz/include" \
      LIBLZMA_LIBS="-Lpath/to/xz/lib -llzma" \
      BZIP2_CFLAGS="-Ipath/to/bzip2/include" \
      BZIP2_LIBS="-Lpath/to/bzip2/lib -lbz2" \
      LIBFFI_CFLAGS="-Ipath/to/libffi/include" \
      LIBFFI_LIBS="-Lpath/to/libffi/lib -lffi" \
      --with-openssl="path/to/openssl" \
      --host=arm64-apple-ios-simulator \
      --build=arm64-apple-darwin \
      --with-build-python=path/to/python3.13 \
      --enable-framework
$ make -j4 all
$ make install

```

The `--host` argument should be one of `arm64-apple-ios-simulator`, `x64_64-apple-ios-simulator` or `arm64-apple-ios`. Your `PATH` should be kept to a minimum to avoid inadvertently linking ARM64 macOS binaries into your iOS project. You must specify a path to pre-compiled binary dependencies.

Once you have built an Apple Framework for each architecture, you will need to manually construct an XCframework.

This will:

Build a copy of Python that can run on macOS (the “build” python);

Download pre-compiled binaries for dependencies of CPython (such as `libFFI` and `xz`)

Build a copy of Python for each supported iOS architecture (x86_64 simulator, ARM64 simulator, and ARM64 device); and

Generate a release artefact for iOS

Once this build completes, the `cross-build/iOS` folder will contain a `Python.xcframework`, and the `cross-build/dist` folder will contain a release tarball.

To run the test suite on iOS, run:

Python 3.15+

$ python3 Platforms/Apple test iOS

```

Python 3.14

$ python3 Apple test iOS

```

Python 3.13

$ make testios

```

The full test suite takes approximately 12 minutes to run on a 2022 M1 MacBook Pro, plus a couple of extra minutes to build the testbed application and boot the simulator. You should see an iOS simulator appear during the testing process; the simulator will boot to an iOS landing screen, the testbed app will be installed, and then started. The screen of the simulator will be black while the test suite is running. When the test suite completes, success or failure will be reported at the command line.

Two environment variables can be used to configure the operation of the Apple build script:

`CACHE_DIR` defines the location where downloaded artefacts, such as precompiled `libFFI` and `xz` binaries, will be stored.

`CROSS_BUILD_DIR` defines the name of the `cross-build` directory that will be used for builds. This can be useful if you need to maintain builds of multiple versions of Python.

The `Platforms/Apple` script has a number of other entry points that allow for fine-grained execution of each part of an iOS build; run `python3Platforms/Apple--help` for more details.

You can also run the test suite in Xcode itself. This is required if you want to run on a physical device. See the iOS README (https://github.com/python/cpython/blob/main/Platforms/Apple/iOS/README.md#debugging-test-failures) for details.

Install dependencies¶ (https://devguide.python.org/getting-started/setup-building/#install-dependencies)

This section explains how to install libraries which are needed to compile some of CPython’s modules (for example, `zlib`).

Linux

For Unix-based systems, we try to use system libraries whenever available. This means optional components will only build if the relevant system headers are available. The best way to obtain these headers varies by distribution, but commands for some popular distributions are given below.

Fedora / RHEL / CentOS

On **Fedora**, **RHEL**, **CentOS** and other `dnf`-based systems:

$ sudo dnf install git pkg-config
$ sudo dnf install dnf-plugins-core  # install this to use 'dnf builddep'
$ sudo dnf builddep python3

```

Some optional development dependencies are not included in the above. To install some additional dependencies for optional build and test components:

$ sudo dnf install \
      gcc gcc-c++ gdb lzma glibc-devel libstdc++-devel openssl-devel \
      readline-devel zlib-devel libzstd-devel libffi-devel bzip2-devel \
      xz-devel sqlite sqlite-devel sqlite-libs libuuid-devel gdbm-libs \
      perf expat expat-devel mpdecimal python3-pip

```

Debian / Ubuntu

On **Debian**, **Ubuntu**, and other `apt`-based systems, try to get the dependencies for the Python you’re working on by using the `apt` command.

First, make sure you have enabled the source packages in the sources list. Where those live depends on your release.

On **Ubuntu 24.04 and later**, and on other releases using the deb822 format, the sources are in `/etc/apt/sources.list.d/ubuntu.sources`. Add `deb-src` to the `Types` field of the entries you want sources for:

$ sudo nano /etc/apt/sources.list.d/ubuntu.sources

```

changing:

Types: deb

```

to:

Types: deb deb-src

```

On **Ubuntu 22.04 and other releases using the one-line format**, add the location of the source packages, including URL, distribution name and component name, to `/etc/apt/sources.list`. Taking Ubuntu 22.04 LTS (Jammy Jellyfish) as the example:

$ deb-src http://archive.ubuntu.com/ubuntu/ jammy main

```

Alternatively, uncomment the lines with `deb-src` using an editor, for example:

$ sudo nano /etc/apt/sources.list

```

For other distributions, like Debian, change the URL and names to correspond with the specific distribution.

Then you should update the packages index:

$ sudo apt-get update

```

Now you can install the build dependencies via `apt`:

$ sudo apt-get build-dep python3
$ sudo apt-get install pkg-config

```

If you want to build all optional modules, install the following packages and their dependencies:

$ sudo apt-get install build-essential gdb lcov pkg-config \
      libbz2-dev libffi-dev libgdbm-dev libgdbm-compat-dev liblzma-dev \
      libncurses5-dev libreadline6-dev libsqlite3-dev libssl-dev \
      lzma lzma-dev tk-dev uuid-dev zlib1g-dev libmpdec-dev libzstd-dev \
      inetutils-inetd

```

Note that Debian 12 and Ubuntu 24.04 do not have the `libmpdec-dev` package. You can remove it from the install list above: for Python 3.15 and older, the build will use a bundled version; for Python 3.16 and newer, the bundled copy has been removed and the `decimal` (https://docs.python.org/3/library/decimal.html#module-decimal) module will fall back to its slower pure-Python implementation. We recommend using the system libmpdec (https://www.bytereef.org/mpdecimal/doc/libmpdec/) library. Either build it from sources or install this package from https://deb.sury.org (https://deb.sury.org).

macOS

For **macOS systems** (versions 10.9+), the Developer Tools can be downloaded and installed automatically; you do not need to download the complete Xcode application.

If necessary, run the following:

$ xcode-select --install

```

This will also ensure that the system header files are installed into `/usr/include`.

Also note that macOS does not include several libraries used by the Python standard library, including `libzma`, so expect to see some extension module build failures unless you install local copies of them. As of OS X 10.11, Apple no longer provides header files for the deprecated system version of OpenSSL which means that you will not be able to build the `_ssl` extension. One solution is to install these libraries from a third-party package manager, like Homebrew (https://brew.sh) or MacPorts (https://www.macports.org), and then add the appropriate paths for the header and library files to your `configure` command.

Homebrew

For **Homebrew**, install dependencies using `brew`:

$ brew bundle --file=Misc/Brewfile

```

Then configure:

$ GDBM_CFLAGS="-I$(brew --prefix gdbm)/include" \
   GDBM_LIBS="-L$(brew --prefix gdbm)/lib -lgdbm" \
   ./configure --config-cache \
               --with-pydebug \
               --with-openssl="$(brew --prefix openssl@3)"

```

MacPorts

For **MacPorts**, install dependencies using `port`:

$ sudo port install pkgconfig openssl xz gdbm tk +quartz mpdecimal zstd

```

Then configure:

$ GDBM_CFLAGS="-I$(dirname $(dirname $(which port)))/include" \
   GDBM_LIBS="-L$(dirname $(dirname $(which port)))/lib -lgdbm" \
   ./configure --config-cache \
               --with-pydebug

```

And finally, run `make`:

$ make -s -j8

```

There will sometimes be optional modules added for a new release which won’t yet be identified in the OS-level build dependencies. In those cases, just ask for assistance in the *Core Development* category on Discourse (https://devguide.python.org/getting-started/getting-help/#help-discourse).

Explaining how to build optional dependencies on a Unix-based system without root access is beyond the scope of this guide.

For more details on various options and considerations for building, refer to the macOS README (https://github.com/python/cpython/blob/main/Mac/README.rst).

Note

While you need a C compiler to build CPython, you don’t need any knowledge of the C language to contribute! Vast areas of CPython are written completely in Python: as of this writing, CPython contains slightly more Python code than C.

Windows

On Windows, extensions are already included and built automatically.

Android

The BeeWare project maintains scripts for building Android dependencies (https://github.com/beeware/cpython-android-source-deps), and distributes pre-compiled Android binaries (https://github.com/beeware/cpython-android-source-deps/releases) for each of them. These binaries are automatically downloaded and used by the CPython build script at Platforms/Android (https://github.com/python/cpython/blob/main/Platforms/Android).

iOS

The BeeWare project maintains scripts for building iOS dependencies (https://github.com/beeware/cpython-apple-source-deps), and distributes pre-compiled iOS binaries (https://github.com/beeware/cpython-apple-source-deps/releases) for each of them. These binaries are automatically downloaded and used by the CPython build script at Platforms/Apple (https://github.com/python/cpython/blob/main/Platforms/Apple).

If you are building for Python 3.13, you will need to manually download and install these binaries, and provide the path to the binaries as part of the call to `configure`.

Regenerate `configure`¶ (https://devguide.python.org/getting-started/setup-building/#regenerate-configure)

If a change is made to Python which relies on some POSIX system-specific functionality (such as using a new system call), it is necessary to update the configure (https://github.com/python/cpython/blob/main/configure) script to test for availability of the functionality. Python’s `configure` script is generated from configure.ac (https://github.com/python/cpython/blob/main/configure.ac) using GNU Autoconf (https://www.gnu.org/software/autoconf/).

After editing `configure.ac`, run `makeregen-configure` to generate `configure`, pyconfig.h.in (https://github.com/python/cpython/blob/main/pyconfig.h.in), and aclocal.m4 (https://github.com/python/cpython/blob/main/aclocal.m4). When submitting a pull request with changes made to `configure.ac`, make sure you also commit the changes in the generated files.

Python’s `configure.ac` script requires a specific version of GNU Autoconf. For Python 3.12 and newer, GNU Autoconf v2.71 is required. For Python 3.11, GNU Autoconf v2.69 is required.

The recommended and by far the easiest way to regenerate `configure` is:

$ make regen-configure

```

This will use Podman or Docker to do the regeneration with the proper version of GNU Autoconf.

If you cannot (or don’t want to) use `makeregen-configure`, install the **autoconf-archive** and **pkg-config** utilities, and make sure the `pkg.m4` macro file located in the appropriate **aclocal** location:

$ ls $(aclocal --print-ac-dir) | grep pkg.m4

```

Note

Running **autoreconf** is not the same as running **autoconf**. For example, running **autoconf** by itself will not regenerate `pyconfig.h.in`. **autoreconf** runs **autoconf** and a number of other tools repeatedly as appropriate.

Regenerate the ABI dump¶ (https://devguide.python.org/getting-started/setup-building/#regenerate-the-abi-dump)

Maintenance branches (not `main`) have a special file located in `Doc/data/pythonX.Y.abi` that allows us to know if a given pull request affects the public ABI. This file is used by the GitHub CI in a check called `CheckiftheABIhaschanged` that will fail if a given pull request has changes to the ABI and the ABI file is not updated.

This check acts as a fail-safe and **doesn’t necessarily mean that the pull request cannot be merged**. When this check fails you should add the relevant release manager to the PR so that they are aware of the change and they can validate if the change can be made or not.

Important

ABI changes are allowed before the first release candidate. After the first release candidate, all further releases must have the same ABI for ensuring compatibility with native extensions and other tools that interact with the Python interpreter. See the documentation about the release candidate (https://devguide.python.org/developer-workflow/development-cycle/#rc) phase.

When the PR check fails, the associated run will have the updated ABI file attached as an artifact. After release manager approval, you can download and add this file into your PR to pass the check.

You can regenerate the ABI file by yourself by invoking the `regenabidump` Make target. Note that for doing this you need to regenerate the ABI file in the same environment that the GitHub CI uses to check for it. This is because different platforms may include some platform-specific details that make the check fail even if the Python ABI is the same. The easier way to regenerate the ABI file using the same platform as the CI uses is by using Docker:

# In the CPython root:
$ docker run -v$(pwd):/src:Z -w /src --rm -it ubuntu:22.04 \
    bash /src/.github/workflows/regen-abidump.sh

```

Note that the `ubuntu` version used to execute the script matters and **must** match the version used by the CI to check the ABI. See the `.github/workflows/build.yml` file for more information.

Troubleshoot the build¶ (https://devguide.python.org/getting-started/setup-building/#troubleshoot-the-build)

This section lists some of the common problems that may arise during the compilation of Python, with proposed solutions.

Avoid recreating auto-generated files¶ (https://devguide.python.org/getting-started/setup-building/#avoid-recreating-auto-generated-files)

Under some circumstances you may encounter Python errors in scripts like `Parser/asdl_c.py` or `Python/makeopcodetargets.py` while running `make`. Python auto-generates some of its own code, and a full build from scratch needs to run the auto-generation scripts. However, this makes the Python build require an already installed Python interpreter; this can also cause version mismatches when trying to build an old (2.x) Python with a new (3.x) Python installed, or vice versa.

To overcome this problem, auto-generated files are also checked into the Git repository. So if you don’t touch the auto-generation scripts, there’s no real need to auto-generate anything.

Editors and tools¶ (https://devguide.python.org/getting-started/setup-building/#editors-and-tools)

Python is used widely enough that practically all code editors have some form of support for writing Python code. Various coding tools also include Python support.

For editors and tools which the core developers have felt some special comment is needed for coding *in* Python, see Additional resources (https://devguide.python.org/#resources).

Directory structure¶ (https://devguide.python.org/getting-started/setup-building/#directory-structure)

There are several top-level directories in the CPython source tree. Knowing what each one is meant to hold will help you find where a certain piece of functionality is implemented. Do realize, though, there are always exceptions to every rule.

`Doc`

The official documentation. This is what https://docs.python.org/ (https://docs.python.org/) uses. See also Building the documentation (https://devguide.python.org/documentation/start-documenting/#building-doc).

`Grammar`

Contains the PEG (Parser Expression Grammar) grammar file for Python.

`Include`

Contains all interpreter-wide header files.

`Lib`

The part of the standard library implemented in pure Python.

`Mac`

Mac-specific code (for example, using IDLE as a macOS application).

`Misc`

Things that do not belong elsewhere. Typically this is varying kinds of developer-specific documentation.

`Modules`

The part of the standard library (plus some other code) that is implemented in C.

`Objects`

Code for all built-in types.

`PC`

Windows-specific code.

`PCbuild`

Build files for the version of MSVC currently used for the Windows installers provided on python.org.

`Parser`

Code related to the parser. The definition of the AST nodes is also kept here.

`Programs`

Source code for C executables, including the main function for the CPython interpreter.

`Python`

The code that makes up the core CPython runtime. This includes the compiler, eval loop and various built-in modules.

`Tools`

Various tools that are (or have been) used to maintain Python.

Using a container¶ (https://devguide.python.org/getting-started/setup-building/#using-a-container)

There are various ways to use a container to build CPython without installing additional tools on your machine. All approaches use the container defined in the cpython-devcontainers repo (https://github.com/python/cpython-devcontainers) in some way.

Contribute using GitHub Codespaces¶ (https://devguide.python.org/getting-started/setup-building/#contribute-using-github-codespaces)

What is GitHub Codespaces?¶ (https://devguide.python.org/getting-started/setup-building/#what-is-github-codespaces)

If you’d like to start contributing to CPython without needing to set up a local developer environment, you can use GitHub Codespaces (https://github.com/features/codespaces). Codespaces is a cloud-based development environment offered by GitHub that allows developers to write, build, test, and debug code directly within their web browser or in Visual Studio Code (VS Code).

To help you get started, CPython contains a devcontainer folder (https://github.com/python/cpython/tree/main/.devcontainer) with a JSON configuration file that provides consistent and versioned codespace configurations for all users of the project. It also contains a Dockerfile that allows you to set up the same environment but locally in a Docker container if you’d prefer to use that directly.

Create a CPython codespace¶ (https://devguide.python.org/getting-started/setup-building/#create-a-cpython-codespace)

Here are the basic steps needed to contribute a pull request using Codespaces. You first need to navigate to the CPython repo (https://github.com/python/cpython) hosted on GitHub.

Then you will need to:

Launch the codespace

Press the `,` key to launch the codespace setup screen for the current branch

For the default dev container (which is what you very likely want), click the green Create new codespace button

For alternative containers, click Change options and choose the appropriate container

Alternatively, click the green Code button and choose the codespaces tab

For the default dev container (which is what you very likely want), click the green Create codespace on main button

For alternative containers, go to the … menu and choose New with options…

A screen should appear that lets you know your codespace is being set up. (Note: Since the CPython devcontainer is provided, codespaces will use the configuration it specifies.)

A web version of VS Code (https://vscode.dev/) will open inside your web browser, already linked up with your code and a terminal to the remote codespace where CPython and its documentation have already been built.

Use the terminal with the usual Git commands to create a new branch, commit and push your changes once you’re ready!

If you close your repository and come back later you can always resume your codespace by navigating to the CPython repo, selecting the codespaces tab and selecting your most recent codespaces session. You should then be able to pick up from where you left off!

Use Codespaces locally¶ (https://devguide.python.org/getting-started/setup-building/#use-codespaces-locally)

On the bottom left side of the codespace screen you will see a green or grey square that says Codespaces. You can click this for additional options. If you prefer working in a locally installed copy of VS Code you can select the option `OpeninVSCode`. You will still be working on the remote codespace instance, thus using the remote instance’s compute power. The compute power may be a much higher spec than your local machine which can be helpful.

Using the dev container directly¶ (https://devguide.python.org/getting-started/setup-building/#using-the-dev-container-directly)

If you want more control over the environment, or to work offline, you can use the same container used in GitHub Codespaces (https://devguide.python.org/getting-started/setup-building/#using-codespaces) directly. This is meant for users who have (or want to get) some experience with containers. These instructions assume a Unix-like environment with Docker (https://www.docker.com/) or Podman (https://podman.io/) installed. The instructions also assume you want the default dev container; tweak the commands as appropriate if you want to use an alternative container (e.g. the WASI dev container).

Using the pre-built container image¶ (https://devguide.python.org/getting-started/setup-building/#using-the-pre-built-container-image)

Dev container images (https://github.com/python/cpython-devcontainers/pkgs/container/devcontainer) are available from the GitHub Container Registry (GHCR) account for the Python org (https://github.com/orgs/python/packages).

To run the container and launch a Bash shell, run one of the following commands in a clone of the CPython repository.

Podman

podman run -it --rm --volume $PWD:/workspace:Z --workdir /workspace ghcr.io/python/devcontainer:latest

```

Docker

docker run -it --rm --volume $PWD:/workspace --workdir /workspace ghcr.io/python/devcontainer:latest

```

Note that the container has read/write access to the working directory. You may want to use a separate clone of CPython, or run `makeclean` to remove caches and build output generated for your host OS.

Building yourself¶ (https://devguide.python.org/getting-started/setup-building/#building-yourself)

If you prefer, you can build the container image yourself. In a clone of the cpython-devcontainers repo (https://github.com/python/cpython-devcontainers), build the container and name it `cpython-dev`:

Podman

podman build devcontainer/ --tag cpython-dev

```

Docker

docker build devcontainer/ --tag cpython-dev

```

The same command will update any existing `cpython-dev` container. Run it again from time to time – especially if the container stops working for you.

To run the container and launch a Bash shell, run one of the following commands in a clone of the CPython repository.

Podman

podman run -it --rm --volume $PWD:/workspace:Z --workdir /workspace cpython-dev bash

```

Docker

docker run -it --rm --volume $PWD:/workspace --workdir /workspace cpython-dev bash

```

The same caveats outlined above when running from a container image from GHCR also apply here.
