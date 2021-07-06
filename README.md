

[![Build Status](https://img.shields.io/badge/platform-android-green)](https://img.shields.io/badge/platform-android-green)
[![Build Status](https://img.shields.io/badge/type-library-blue)](https://img.shields.io/badge/type-library-blue)
[![Licence](https://img.shields.io/cocoapods/l/LivenessSDKOnline?color=red&logo=red)](https://img.shields.io/cocoapods/l/LivenessSDKOnline?color=red&logo=red)


# LivenessOfflineSDk
## 📜 Introduction
Brought to you by FaceX.io, LivenessOfflineSDk Android can now be used to integrate offline liveness Detection by Motion/gesture into your Android applications

## 🔧 Functioning
This LivenessOfflineSDk is Liveness based on Motion detection. Users will be directed by the screen to perform facial gestures and actions which will be analyzed to verify and identify live visitors. 

## 📑 Index
* [Documentation](#-documentation)
* [Features](#-features)
* [Installation](#-installation)
  * [AAR](#using--aar--android-archive)
* [How to use](#-how-to-use)
* [Interface](#-interfaces)
   * [LivenessListener](#livenesslistener)
* [Customization](#-customization)
  * [Steps](#steps)
  * [Thersholds](#-Thresholds)  
* [Supported OS & SDK Versions](#-supported-os--sdk-versions)
* [License](#-license)

## 📚 Documentation 

- Step 1: Sign up for a developer account through [FaceX User Portal](https://search.facex.io/#/register)
- Step 2: Navigate to Plans & Payments Tab & Select  [Plans](https://search.facex.io/#/home/payments/plans)
- Step 3: Scroll down to Mobile SDKs and Select Active Liveness
- Step 3: Purchase a plan matching your license requirement after adding required details 
- Step 4: Navigate to Mobile SDK Tab & Select [License History](https://search.facex.io/#/home/mobilesdk/license)
- Step 5: Download the json file for Android SDK from the offline license Section
- Step 6: Download the Offline Active Livenesss Android SDK from this Github [LivenessSDKOffline](https://github.com/teamfacex/LivenessSDK-Android)
- Step 7: Add the JSON file from the portal to your project.

## 🌟 Features
- Supports Android 5.0+


## 📲 Installation
* Requires Java8 support/ gradle plugin 3+

#### Using [ AAR  (Android Archive)](https://developer.android.com/studio/projects/android-library)

An **AAR file** contains a software library used for developing Android apps. It is structurally similar to an . APK **file** (Android Package), but it allows a developer to store a reusable component that can be used across multiple different apps. To integrate AAR  into your android project:
- Purchase Active Liveness SDK license from [facex portal](https://search.facex.io).
- Download the `file.json` config file from the portal. Make sure file name is `file.json`.
- Create `assets` directory in the android project ( if not already there) and copy the downloaded `file.json` to `assets` directory.
- Download the latest `liveness.aar` release from [here](https://github.com/teamfacex/LivenessSDK-Android/releases/latest/download/liveness.aar).
- Open android studio and add the liveness SDK to your android project
  - Click  `File > New > New Module`.
  - Click `Import .JAR/.AAR Package` from repo directory then click `Next`.
  -  Enter the location of the `liveness.aar` file in the cloned directory then click `Finish`
- Make sure the library is listed at the top of your `settings.gradle` file, as shown here for a library named "liveness":
  -  `include ':app',  ':liveness'`
 - Open the app module's `build.gradle` file and add a new line to the `dependencies` block as shown in the following snippet:
   - `dependencies { implementation project(":liveness")  }`

## 🐒 How to use
- Make sure to get the camera permission.
```
if (ContextCompat.checkSelfPermission(
                this,
                Manifest.permission.CAMERA
            ) != PackageManager.PERMISSION_GRANTED
        ) {

            if (ActivityCompat.shouldShowRequestPermissionRationale(
                    this,
                    Manifest.permission.CAMERA
                )
            ) {


            } else {
                ActivityCompat.requestPermissions(
                    this,
                    arrayOf(Manifest.permission.CAMERA),
                    1
                )
            }

        } else {

        }
override fun onRequestPermissionsResult(requestCode: Int,
                                            permissions: Array<String>, grantResults: IntArray) {
        when (requestCode) {
            1 -> {
                // If request is cancelled, the result arrays are empty.
                if ((grantResults.isNotEmpty() && grantResults[0] == PackageManager.PERMISSION_GRANTED)) {
//                    liveness.startLiveness()
                }
                return
            }

        }
    }
```
#### Kotlin

``` 
import io.facex.liveness.Liveness  
import io.facex.liveness.LivenessListener

class MainActivity : AppCompatActivity(),LivenessListener{
   
private lateinit var liveness: Liveness

 override fun livenessError(live: Boolean?, errorMessage: String?) {   
}  

override fun livenessSuccess(live: Boolean?,bitmap : Bitmap) {  
 
}
override fun onCreate(savedInstanceState: Bundle?) {
	liveness= Liveness(this, R.id.fragment_holder)
	liveness.Eyes=true
	liveness.Mouth=true
	....
	liveness.startLiveness()
  }
}
```

#### Java

```
import io.facex.liveness.Liveness  
import io.facex.liveness.LivenessListener

public class Mainactivity extends AppCompatActivity implements LivenessListener{
  private Liveness liveness;

  @Override
  public void livenessError(Boolean live,String errorMessage){

  }

  @Override
  public void livenessSuccess(Boolean live,Bitmap bitmap){    
    
  }

  @Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
      liveness= new Liveness(this, R.id.fragment_holder);
	    liveness.Eyes=true;
	    liveness.Mouth=true;
	    ....
	    liveness.startLiveness();
   }
}
```

##### layout file for fragment

```
liveness.startLiveness() creates a fragment, so it needs a view to bind the fragment.
Pass in the id of the fragment container using the liveness constructor.
eg: fragment_holder


<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/fragment_holder"
    android:background="@color/black"
    tools:context=".MainActivity">

    .............................
    
</androidx.constraintlayout.widget.ConstraintLayout>
```

## Interfaces

#### LivenessListener 

```
Kotlin

override fun livenessSuccess(live: Boolean?,bitmap : Bitmap) {
  }
  
 override fun livenessError(live: Boolean?, errorMessage: String?) {
  }

Java
  @Override
  public void livenessError(Boolean live,String errorMessage){

  }

  @Override
  public void livenessSuccess(Boolean live,Bitmap bitmap){    
    
  }
```

## 🎛 Customization

You can set some properties for liveness.

#### Steps

|Steps|Value|Default| 
|-------|-------|-------| 
|**Eyes**|`Boolean`|`true`| 
|**Mouth** |`Boolean`|`true`| 
|**Yaw**|`Boolean`|`true`| 
|**Random** |`Boolean`|`true`| 


#### Thresholds

|Property|Values|Default| 
|-------|-------|-------| 
|**EYE_THRESHOLD**|`0.0 ... 6.0`|`2.6`| 
|**MOUTH_THRESHOLD**|`2.0 ... 9.0`|`6.0`| 
|**TIMER**|`Seconds`|`5 seconds`| 
|**MAX_TIMER**|`Seconds`|`15 seconds`|




## 📋 Supported OS & SDK Versions
* Android 5.0+
* Java 8

## 👮🏻 License

- [EULA](https://github.com/teamfacex/LivenessSDK-Android/blob/master/LICENCE)
