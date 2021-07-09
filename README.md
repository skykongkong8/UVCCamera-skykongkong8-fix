UVCCamera
=========
## This is optimized version for Windows 10, SDK Android API Level 27, NDK 21, Gradle 7.1.1 
### Updated Date: 2021.07.09
### ONLY FOR TEST PURPOSE, NO COMMERCIAL USE
### Great Appreciation for contribution of [saki4510t](https://github.com/saki4510t), and [komakai](https://github.com/komakai)


library and sample to access to UVC web camera on non-rooted Android device

Copyright (c) 2014-2017 saki t_saki@serenegiant.com

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.

All files in the folder are under this Apache License, Version 2.0.
Files in the jni/libjpeg, jni/libusb and jin/libuvc folders may have a different license,
see the respective files.

How to compile library  
=========
The Gradle build system will build the entire project, including the NDK parts. If you want to build with Gradle build system,

1. make directory on your favorite place (this directory is parent directory of `UVCCamera` project).
2. change directory into the directory.
3. clone this repository with `git  clone https://github.com/skykongkong8/UVCCamera.git`
4. change directory into `UVCCamera` directory with `cd UVCCamera`
5. build library with all sample projects using `gradle build`

It will takes several minutes to build. Now you can see apks in each `{sample project}/build/outputs/apks` directory.  
Or if you want to install and try all sample projects on your device, run `gradle installDebug`.  

Note: Just make sure that `local.properties` contains the paths for `sdk.dir` and `ndk.dir`. Or you can set them as enviroment variables of you shell. On some system, you may need add `JAVA_HOME` enviroment valiable that points to JDK directory.  

KOREAN GUIDELINE
==============
# 1. Introduction
* 먼저, 이 라이브러리의 원본은 [saki4510t](https://github.com/saki4510t)와 branch 수정자 [komakai](https://github.com/komakai)에게 있음을 밝힙니다.
* 이 매뉴얼은 Windows10 환경에서 Gradle 을 사용하여 ‘Google Pixel (Android version 10)’에 설치하는 방법을 다룹니다.
* 아래 적힌 매뉴얼은 이미 수정된 사항이며 komakai의 branch에서 아래의 절차를 따라가면 위 라이브러리와 완벽히 같은 파일을 생성할 수 있습니다.
* **아래 과정을 보고, 각자의 환경에 맞게 수정하여 사용하시길 바랍니다.**
* 주요 부분만 요약한 내용과, 개발 환경에 대해 잘 모르더라도 간단한 코딩 지식만으로 할 수 있도록 상세히 안내한 가이드라인이 구분되어 있습니다.
> * **경고**: 몇 가지 앱은 자체적으로 불안정하거나, 구버전이라 맞지 않는 형식이 있습니다.
> * **경고**: 시작하기 전에, ***가장 중요한 것은 '띄어쓰기가 없으며', '영어' username***을 가지고 시작하는 것입니다.
> * Windows10의 경우 이를 중간에 바꾸는 것이 불가능하므로 향후 다른 프로젝트를 위해서라도 새로운 로컬계정을 생성하는 것을 추천합니다.

# 2. 필요 API와 프로그램
1. [SDK](https://developer.android.com/studio?hl=ko) (최신 Android Studio 를 설치한 후 SDK Platform 을 따로 설치하면 됩니다.)
 * Android 8.1(Oreo) (API Level 27) -target SDK
 * Android 4.0(IceCreamSandwich) (API Level 14) -min SDK
2. NDK (Android Studio 에서 설치)
 * 22.1.7171670
 * 14b 버전을 사용할 필요 없습니다.
3. JDK
 * 예제 내부적으로 JDK_1_8 이 지정되어있습니다. SDK 에 지정된 JDK(jre) 경로를 우선 사용해도 무방합니다.
 * 문제가 생긴다면 [JDK8 을 직접 oracle 에서 설치](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)하여 경로를 지정하거나, JAVA_HOME 환경 변수로 지정합니다.
4. Gradle (Android Studio 에서 설치 가능)
 * Gradle 7.1.1
 * android gradle plugin 4.2.0
 * versionBuildTool 30.0.2
   * gradle plugin 에 맞는 최저 사양 versionBuildTool  

# 3. 요약 절차
### 상기된 API 버전 조합을 준수할 것
### 자세한 경로와 형식은 아래 '매우 상세한 절차'를 참고할 것
1. 프로젝트를 진행할 디렉토리를 생성하고 해당 디렉토리 내부로 들어간다.
2. 아래 Git 커맨드로 파일을 불러온다.
```git
git clone https://github.com/skykongkong8/UVCCamera.git
``` 
3. local.properties 파일을 생성하여 SDK, NDK 경로를 잡아준다.
4. gradle 과 gradle plugin 버전을 잘 확인하여 설정한다.
5. 프로젝트를 gradle build하여 Android로 전환시킨다.
6. PC와 Pixel을 연결한다.
7. RUN으로 App을 설치한다.

# 4. 매우 상세한 절차
### 이는 [komakai-fixes branch](https://github.com/komakai/UVCCamera)에서 수정한 모든 일련의 과정을 적은 것입니다. **코드는 이미 수정되어 있으니**, 상황에 맞는 API Version을 다운로드하여 사용하십시오.
1. 프로젝트를 진행할 디렉토리를 생성하고 해당 디렉토리 내부로 들어간다.
2. 아래 Git 커맨드로 파일을 불러온다.
```git
git clone https://github.com/skykongkong8/UVCCamera.git
```
3. Android Studio 에서 ‘기존 프로젝트 열기’를 통해 **gradle 유형**으로 해당 경로 내부의 UVCCamera-komakai-fixes 를 받아온다. (안쪽 것)  
**편의상 이 디렉토리를 ‘.’ 이라고 표현하겠다**  
> gradle 형식으로 받아오지 않으면, 파일 중 gradle 유형이 아닌 것이 있어 gradle 커맨드로 build 하지 못한다는 메시지가 뜬다.
4. SDK Manager > Appearance & Behavior > System Settings > Android SDK > SDK Platforms 에서 API Level 27, 14 를 설치한다.
5. 같은 창의 SDK Tools 에서 NDK(Side by side), Google Play Licensing Library, Google USB Driver 를 설치한다.
6. 위의 API 버전들을 확인하고, File > Project Structure > SDK Location 에서 그에 맞게 프로그램 버전과 경로를 설정한다.
* 이때, local.properties 파일에 직접 저장해야 할 수 있다.  
이 경우 ./local.properties 파일을 새로 생성하고 sdk 와 ndk 의 경로를 각각 아래의 “형식”으로 적는다. (역슬래시의 위치와 개수에 유의, 각자에게 맞는 경로를 입력할 것)
```java
sdk.dir=C\:\\Users\\username\\AppData\\Local\\Android\\Sdk
ndk.dir=C\:\\Users\\username\\AppData\\Local\\Android\\Sdk\\ndk\\22.1.7171670
```
7. File > Project Structure > Modules > Properties/Default Config 모두에서 각각의 SDK/NDK Version 과 Target SDK Version(27), Min SDK Version(14)을 설정한다.
8. File > Settings > Build, Execution, Deployment > Build Tools > Gradle 이나, File > Project Structures > Project 에서 사용할 Gradle 버전을 GUI 상으로 지정할 수 있다.
* 그러나 코드상으로 직접 지정하는 것 또한 가능하다. (그리고 이번 프로젝트의 경우 이를 권장하고 있다.)  
  가장 head 의 .\gradle\gradle-wrapper.properties 에서 gradle 버전을 아래와 같이 지정하고
```java
distributionUrl=https\://services.gradle.org/distributions/gradle-7.1.1-bin.zip
```
* 가장 head 의 .\build.gradle 에서 아래와 같이 android plugin과 versionBuildTool을 지정할 수 있다.
```java
classpath 'com.android.tools.build:gradle:4.2.0'
versionBuildTool = '30.0.2'
```
* [여기](https://developer.android.com/studio/releases/gradle-plugin?hl=ko)에서 호환되는 gradle 과 plugin 버전을 확인할 수 있다.  
  더 낮은 gradle 버전을 사용하고 싶다면 참고하면 된다.
* 그러나 java 버전과 호환되는 gradle 을 사용하여야 하기 때문에 3.5.1 이하로 낮추어서는 안 된다.  
  또, 이에 맞는 versionBuildTool 또한 맞춰주어야 한다. (자동으로 Android Studio 에서 알려줌)
9. 우리가 사용하는 Google Pixel 은 64 비트를 사용한다.  
따라서, .\libuvccamera\src\main\jni\UVCCamera\Application.mk 에서 APP_ABI 를 아래와 같이 수정한다.  
```java
APP_ABI := armeabi-v7a arm64-v8a
```
10. 각 예제별로 '예제'\src\main\AndroidManifest.xml 파일이 있다.  
    여기 나오는 theme 방식이 너무 구버전이라 업데이트 버전을 사용해야한다. 아래와 같이 바꾸어준다.
```java
android:theme="@style/Theme.AppCompat
```
11. 프로젝트를 build 하여 Android 앱으로 전환시킨다.
12. Google Pixel 의 Settings > About Phone > Build Number 를 연타하면 개발자 모드로 전환할 수 있다.
* 이후 Settings > System > Advanced > Developer options > USB debugging 을 활성화시킨다.
13. PC - Pixel 연결하기
* 방법 1: 물리적 연결
  * C 타입 케이블로 연결하면 Android Studio 에 기기가 인식된다.
* 방법 2: wifi 다이렉트 *(통상 Android 11 이상을 권장하지만, 해도 된다.)*
  * PC 와 Google Pixel 을 같은 wifi 에 연결한 뒤, CMD 창에 아래와 같이 입력한다.
    * 만약 adb가 없다면 환경 변수에서 추가하면 된다. SDK가 설치되면서 자동으로 설치되었을 것이기 때문이다.
```bash
adb tcpip 5555
adb connect 'device_ip_address'
```
  * 그 후 진행되는 Logcat 을 보고 싶다면 CMD 에서
```bash
adb logcat
```
* [더 자세한 안내](https://developer.android.com/studio/command-line/adb?hl=ko)
* wifi 다이렉트로 연결하면 외부 카메라와 물리적 연결을 하였을 때 발생하는 오류
메세지도 볼 수 있으므로 더욱 편리하다.
14. RUN
* Logcat 에서 adb 관련 메시지를 확인할 수 있다.
15. 애플리케이션이 설치된다. 카메라로 잘 작동하는지 확인한다.

# 5. 도움이 될 만한 기타 Error 해결 방법
* Using insecure protocols with repositories, without explicit opt-in, is unsupported.
  * 모든 maven 마다 아래와 같은 allowInsecureProtocol = true를 추가한다.
  * Maven은 가장 head의 .\build.gradle 파일 내부에 있다.
```java
maven { url 'https://maven.google.com'
allowInsecureProtocol = true}
```
* jcenter() 관련 경고
  * Gradle 8.0 부터 지원하지 않는다는 경고이다. 현재의 경우 심각한 에러는 아니므로 넘기거나, mavencentral()로 대체하면 된다.
* java.lang.NullPointerException
  *  너무 많은 원인이 있을 수 있지만, .\.gradle 디렉토리를 삭제하고 재실행해보기를 권장한다. 캐싱 과정에서 꼬여서 그런 경우가 있다고 한다.
* SDK CMD에서 깨진 오류 메세지
  * 대부분 경로 문제일 확률이 높다. 경로에 한글이나 띄어쓰기가 없는지 확인하자.
* 'Finished with non-zero exit value 1' 또는 'Keystone 경로/유형/형식 이 invalid 함'
  * 역시 경로 문제일 가능성이 높다. 경로 내 한글이나 띄어쓰기가 없나 확인하자.
* [여기](https://github.com/saki4510t/UVCCamera/issues)에서 검색하여 참고한다.
