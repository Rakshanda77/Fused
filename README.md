# Fused Location Service
Create an project with an empty activity.
Step 1: In the build gradle add the following Dependencies.
This is used to take permission for map
    //implementation 'com.google.android.gms:play-services-maps:17.0.0'
    This is used to take permission for location.
    //implementation 'com.google.android.gms:play-services-location:17.0.0'
      Step 2: get a google map key By creating an project in developers.google.com
    In the res folder there is a file name as string.xml.
    put api key in that file.
  <string name="map_key" translatable="false">
AIzaSyCmquTm7fXCFb2Ymkl3iAraQcULSkybNz4
    </string> 
Step 3: Add the require permissions in the andriod_manifest.xml file.
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.INTERNET" />
    
    
