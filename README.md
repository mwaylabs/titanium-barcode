Barcode Scanner For Appcelerator Titanium
=========================================

Build prerequisites
-------------------

To build the module, there are some dependencies which need to be fulfilled:

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
    cd tianium-barcode
    # run ant to build the module
    ant clean && ant

The newly created *.jar and *.zip files can be found in the dist directory.

Use the module
--------------

- Build the module or download is from the download section
- Place it into your appcelerator project directory
- Add the module to the module section of your tiapp.xml file: <modules><module version="0.1">com.mwaysolutions.barcode</module></modules>
- Use it in your application with require('com.mwaysolutions.barcode');


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

