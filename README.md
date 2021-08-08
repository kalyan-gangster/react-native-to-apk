# react-native-to-apk-and-aab

 1. ```keytool -genkeypair -v -storetype PKCS12 -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000``` This code will create a Keystore file ( finish the formalities  ).
 2. then place this keystore file in `android/app`.
 3. Next, add the following lines to `android\app\build.gradle` 
```...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')) {
                storeFile file(MYAPP_UPLOAD_STORE_FILE)
                storePassword MYAPP_UPLOAD_STORE_PASSWORD
                keyAlias MYAPP_UPLOAD_KEY_ALIAS
                keyPassword MYAPP_UPLOAD_KEY_PASSWORD
            }
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```

4. Add the following lines to `gradle.properties`
```MYAPP_RELEASE_STORE_FILE=my-key.keystore  
MYAPP_RELEASE_KEY_ALIAS=my-key-alias  
MYAPP_RELEASE_STORE_PASSWORD=******  
MYAPP_RELEASE_KEY_PASSWORD=******
```
5. `cd android`if needed 
### apk
  - For cmd,  `gradlew assembleRelease`
  - For powershell,  `./gradlew assembleRelease`
### aab
  - For cmd,  `gradlew bundleRelease`
  - For powershell,  `./gradlew bundleRelease`

### end
