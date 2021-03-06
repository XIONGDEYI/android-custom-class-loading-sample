# android-custom-class-loading-sample
Exported from code.google.com/p/android-custom-class-loading-sample

## Custom Class Loading in Dalvik
[This post is by Fred Chung, who’s an Android Developer Advocate — Tim Bray]

The Dalvik VM provides facilities for developers to perform custom class loading. Instead of loading Dalvik executable (“dex”) files from the default location, an application can load them from alternative locations such as internal storage or over the network.

This technique is not for every application; In fact, most do just fine without it. However, there are situations where custom class loading can come in handy. Here are a couple of scenarios:
- Big apps can contain more than 64K method references, which is the maximum number of supported in a dex file. To get around this limitation, developers can partition part of the program into multiple secondary dex files, and load them at runtime.
- Frameworks can be designed to make their execution logic extensible by dynamic code loading at runtime.

We have created a sample app to demonstrate the partitioning of dex files and runtime class loading. (Note that for reasons discussed below, the app cannot be built with the ADT Eclipse plug-in. Instead, use the included Ant build script. See Readme.txt for detail.)
The app has a simple Activity that invokes a library component to display a Toast. The Activity and its resources are kept in the default dex, whereas the library code is stored in a secondary dex bundled in the APK. This requires a modified build process, which is shown below in detail.
Before the library method can be invoked, the app has to first explicitly load the secondary dex file. Let’s take a look at the relevant moving parts.
Code Organization

The application consists of 3 classes.
- com.example.dex.MainActivity: UI component from which the library is invoked
- com.example.dex.LibraryInterface: Interface definition for the library
- com.example.dex.lib.LibraryProvider: Implementation of the library

The library is packaged in a secondary dex, while the rest of the classes are included in the default (primary) dex file. The “Build process” section below illustrates how to accomplish this. Of course, the packaging decision is dependent on the particular scenario a developer is dealing with.
Class loading and method invocation

The secondary dex file, containing LibraryProvider, is stored as an application asset. First, it has to be copied to a storage location whose path can be supplied to the class loader. The sample app uses the app’s private internal storage area for this purpose. (Technically, external storage would also work, but one has to consider the security implications of keeping application binaries there.) 

## Link
[More Information](http://android-developers.blogspot.jp/2011/07/custom-class-loading-in-dalvik.html)
