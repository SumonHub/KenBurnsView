# KenBurnsView
The next label photo anim with KenBurns effect

# Gradle Dependency
Step 1. Add the JitPack repository to your build file
Add it in your root build.gradle at the end of repositories:

      allprojects {
          repositories {
            ...
            maven { url 'https://jitpack.io' }
          }
        }
Step 2. Add the dependency
      
      dependencies {
                implementation 'com.github.SumonHub:KenBurnsView:1.0.0'
        }
        
# To-do
      
Step 1. In .xml file-

      <org.sumon.library.KenBurnsView
        android:id="@+id/ken_burns_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
              
Step 2. In your onCreate() method.
 
      protected void onCreate(Bundle savedInstanceState) {
              super.onCreate(savedInstanceState);
              setContentView(R.layout.activity_main);
                 _initializeKenBurnsView();
    }

    private void _initializeKenBurnsView() {
        // KenBurnsView
        final KenBurnsView kenBurnsView = (KenBurnsView) findViewById(R.id.ken_burns_view);
        kenBurnsView.setScaleType(ImageView.ScaleType.CENTER_CROP);
        kenBurnsView.setSwapMs(3750);
        kenBurnsView.setFadeInOutMs(750);

        // ResourceIDs
        List<Integer> resourceIDs = Arrays.asList(SampleImages.IMAGES_RESOURCE);
        kenBurnsView.loadResourceIDs(resourceIDs);
        
          // File path, or a uri or url
          //List<String> urls = Arrays.asList(SampleImages.IMAGES_URL);
          //kenBurnsView.loadStrings(urls);
          
          // MIX (url & id)
          //List<Object> mixingList = Arrays.asList(SampleImages.IMAGES_MIX);
          //kenBurnsView.loadMixing(mixingList);

        // LoopViewListener
        LoopViewPager.LoopViewPagerListener listener = new LoopViewPager.LoopViewPagerListener() {
            @Override
            public View OnInstantiateItem(int page) {
                TextView counterText = new TextView(getApplicationContext());
                counterText.setText(String.valueOf(page));
                return counterText;
            }

            @Override
            public void onPageScroll(int position, float positionOffset, int positionOffsetPixels) {
            }

            @Override
            public void onPageSelected(int position) {
                kenBurnsView.forceSelected(position);
            }

            @Override
            public void onPageScrollChanged(int page) {
            }
        };

        // LoopView
        LoopViewPager loopViewPager = new LoopViewPager(this, resourceIDs.size(), listener);

        FrameLayout viewPagerFrame = findViewById(R.id.view_pager_frame);
        viewPagerFrame.addView(loopViewPager);

        kenBurnsView.setPager(loopViewPager);
    }
}


### Demo
![](https://github.com/SumonHub/KenBurnsView/blob/master/preview/preview.gif)

