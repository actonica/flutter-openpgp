# OpenPGP

Library for use openPGP with support for android, ios, macos, linux, web and hover

## Contents

- [Usage](#usage)
- [Setup](#setup)
  - [Android](#android)
    - [ProGuard](#proguard)
  - [iOS](#ios)
  - [Web](#web)
  - [Linux](#linux)
  - [MacOS](#macos)
  - [Hover](#hover)
- [Example](#example)
- [Native Code](#native-code)

## Usage

## Generate methods
```dart
import 'package:openpgp/openpgp.dart';

var keyPair = await OpenPGP.generate(
      options: Options(
        name: 'test',
        comment: 'test',
        email: 'test@test.com',
        passphrase: "123456",
        keyOptions: KeyOptions(
            rsaBits: 2048,
            cipher: Cypher.aes128,
            compression: Compression.none,
            hash: Hash.sha256,
            compressionLevel: 0,
        ),
      ),
);
```

### Encrypt methods

```dart
import 'package:fast_rsa/rsa.dart';

var bytesSample := Uint8List.fromList('data'.codeUnits)

var result = await OpenPGP.encrypt("text","[publicKey here]");
var result = await OpenPGP.encryptSymmetric("text","[passphrase here]");
var result = await OpenPGP.encryptBytes(bytesSample,"[publicKey here]");
var result = await OpenPGP.encryptSymmetricBytes(bytesSample,"[passphrase here]");

```

### Decrypt methods

```dart
import 'package:fast_rsa/rsa.dart';

var bytesSample := Uint8List.fromList('data'.codeUnits)

var result = await OpenPGP.decrypt("text encrypted","[privateKey here]","[passphrase here]");
var result = await OpenPGP.decryptSymmetric("text encrypted","[passphrase here]");
var result = await OpenPGP.decryptBytes(bytesSample,"[privateKey here]","[passphrase here]");
var result = await OpenPGP.decryptSymmetricBytes(bytesSample,"[passphrase here]");
```

### Sign methods

```dart
import 'package:fast_rsa/rsa.dart';

var bytesSample := Uint8List.fromList('data'.codeUnits)

var result = await OpenPGP.sign("text","[publicKey here]","[privateKey here]","[passphrase here]");
var result = await OpenPGP.signBytesToString(bytesSample,"[publicKey here]","[privateKey here]","[passphrase here]");

```

### Verify methods

```dart
import 'package:fast_rsa/rsa.dart';

var bytesSample := Uint8List.fromList('data'.codeUnits)

var result = await OpenPGP.verify("text signed","text","[publicKey here]");
var result = await OpenPGP.verifyBytes("text signed", bytesSample,"[publicKey here]");

```

## Setup

### Android

#### ProGuard

Add this lines to `android/app/proguard-rules.pro` for proguard support

```proguard
-keep class go.** { *; }
-keep class openpgp.** { *; }
```

### iOS

no additional setup required

### Web

add to you `pubspec.yaml`

```yaml
assets:
  - packages/openpgp/web/assets/wasm_exec.js
  - packages/openpgp/web/assets/openpgp.wasm
```

ref: https://github.com/jerson/flutter-openpgp/blob/master/example/pubspec.yaml

and in you `web/index.html`

```html
<script
  src="assets/packages/openpgp/web/assets/wasm_exec.js"
  type="application/javascript"
></script>
```

ref: https://github.com/jerson/flutter-openpgp/blob/master/example/web/index.html

### Linux (need to upgrade to new linux flutter template, use older version)

add to you `linux/app_configuration.mk`

```make
EXTRA_LDFLAGS=-lopenpgp
```

ref: https://github.com/jerson/flutter-openpgp/blob/master/example/linux/app_configuration.mk

### MacOS

no additional setup required

### Hover

just update your plugins

```bash
hover plugins get
```

## Example

Inside example folder

```bash
cd example && flutter run
```

## Native Code

the native library is made in Golang and build with gomobile for faster performance

https://github.com/jerson/openpgp-mobile
