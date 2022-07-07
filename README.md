#  Firebase Integration with React Native
## Configuring a Firebase Project

To start a new Firebase app with a frontend framework or a library, you need the API keys. To obtain these API keys, you need access to a Firebase project. A new Firebase project is created from the Firebase console.



- click on the Add project button and then enter the name of the Firebase project.
- click the Continue on the step 2 screen.
- On the step 3 screen, you can leave everything as default and press the Create project button to create a new Firebase project.
✨When the loading finishes, press the button and you’ll be welcomed by the main dashboard screen of the Firebase project. ✨

## Adding Firebase to a React Native project

The react-native-firebase library is the officially recommended collection of packages that brings React Native support for all Firebase services on both Android and iOS apps.

To add it to our existing React Native application, we need to install the following dependency:
```sh
yarn add @react-native-firebase/app
```

To connect the iOS app with your Firebase project’s configuration, you need to generate, download, and add a GoogleService-Info.plist file to the iOS bundle.

- From the Firebase dashboard screen, click on Project Overview > Settings and in the General tab, go to Your Apps section. Click on the Add app button.
- Select iOS in the modal and then, in step 1, enter your app details and click the Register app button.
- In step 2, download the
```sh
GoogleService-Info.plist file.
```
- Then, using Xcode, open the projects
- Right-click on the project name and "Add files" to the project:
- Select the downloaded GoogleService-Info.plist file from your computer, and ensure the "Copy items if needed" checkbox is enabled.
- To allow Firebase on iOS to use the credentials, the Firebase iOS SDK must be configured during the bootstrap phase of your application.

- Open the  file and, at the top of the file, add:
```sh
#import <Firebase.h>
```
Within the same file, add the following at the top of the [ didFinishLaunchingWithOptions ]  function:
```sh
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
  if ([FIRApp defaultApp] == nil) {
    [FIRApp configure]; 
  }
// … the rest of the function body remains the same
```

Next, rebuild the iOS app. Execute the following commands:
```sh
cd ios/ 
pod install --repo-update 
cd .. 
npx react-native run-ios
```
## Android
- To connect the Android app to your Firebase project’s configuration, you need to generate, download and add a google-services.json file to the iOS bundle.

- From the Firebase dashboard screen, click on Project Overview > Settings and in the General tab, go to the “Your Apps” section. Click on the Add app button and then click the button with the Android icon in the modal.

- In Step 1, enter the details of your app and then click the button “Register app”.

- The "Android package name" in the image below, must match your local projects package name which can be found inside of the manifest tag within the /android/app/src/main/AndroidManifest.xml file within your project.
- In step 2, download the google-services.json file and place it inside of your React Native project at the following location: /android/app/google-services.json.

- To allow Firebase on Android to use the credentials, the google-services plugin must be enabled on the project. This requires modification to two files in the Android directory. Add the google-services plugin as a dependency inside of your /android/build.gradle file.
```sh
buildscript {
  dependencies {
    // ... other dependencies
    // Add the line below 
    classpath 'com.google.gms:google-services:4.3.8'
  }
}
```
- Lastly, execute the plugin by adding the following to your /android/app/build.gradle file:

```sh
apply plugin: 'com.android.application'
apply plugin: 'com.google.gms.google-services' // <- Add this line

```

Next, rebuild the android app. Execute the following commands:
```sh
npx react-native run-android
```


