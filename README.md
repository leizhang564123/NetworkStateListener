How do you use it?
To get a Git project into your build:
Step 1. Add the JitPack repository to your build file
Add it in your root build.gradle at the end of repositories:

  allprojects {
	repositories {
		
		maven { url 'https://www.jitpack.io' }
		}
	}
Step 2. Add the dependency

	dependencies {
	        implementation 'com.github.leizhang564123:NetworkStateListener:v1.0.0'
	}
Step 3.AndroidManifest.xml  add permission：
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
Step 4.Initialization in your Application：
NetworkManager.getInstance().init(this);
Step 5.use in your activity or fragment：
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
      
        NetworkManager.getInstance().registerObserver(this);
    }

    @NetWork(netType = NetType.AUTO)
    public void network(NetType netType) {
        switch (netType) {
            case WIFI:
                Log.e(Constants.LOG_TAG, "wifi");
                break;
            case CMNET:
            case CMWAP:
                Log.e(Constants.LOG_TAG, "4G");
                break;
            case AUTO:
                break;
            case NONE:
                Log.e(Constants.LOG_TAG, "no network");
                break;
            default:
                break;
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
       
        NetworkManager.getInstance().unRegisterObserver(this);
    }
