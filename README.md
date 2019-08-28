

<img width="80" style="display: inline;" src="https://filedn.com/lssh2fV92SE8dRT5CWJvvSy/libly/hydride.png" />


# Hydride (Android)

Hydride is an Android encryption library that allows developers to incorporate amazing 
cryptography that is compatible on a wide range of platforms into their projects. 
Hydride uses the [Libhydrogen](https://github.com/jedisct1/libsodium) project via JNA wrapping.

## Installation

Hydride is only available via Jitpack at the moment. Maven and SBT installation instructions available [here](https://jitpack.io/).

```groovy
// Top-level build.gradle
repositories {
    // ...
    maven { url 'https://jitpack.io' } // Add this line
}

dependencies {
    // ...
    implementation 'com.github.libly:hydride-android:0.1.1' // Add this line
    
}
```

## Supported platforms
Unlike other implementations, Hydride **packages the libhydrogen shared libraries** within itself so you don't have to waste time compiling them.
Other implementations probably force you to build those shared libraries or include a build step to build those 
shared libraries which, in my experience, fail most of the time. Platforms that are currently supported:

* Android 16 and above.

## Usage

To get started simple initialise an `Hydrogen` object and use its methods. Here's a simple example to get started:

```java
// Initialise
Native.register(Hydrogen.class, "hydrogen");
Hydrogen hydrogen = new Hydrogen();
hydrogen.hydro_init();

// Make a key
byte[] key = new byte[Hydrogen.HYDRO_SIGN_SECRETKEYBYTES];
hydrogen.hydro_secretbox_keygen(key);

// Make a cipher array to hold the resulting encrypted text
byte[] cipher = new byte[Hydrogen.HYDRO_SECRETBOX_HEADERBYTES + messageBytes.length];
String context = "context1";
byte[] contextBytes = context.getBytes();
String message = "This is a message that will be encrypted.";
byte[] messageBytes = message.getBytes();
long messageId = 1L;

// Now encrypt
int encryptSuccess = hydrogen.hydro_secretbox_encrypt(cipher, messageBytes, messageBytes.length, messageId, contextBytes, key);
```

For more information on how to use please refer to the [Libhydrogen wiki](https://github.com/jedisct1/libhydrogen/wiki) where 
you can find a full list of all available operations. Just use `hydrogen.your_operation_name()` to use them.


## Hydride (Java)
If you are looking for the Java variant of Hydride then look no further, [click here to access Hydride for Java](https://github.com/libly/hydride-java).