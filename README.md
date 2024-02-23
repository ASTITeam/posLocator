
# NLP Location Provider
Network Location Provider can be used in POS devices and smart Android device sdk.

## Supports Android 7 - 14 (Nougat-to-UPSIDE_DOWN_CAKE):
**Systems app tracking cases:**
**Network Location Provider will:**
1. Read data from cellular GNSS information from the App
2. Calculate and parse location information,
3. View and Analyze the carrier phase(if it is present in the log file).

## Install the library
    implementation ("com.github.ASTITeam:poslocator:1.0.0"){ transitive = true }

Or if the library is to be used only for debug builds and not release builds, then

    debugImplementation ("com.github.ASTITeam:poslocator:1.0.0"){ transitive = true }

Add the repository maven URL in the settings.properties or the maven settings, If required to find the repository version:

    repositories 
    {
        google()
        maven {
           url "https://github.com/ASTITeam/poslocator/tree/main/releases/com/github/ASTITeam/poslocator"
        }
    }

## Initialize start and stop location lat/lng's in your class

**Start POS Location Service to capture Location using LocationListener:**

     POSLocationBuilder poslocationBuilder = new POSLocationBuilder(getContext(), CLIENT_TOKEN, new CustomLocationListener() 
      {
            @Override
            public void onLocationChanged(CustomLocation customLoc) {
                printLog("loc","provider: "+location.getProvider()
                        +"latlng: "+location.getLatitude() +","+location.getLongitude()
                        +" accuracy: "+location.getAccuracy() +" time: "+location.getTime(),Color.WHITE);
            }
        });
    //interval in min's min 2 minutes - can be changed based on the configuration - Min should be 2 min
    poslocationBuilder.setIntervalTimeInMins(2);
    poslocationBuilder.startLocationCapture();

**Stop location capturing:**

    poslocationBuilder.stopLocationCapture();

**Last Recorded Location:** (Required to start POSLocationProviderService service to get the last Recorded location)

    POSLocationBuilder.getLocation(getContext());

**For Sample Location fragment initialization:**
    
    LoggerFragment editProfileFragment = LoggerFragment.getInstance("CLIENT_TOKEN");
    fragmentManger.beginTransaction()
    .replace(R.id.logger_fragment, editProfileFragment)
    .addToBackStack(null)
    .commit();
