# iOS and Android apps

This app is built using `Ionic Framework 6`

> If you're new to Ionic, you can get started here: https://ionicframework.com/docs/
>
> Ionic forum: https://forum.ionicframework.com/

At the end of this document you will find a working system report, to help you dig possible build errors.


## Before starting

- You need a working, public (not password protected) `Jobster Theme` installation.

- Make sure that you have installed and configured the `WPJobster Mobile API` plugin that you have received with this source code.


## Required assets

- **Icon**: 1024 x 1024, PNG (24bit color)

	**Optional**: Background and Foreground for Android Adaptive icons.

	> iOS guidelines: https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/app-icon/

	> Android guidelines: https://developer.android.com/google-play/resources/icon-design-specifications

	> Adaptive Icons: https://medium.com/google-design/designing-adaptive-icons-515af294c783

- **Splash** screen: 2732 x 2732, PNG (8bit color)

	> This will be cropped, so make sure that you add some safe margins.

- **Logo**: 300 px height, PNG


## Customizing, compiling and publishing the apps

1. Install NPM dependencies.

		$ npm install

	If you need to check dependencies, run the followowing:

		$ npm list --depth=0

	If you have any issues you can try to remove [./node_modules/](./node_modules/) then try `$ ionic serve`, it will ask for them again.

2. Generate keystore and save the resulting SHA-1 and SHA-256 hashes in order to add them to Firebase on your Android app's settings. Do not lose your keystore password, because you'll lose the ability to update the app in the future.

	Replace `{{myapp}}` with your app name lowercase, like `jobster`, and run:

		$ keytool -genkey -v -keystore {{myapp}}key.keystore -alias {{myapp}}key -keyalg RSA -keysize 2048 -validity 10000

		$ keytool -list -v -alias {{myapp}}key -keystore {{myapp}}key.keystore

3. Create Firebase apps and add iOS and Android platforms.

	For Android, use the generated SHA-1 and SHA-256 from the previous step.

	For iOS, once you create the app on App Store Connect you will have an `App Store ID` and `Team ID`, that you can add to Firebase. (optional)

	3.1. Download `google-services.json` from your Firebase Android app and copy it to the project [root](./) directory.

	3.2. Download `GoogleService-Info.plist` from your Firebase iOS app and copy it to the project [root](./) directory.

    More info: https://capacitorjs.com/docs/apis/push-notifications

4. Copy `icon.png` and `splash.png` to the [./resources/](./resources/) directory.

	4.1. Copy and replace the `icon-foreground.png` and `icon-background.png` in [./resources/android/](./resources/android/) for adaptive icons.

	If you don't want to use adaptive icons, delete the [./resources/android/](./resources/android/) directory and the main icon will be used.

	4.2. Generate all required sizes by running the following:

		$ cordova-res ios --skip-config --copy
        $ cordova-res android --skip-config --copy

    More info: https://capacitorjs.com/docs/guides/splash-screens-and-icons

5. Copy and replace `logo.png` in [./src/assets/images/](./src/assets/images/).

6. Update API URL in the [.env](.env) file. API URL is your website's main URL, like `https://example.com` (no trailing slash). Use [.env.example](.env.example) as a starting point.

	Update appID and appName in [capacitor.config.ts](capacitor.config.ts)

	In [./ios/App/App/info.plist](./ios/App/App/info.plist), update the WKAppBoundDomains property with your own domain name(s).

7. Test in browser by running the following:

		$ ionic serve

8. Build Android:

	The following script will generate the necessary files and will start Android Studio.

		$ npm run android

	Follow the links below for detailed instructions:

	> Developing: https://ionicframework.com/docs/developing/android

	> Publishing: https://ionicframework.com/docs/publishing/play-store

	> Official guidelines: https://developer.android.com/studio/publish/

9. Build iOS:

	The following script will generate the necessary files and will start xCode.

		$ npm run ios

	> Developing: https://ionicframework.com/docs/developing/ios

	> Publishing: https://ionicframework.com/docs/deployment/app-store

	> Official guidelines: https://developer.apple.com/ios/submit/


## iOS Screenshots Requirements

- 6.5 inch (1242 x 2688 pixels) (iPhone 12 Pro Max, iPhone 11 Pro Max, iPhone 11, iPhone XS Max, iPhone XR)

- 5.5 inch (1242 x 2208 pixels) (iPhone 8 Plus, iPhone 7 Plus, iPhone 6s Plus)

- 12.9 inch (2048 x 2732 pixels) (iPad Pro (4th generation, 3rd generation))

- 12.9 inch (2048 x 2732 pixels) (2nd generation iPad Pro)


## Updating

- Merge the newer source code

- Make sure that your dependencies are up to date. If needed, remove [./node_modules/](./node_modules/) and [package-lock.json](package-lock.json), then re-run:

		$ npm install

- You may have to remove the platforms and generate them again if there are any issues


## System report

Other versions may work, so these are not strict requirements, but we have built successfully with the following:

	$ ionic info

	Ionic:

		Ionic CLI       : 6.20.1 (/usr/local/lib/node_modules/@ionic/cli)
		Ionic Framework : @ionic/vue 6.3.0

	Capacitor:

		Capacitor CLI      : 4.3.0
		@capacitor/android : 4.3.0
		@capacitor/core    : 4.3.0
		@capacitor/ios     : 4.3.0

	Utility:

		cordova-res : not installed globally
		native-run  : 1.7.1

	System:

		NodeJS : v16.13.2 (/usr/local/bin/node)
		npm    : 8.3.1
		OS     : macOS Monterey
