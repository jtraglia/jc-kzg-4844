# jc-kzg-4844

[![Build Status](https://circleci.com/gh/Consensys/jc-kzg-4844.svg?style=svg)](https://circleci.com/gh/Consensys/workflows/jc-kzg-4844)
[![GitHub license](https://img.shields.io/github/license/Consensys/jc-kzg-4844.svg?logo=apache)](https://github.com/Consensys/jc-kzg-4844/blob/master/LICENSE)
[![Version of 'c-kzg-4844'](https://img.shields.io/badge/c--kzg--4844-v0.4.0-blue.svg)](https://github.com/ethereum/c-kzg-4844/releases/tag/v0.4.0)
[![Latest version of 'jc-kzg-4844' @ Cloudsmith](https://api-prd.cloudsmith.io/v1/badges/version/consensys/maven/maven/jc-kzg-4844/latest/a=noarch;xg=tech.pegasys/?render=true&show_latest=true)](https://cloudsmith.io/~consensys/repos/maven/packages/detail/maven/jc-kzg-4844/latest/a=noarch;xg=tech.pegasys/)

Provides building and packaging of the [Java bindings](https://github.com/ethereum/c-kzg-4844/tree/main/bindings/java) in [C-KZG-4844](https://github.com/ethereum/c-kzg-4844).

## Dependency

```groovy
repositories {
    maven { url "https://artifacts.consensys.net/public/maven/maven/" }
}

dependencies {
    implementation("tech.pegasys:jc-kzg-4844:<version>")
}
```

## Minimal sample

```java
// load the library once at startup
CKZG4844JNI.loadNativeLibrary();

// once a trusted setup is loaded, all methods will use it
CKZG4844JNI.loadTrustedSetup("trusted-setup.txt");

byte[] blob = ...;
byte[] commitment = CKZG4844JNI.blobToKzgCommitment(blob);
byte[] proof = CKZG4844JNI.computeBlobKzgProof(blob, commitment);

boolean isValidProof = CKZG4844JNI.verifyBlobKzgProof(blob, commitment, proof);

// the current trusted setup should be freed before a new one is loaded
CKZG4844JNI.freeTrustedSetup();
```

## Loading trusted setup

There are two ways to load the trusted setup.

### File
The file needs to be of the following format: [trusted_setup.txt](https://github.com/ethereum/c-kzg-4844/blob/main/src/trusted_setup.txt)

### Method parameters 
Look at the `loadTrustedSetup(byte[], long, byte[], long)` method.

## Supported platforms

- x86-64
    - Windows
    - Linux
    - MacOS
- aarch64
    - Linux
    - MacOS
