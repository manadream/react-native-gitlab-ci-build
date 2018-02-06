# react-native-gitlab-ci-build
Docker file for building react native applications in Gitlab CI

Based on https://hub.docker.com/r/magiczvn/gitlab-ci-react-native-android/

sample .gitlab-ci.yml:

```
image: jpkrause/react-native-gitlab-ci-build

cache:
  paths:
    - node_modules/
    - .gradle/

stages:
  - build

before_script:
  - export GRADLE_USER_HOME=$(pwd)/.gradle
  - chmod +x ./android/gradlew

build:
  stage: build
  script:
    - npm install --unsafe-perm
    - cd android && ./gradlew assembleDebug --stacktrace
  artifacts:
    paths:
    - android/app/build/outputs/apk
```
