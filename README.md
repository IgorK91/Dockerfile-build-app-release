# Dockerfile-build-app-release
This file build app-release
How to use:
Place Dockerfile in your project folder.
Open CMD.
cd C:\<name folder you project>
docker build -t b:b . 
docker run b:b gradle assembleRelease
docker ps -a // Select the name of your container
docker cp <name of your container>:/usr/local/android-app/app/build/outputs/apk/release/app-release.apk .

Attention!
Before assembly: in you build-gradle-app need to insert
android {
    signingConfigs{
        release{
            keyAlias 'you alias'
            keyPassword 'you password'
            storeFile file('\\key.jks') // path to keys. You key need insert in folder "app" you project
            storePassword 'you password'
        }
    }
    
     buildTypes {
        release {
            minifyEnabled true
            proguardFiles 'proguard-rules.pro', getDefaultProguardFile('proguard-android.txt')
            signingConfig signingConfigs.release
        }
