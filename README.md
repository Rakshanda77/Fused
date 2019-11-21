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
    Edit Andriod Manifesf file and get this tag to make connection.
    <meta-data
            android:name="com.google.android.geo.API_KEY"
        android:value="@string/map_key"/>
    </string> 
Step 3: Add the require permissions in the andriod_manifest.xml file.
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.INTERNET" />
    Step 3:
    In activity_main.xml file edit the front-end by just adding a fragment in the layout.
    Simply add fragment into that file.
    <fragment
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:id="@+id/map"
       android:name="com.google.android.gms.maps.SupportMapFragment"></fragment>
       
       Step 4:
       Our main activity extends fragmentActivity and implements onMapReadyCallBack
       //Fragment is used to display map
       //Location class is used to show langitude ,logitude means all the geographical things
       //FusedLocationProviderClien used to get last location of device.
       
       Step5:
       In main function we are just getting last location of user and callig one function which will display current location of user.
       
       //Main function looks like this.
       @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
fusedLocationProviderClient = LocationServices.getFusedLocationProviderClient(this);
GetlastLocation();
}

Step6:
In the getLastLocation() function

We are simply tryin to call getLastLocation of device.By adding this we need to give some permissions 
to get location of device.

Task<Location> task = fusedLocationProviderClient.getLastLocation();
/This code is just getting permission from andrio manifest file.
and we are updating static variable of location with the current location.

if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED
                && checkSelfPermission(Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            
            ActivityCompat.requestPermissions(this, new String[]
                    {Manifest.permission.ACCESS_FINE_LOCATION}, request_code);
            return;
       
    
    
