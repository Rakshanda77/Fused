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
    
Step 3: In activity_main.xml file edit the front-end by just adding a fragment in the layout.

    Simply add fragment into that file.
    
    <fragment
    
    android:layout_width="match_parent"
    
    android:layout_height="match_parent"
    
    android:id="@+id/map"
    
    android:name="com.google.android.gms.maps.SupportMapFragment"></fragment>
       
      
 Step 4: Our main activity extends fragmentActivity and implements onMapReadyCallBack
       
       //Fragment is used to display map
       
       //Location class is used to show langitude ,logitude means all the geographical things
       
       //FusedLocationProviderClien used to get last location of device.
       
       
Step5: In main function we are just getting last location of user.

callig one function which will display current location of user.
       

//Main function looks like this.

@Override
    protected void onCreate(Bundle savedInstanceState) {
    
        super.onCreate(savedInstanceState);
        
        setContentView(R.layout.activity_main);
        
fusedLocationProviderClient = LocationServices.getFusedLocationProviderClient(this);

GetlastLocation();
}

So Basically we will make changes in three functions:

Step6: In the getLastLocation() function

We are simply trying to call getLastLocation of device.

By adding this we need to give some permissions to get location of device.





private void GetlastLocation() {
        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != 
        
        PackageManager.PERMISSION_GRANTED
               
               
               && checkSelfPermission(Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {

            ActivityCompat.requestPermissions(this, new String[]
            
                    {Manifest.permission.ACCESS_FINE_LOCATION}, request_code);
                    
            return;
        }
        Task<Location> task = fusedLocationProviderClient.getLastLocation();
        
        task.addOnSuccessListener(new OnSuccessListener<Location>() {
        
            @Override
            public void onSuccess(Location location) {
            
                if(location != null){
                
                    mlocation = location;
                    
//                    Toast.makeText(getApplicationContext(), mlocation.getLatitude()+ "" + mlocation.getLongitude(),
//                            Toast.LENGTH_SHORT).show();

                    SupportMapFragment supportMapFragment = (SupportMapFragment) getSupportFragmentManager()
                            .findFragmentById(R.id.map);
                            
                    supportMapFragment.getMapAsync(MainActivity.this);
                }
            }

        });
    }
    
    This function basically used to show few things on map.
    Like Title.
    To zoom the location.
    
    
    
@Override
    public void onMapReady(GoogleMap googleMap) {
    
        mMap = googleMap;
        
        //used to show langitude on map
        
        LatLng latLng = new LatLng(mlocation.getLatitude(),mlocation.getLongitude());
        
        //use to show marker
        
        MarkerOptions markerOptions = new MarkerOptions().position(latLng).title("You are here");
        
        //by making animate factory
        
        // used to zoom camera on your location
        
        googleMap.animateCamera(CameraUpdateFactory.newLatLng(latLng));
        
        googleMap.animateCamera(CameraUpdateFactory.newLatLngZoom(latLng,4));
        
        googleMap.addMarker(markerOptions);
        

        // Add a marker in Sydney and move the camera
        
        mMap.setMyLocationEnabled(true);


    }
    
    
    
    just made a simple call to our current location in switch case:
    
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    
        switch (requestCode) {
        
            case request_code:
            
                if (grantResults.length>0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                
                    GetlastLocation();
                    
                }
                
                break;
                
        }
    }
