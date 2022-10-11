# applovin-ad-implementatio


//////===================================================================
Do you want to know the Applovin ad implementation process? If you wish to implement the Applovin ad on your android phone then you are in right place. I will guide you in implementing Applovin Banner and Interstitial Ads in this tutorial. So let’s stat
1. Add Applovin SDK to your project
First of all, add the following dependency on your project. For this go to your build. gradle file and add the dependency on dependency section. Then click sync. It will take some minutes to add this SDK. Note that must enable the internet connection on your PC.
implementation 'com.applovin:applovin-sdk:+'

2. Add Applovin SDK key
Basically SDK key is one kind of app id. In AdMob or Facebook, we see a separate App ID for every app. But In Applovin We can find only one App id that’s name is SDK key. To find your SDK key-

Log in to your Applovin account Then Click Account
In the Account setting, we will see the Keys option. Click the keys option.
Now at the top, you will see the SDK key. Copy this SDK Key.
After that, copy the following code and paste it into the Manifest file inside the <Application> Tag. Now add the SDK key instead of @string/SDK.

  <meta-data android:name="applovin.sdk.key"
            android:value="@string/sdk"/>
            
            
            3. Applovin Banner Ad implementation process
To implement banner ads we have to work on our java and XML files. XML files are used for design and java files are used to control our ad.

Banner XML files
  
  
   <androidx.appcompat.widget.LinearLayoutCompat
        android:layout_centerHorizontal="true"
        android:layout_alignParentBottom="true"
        android:id="@+id/maxad_container"
        android:layout_width="match_parent"
        android:layout_height="50dp">
    </androidx.appcompat.widget.LinearLayoutCompat>
  
  
Add this XML file to your desired Activity.xml files.


Java code for Banner Ad
Now open your Activity java file and declared an Adview Variable.
private MaxAdView adView;
Then go inside the onCreate Method and initialize the Applovin SDK. After initializing call a user-defined method. Here I am using a method called bannerAd();. You can also write code inside the initialize. Now just copy the code and paste this inside onCreate Method.

 AppLovinSdk.getInstance( this ).setMediationProvider( "max" );
        AppLovinSdk.initializeSdk( this, new AppLovinSdk.SdkInitializationListener() {
            @RequiresApi(api = Build.VERSION_CODES.M)
            @Override
            public void onSdkInitialized(final AppLovinSdkConfiguration configuration)
            {
                // AppLovin SDK is initialized, start loading ads

                interstitialadload();
                bannerAd();
            }
        } );
        
         private void bannerAd() {

        //use your own ad unit id
        adView = new MaxAdView( "40b2b27ba750bb2a", this );

        // Stretch to the width of the screen for banners to be fully functional
        int width = ViewGroup.LayoutParams.MATCH_PARENT;

        // Banner height on phones and tablets is 50 and 90, respectively
        int heightPx = getResources().getDimensionPixelSize( R.dimen.banner_height );

        adView.setLayoutParams( new FrameLayout.LayoutParams( width, heightPx ) );

        // Set background or background color for banners to be fully functional
        adView.setBackgroundColor(getColor(R.color.white));

        ViewGroup rootView = findViewById(R.id.maxad_container );
        rootView.addView( adView );

        // Load the ad
        adView.loadAd();

    }
    
    4. Applovin Interstitial Ad implementation process
For Interstitial ad first of all we have to declare an Interstitial variable. Copy the following variable and paste it outside the onCreate method.

private MaxInterstitialAd interstitialAd;
Now Create a method for loading interstitial ads and call this method from SDK to initialize the method. Here I am creating a method name interstitialadload();. Now paste the following code inside the interstitialadload() method.

 private void interstitialadload() {

        interstitialAd = new MaxInterstitialAd(getResources().getString(R.string.appid), MainActivity.this
        );
        MaxAdListener adListener= new MaxAdListener() {
            @Override
            public void onAdLoaded(MaxAd ad) {
                Toast.makeText(MainActivity.this, "Max ad loaded", Toast.LENGTH_SHORT).show();

            }

            @Override
            public void onAdDisplayed(MaxAd ad) {
                interstitialadload();

            }

            @Override
            public void onAdHidden(MaxAd ad) {

            }

            @Override
            public void onAdClicked(MaxAd ad) {

            }

            @Override
            public void onAdLoadFailed(String adUnitId, MaxError error) {

            }

            @Override
            public void onAdDisplayFailed(MaxAd ad, MaxError error) {

            }
        };
        interstitialAd.setListener(adListener);
        interstitialAd.loadAd();


    }
    For showing interstitial ads I am using a button. When the user clicks this button then an interstitial ad will show. Below is the code for showing the interstitial ad.

 button.setOnClickListener(new View.OnClickListener() {
             @Override
             public void onClick(View view) {
                    if (interstitialAd.isReady()){


                        interstitialAd.showAd();
                    }
             }
         });
         
         
         
         
         This is the process for implementing Applovin Banner And Interstitial ad. I am also providing you with the source of this project. you can download it below.
         
         
         
         
         
         



