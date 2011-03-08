Barcode Scanner For Appcelerator Titanium
=========================================

This is a small barcode scanner module you can use together with [Titanium Appcelerator](http://appcelerator.com) on an Android device.

Build prerequisites
-------------------

To build the module, there are some dependencies which need to be fulfilled:

- Git
- Titanium Mobile SDK 1.5.0 or above
- Python >= 2.5
- Sun Java SDK 6.0
- Android SDK with Google APIs and SDK version 4 installed
- Ant >= 1.7.1


Build the module
----------------

To build the module, you need to clone our git repository and build the sources with ant:

    # clone the repository
    git clone https://github.com/mwaylabs/titanium-barcode.git
    cd titanium-barcode
    # run ant to build the module
    ant clean && ant

If the build fails, make sure the entries in the buld.properies file point to the right path:

    titanium.platform=/Library/Application Support/Titanium/mobilesdk/osx/1.5.1/android
    android.platform=/opt/android-sdk/platforms/android-4
    google.apis=/opt/android-sdk/add-ons/addon_google_apis_google_inc_4

The newly created *.jar and *.zip files can be found in the dist directory. The module you need is called com.mwaysolutions.barcode-android-$VERSION.zip

Use the module
--------------

- Build the module or download is from the download section
- Place it into your appcelerator project directory
- Add the module to the module section of your tiapp.xml file: <modules><module version="0.2">com.mwaysolutions.barcode</module></modules>
- Use it in your application with require('com.mwaysolutions.barcode');
- Build your project as usual with the Titanium Developer application


The Scanner looks strange on devices with a high resolution screen?!
--------------------------------------------------------------------

If the layout of the scanner activity is not centered, add the following entry to your tiapp.xml:

    <android xmlns:android="http://schemas.android.com/apk/res/android">
        <manifest>
          <supports-screens
            android:smallScreens="true"
            android:normalScreens="true"
            android:largeScreens="true"
            android:anyDensity="true" />
        </manifest>
    </android>


Code Example
------------

    var window = Ti.UI.createWindow({
	    backgroundColor:'white'
    });

    var label = Ti.UI.createLabel();
    window.add(label);
    window.open();

    var titaniumBarcode = require('com.mwaysolutions.barcode');

    titaniumBarcode.scan({
      success: function (data) {
        if(data && data.barcode) {
          var label = Titanium.UI.createLabel({
            text:'Barcode: ' + data.barcode,
            textAlign:'center',
            width:'auto'
          });
          win.add(label);
        } else {
          alert(JSON.stringify(data));
        }
      },

      error: function (err) { 
        alert("Error!! " + err); 
      },

      cancel: function () { 
        alert("cancel"); 
      }
    });

