#JavaCPP FFmpeg Android Builder

Build FFmpeg native libraries for JavaCPP on Android.

This repository provides an Android build environment for compiling the native FFmpeg libraries required by the JavaCPP FFmpeg preset.

The goal is simple:

«Build FFmpeg ".so" libraries that JavaCPP can load and use on Android.»

What This Does

This project builds the native FFmpeg components used by JavaCPP, including libraries such as:

libavcodec.so
libavdevice.so
libavfilter.so
libavformat.so
libavutil.so
libswresample.so
libswscale.so

The resulting libraries are intended to be used together with the JavaCPP FFmpeg Java bindings.

This repository does not build JavaCPP itself and does not provide an Android application.

Why?

JavaCPP's FFmpeg bindings normally rely on native FFmpeg libraries built for the target platform.

Android requires Android-specific native binaries, so the normal desktop FFmpeg binaries cannot simply be used.

This project provides a way to build those FFmpeg libraries specifically for Android.

Supported Android Architectures

The build can target Android architectures supported by the configured Android NDK toolchain.

Typical targets include:

arm64-v8a
armeabi-v7a
x86
x86_64

For modern Android devices, "arm64-v8a" is generally the primary target.

Output

After a successful build, the generated libraries can be organized by Android ABI:

libs/
├── arm64-v8a/
│   ├── libavcodec.so
│   ├── libavdevice.so
│   ├── libavfilter.so
│   ├── libavformat.so
│   ├── libavutil.so
│   ├── libswresample.so
│   └── libswscale.so
│
├── armeabi-v7a/
│   └── ...
│
├── x86/
│   └── ...
│
└── x86_64/
    └── ...

The exact output location depends on the build workflow.

Using With JavaCPP

The generated FFmpeg libraries are intended to be used with the corresponding JavaCPP FFmpeg bindings.

Conceptually, the setup is:

Java application
       │
       ▼
JavaCPP FFmpeg bindings
       │
       ▼
Android FFmpeg .so libraries
       │
       ├── libavcodec.so
       ├── libavformat.so
       ├── libavutil.so
       ├── libavfilter.so
       ├── libavdevice.so
       ├── libswresample.so
       └── libswscale.so

JavaCPP handles the Java-to-native interface while the libraries produced by this repository provide the Android-native FFmpeg implementation.

Native Library Naming

JavaCPP may expect native libraries with its own naming conventions.

For example, a JavaCPP-generated FFmpeg binding may attempt to load a library such as:

jniavutil

rather than directly loading:

libavutil.so

Therefore, the native libraries produced for JavaCPP must be packaged according to the JavaCPP loading configuration being used.

This is important when integrating the resulting libraries into another Android project.

Building

The build uses the Android NDK to cross-compile FFmpeg for Android.

Clone the repository:

git clone https://github.com/whaltermc/javacpp-android-builder.git
cd javacpp-android-builder

The repository's GitHub Actions workflows can be used to perform the Android build automatically.

GitHub Actions

The repository contains GitHub Actions workflows under:

.github/workflows/

The workflow is responsible for setting up the required Android build environment and compiling the FFmpeg native libraries.

This makes it possible to produce Android FFmpeg binaries without requiring the complete Android NDK environment to be manually configured on the local machine.

JavaCPP Compatibility

The generated libraries are intended specifically for use with:

- JavaCPP
- JavaCPP FFmpeg bindings
- Android applications that use JavaCPP FFmpeg

The FFmpeg version and JavaCPP FFmpeg preset version should be kept compatible.

When changing the FFmpeg version, verify that the corresponding JavaCPP FFmpeg bindings support that version.

What This Repository Is Not

This project is not:

- A JavaCPP fork
- An FFmpeg Java binding
- An Android app
- A complete Android application template
- A replacement for JavaCPP
- A replacement for FFmpeg

It is a native FFmpeg build project for JavaCPP on Android.

Related Projects

JavaCPP

"JavaCPP" (https://reference-url-citation.invalid/0)

JavaCPP provides the Java/native interface used by the bindings.

JavaCPP Presets

"JavaCPP Presets" (https://reference-url-citation.invalid/1)

Contains the FFmpeg preset and native build configuration.

FFmpeg

"FFmpeg" (https://reference-url-citation.invalid/2)

The multimedia framework whose native libraries are built by this project.

Credits

Created and maintained by whaltermc.

This project builds upon the JavaCPP/JavaCPP Presets and FFmpeg projects.

License

This repository and the generated FFmpeg binaries are subject to the licenses of their respective components.

See the upstream JavaCPP, JavaCPP Presets, and FFmpeg repositories for their applicable licenses and notices.
