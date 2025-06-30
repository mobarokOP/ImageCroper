# ImageCroper - Image Cropping Library for Android

#### This project aims to provide an ultimate and flexible image cropping experience. Made in [Mobarok Hossaim](https://mobarokop.github.io)


<img src="preview.gif" width="800" height="600">

# Usage

*For a working implementation, please have a look at the Sample Project - sample*


1. Include the library as a local library project.

	```
	allprojects {
	   repositories {
	      jcenter()
	      maven { url "https://jitpack.io" }
	   }
	}
	```

    ```  implementation 'com.github.mobarokOP:ImageCroper:1.1' ``` - lightweight general solution

2. Add UCropActivity into your AndroidManifest.xml

    ```
    <activity
        android:name="com.yalantis.ucrop.UCropActivity"
        android:screenOrientation="portrait"
        android:theme="@style/Theme.AppCompat.Light.NoActionBar"/>
    ```

3. The uCrop configuration is created using the builder pattern.

   ```java
   UCrop.of(sourceUri, destinationUri)
       .withAspectRatio(16, 9)
       .withMaxResultSize(maxWidth, maxHeight)
       .start(context);
   ```

4. Override `onActivityResult` method and handle uCrop result.

    ```java
    @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        if (resultCode == RESULT_OK && requestCode == UCrop.REQUEST_CROP) {
            final Uri resultUri = UCrop.getOutput(data);
        } else if (resultCode == UCrop.RESULT_ERROR) {
            final Throwable cropError = UCrop.getError(data);
        }
    }
    ```

5. You may want to add this to your PROGUARD config:

    ```
    -dontwarn com.yalantis.ucrop**
    -keep class com.yalantis.ucrop** { *; }
    -keep interface com.yalantis.ucrop** { *; }
    ```

# Customization

If you want to let your users choose crop ratio dynamically, just do not call `withAspectRatio(x, y)`.

uCrop builder class has method `withOptions(UCrop.Options options)` which extends library configurations.

Currently, you can change:

   * image compression format (e.g. PNG, JPEG), compression
   * image compression quality [0 - 100]. PNG which is lossless, will ignore the quality setting.
   * whether all gestures are enabled simultaneously
   * maximum size for Bitmap that is decoded from source Uri and used within crop view. If you want to override the default behaviour.
   * toggle whether to show crop frame/guidelines
   * setup color/width/count of crop frame/rows/columns
   * choose whether you want rectangle or oval(`options.setCircleDimmedLayer(true)`) crop area
   * the UI colors (Toolbar, StatusBar, active widget state)
   * and more...

# Compatibility

  * Library - Android (API 24) - API 36
  * Sample - Android (API 24) - API 36
  * CPU - armeabi armeabi-v7a x86 x86_64 arm64-v8a (for versions >= 2.1.2)
.

### Version: 1.0

  * Initial Build

### Let us know!

We’d be really happy if you sent us links to your projects where you use our component. Just send an email to github@yalantis.com And do let us know if you have any questions or suggestion regarding the library.

#### Apps using uCrop


## License

    Copyright 2025, Mobarok Hossain

    Software doesn't collect, store or transfer data to Yalantis or third parties.
    Emplacement of this Software is carried out locally at device.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
