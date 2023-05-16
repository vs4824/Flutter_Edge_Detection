# Flutter Edge Detection

A flutter plugin to detect edges of objects, scan paper, detect corners, detect rectangles. It allows cropping of the detected object image and returns the path of the cropped image.

## Usage

### iOS

iOS 10.0 or higher is needed to use the plugin. If compiling for any version lower than 10.0 make sure to check the iOS version before using the plugin. Change the minimum platform version to 10 (or higher) in your ios/Podfile file.

Add below permission to the ios/Runner/Info.plist:

one with the key Privacy - Camera Usage Description and a usage description.
Or in text format add the key:

   ```
   <key>NSCameraUsageDescription</key>
<string>Can I use the camera please?</string>
   ```

### Android

The plugin code is written in kotlin 1.5.31 so the same has to be set to the android project of yours for compilation. Change the kotlin_version to 1.5.31 in your android/build.gradle file.

   ```
   ext.kotlin_version = '1.5.31'
   ```

Change the minimum Android SDK version to 21 (or higher) in your android/app/build.gradle file.

   ```
   minSdkVersion 21
   ```

## Add dependency：

Please check the latest version before installation.

   ```
   dependencies:
  flutter:
    sdk: flutter
  edge_detection: ^1.1.1
  permission_handler: ^10.0.0
  path_provider: ^2.0.11
  path: ^1.8.2
   ```

## Add the following imports to your Dart code

   ```
   import 'package:edge_detection/edge_detection.dart';
   ```

   ```
   // Check permissions and request its
bool isCameraGranted = await Permission.camera.request().isGranted;
if (!isCameraGranted) {
    isCameraGranted = await Permission.camera.request() == PermissionStatus.granted;
}

if (!isCameraGranted) {
    // Have not permission to camera
    return;
}

// Generate filepath for saving
String imagePath = join((await getApplicationSupportDirectory()).path,
    "${(DateTime.now().millisecondsSinceEpoch / 1000).round()}.jpeg");

// Use below code for live camera detection with option to select from gallery in the camera feed.
        
try {
    //Make sure to await the call to detectEdge.
    bool success = await EdgeDetection.detectEdge(imagePath,
        canUseGallery: true,
        androidScanTitle: 'Scanning', // use custom localizations for android
        androidCropTitle: 'Crop',
        androidCropBlackWhiteTitle: 'Black White',
        androidCropReset: 'Reset',
    );
} catch (e) {
    print(e);
}

// Use below code for selecting directly from the gallery.

try {
    //Make sure to await the call to detectEdgeFromGallery.
    bool success = await EdgeDetection.detectEdgeFromGallery(imagePath,
        androidCropTitle: 'Crop', // use custom localizations for android
        androidCropBlackWhiteTitle: 'Black White',
        androidCropReset: 'Reset',
    );
} catch (e) {
    print(e);
}
   ```


