# Androidのビルド用のDocker


## Werckerで使う場合

ライブラリのバージョンとかには**注意**

```wercker.yml
box: gupuru/wercker_android:0.3.2

build:
  steps:
    - script:
        name: show base information
        code: |
          gradle -v
          echo $ANDROID_HOME
          echo $ANDROID_SDK_VERSION
          echo $ANDROID_BUILD_TOOLS
          echo $ANDROID_UPDATE_FILTER
    - script:
        name: run gradle
        code: |
          ./gradlew --full-stacktrace -q --project-cache-dir=$WERCKER_CACHE_DIR assembleDebug
  after-steps:
    - script:
        name: inspect build result
        code: |
          cp ./app/build/outputs/apk/*.apk $WERCKER_REPORT_ARTIFACTS_DIR
```
