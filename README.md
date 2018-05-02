# goldclick
Lightweight and fast with small size, higher fill rates, Goldclick SDK is a good monetization increasing tool for developers and your traffic.

1. SDK Import  minSdkVersion>=16  
implementation 'com.goldclick.adcore:adcore:1.0.16'
allprojects {  
repositories {  
   jcenter { url "https://dl.bintray.com/goldclickdev/maven" }
}}
     
2. Proguard-rules  
-keep class com.goldclick.core.model.**{*;}
-keep class com.facebook.ads.**{*;}
-keep class com.google.android.gms.ads.**{*;}
-keep class android.support.v4.util.ArrayMap{*;}

3. Initialization setting  
Add the following code to submenu ”onCreate”of “Application”  
GoldClickAd.init(Context context,String appId);

4. Banner ADs integration  
4.1 Add the following code to XML  
<com.goldclick.core.core.GCAdBanner  
     android:id="@+id/gcAdBanner"  
     android:layout_width="match_parent"  
     android:layout_height="wrap_content"/>

4.2 Calling the following code from java code  
    GCAdBanner gcAdBanner = findViewById(R.id.gcAdBanner);  
    gcAdBanner.loadAd();//ADs loading

5. Interstitial ADs integration  
final GCAdPop gcAdPop = new GCAdPop(context);  
 gcAdPop.setAdListener(new GCAdListener() {  
 @Override  
 public void loadStart() {//ADs loading }  
 @Override  
 public void loadSuccess() {//ADs loading success  gcAdPop.show();//Pop Ads display }  
 @Override  
 public void loadErr(String msg) {//ADs loading error }  
 @Override  
 public void clickAd() {// Click ADs }  
  });  
  gcAdPop.loadAd();

6. Add the following code to “build.gradle”in the layer of APP once conflict occurred in the process of integration(Please notice the red words).  
dependencies {  
...  
configurations.all {  
resolutionStrategy.eachDependency { DependencyResolveDetails details ->  
def requested = details.requested  
if (requested.getGroup().equals("com.android.support") && !requested.getName().contains('multidex')) {
                details.useVersion 'the current version of android support  like 27.0.2'  }  }  }  
 }
