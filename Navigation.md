# ライブラリの導入
implementation "android.arch.navigation:navigation-fragment:1.0.0"  
implementation "android.arch.navigation:navigation-ui:1.0.0"  
implementation "android.arch.navigation:navigation-fragment-ktx:1.0.0"  
implementation "android.arch.navigation:navigation-ui-ktx:1.0.0"  

バージョンは適宜修正

# Navigationの流れ
1. resフォルダの直下にnavigationフォルダを追加
2. navigationフォルダのメニューから、New -> Navigation resource fileでxmlを追加  
このxmlを編集して画面遷移を定義する  
3. Activityのレイアウトファイルに設定する
4. ActivityのonCreate()でセットアップする

## Navigationファイルの例
```
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/aac_practice"
    app:startDestination="@id/aacPracticeMain">

    <fragment
        android:id="@+id/aacPracticeMain"
        android:name="com.example.aacpractice.MainFragment"
        android:label="@string/app_name">

        <action
            android:id="@+id/action_main_to_bottomSheet"
            app:destination="@id/aacPracticeBottomSheet"/>
    </fragment>

    <fragment
        android:id="@+id/aacPracticeBottomSheet"
        android:name="com.example.aacpractice.bottomsheet.BottomSheetPracticeFragment"
        android:label="@string/practice_bottom_sheet"/>
</navigation>
```
## Activityのレイアウトファイルに設定する
```
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <fragment
            android:id="@+id/navHostFragmentAacPractice"
            android:layout_height="match_parent"
            android:layout_width="match_parent"
            android:name="androidx.navigation.fragment.NavHostFragment"
            app:navGraph="@navigation/aac_practice"
            app:defaultNavHost="true" />

    </FrameLayout>
</layout>
```
## ActivityのonCreate()でセットアップする
```
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val navController = findNavController(R.id.navHostFragmentAacPractice)
        setupActionBarWithNavController(navController)
    }

    override fun onSupportNavigateUp()
            = findNavController(R.id.navHostFragmentAacPractice).navigateUp()
}
```

# SafeArgs
```
// Project/build.gradle

buildscript {
    ext.kotlin_version = '1.3.50'
    repositories {
        google()
        jcenter()
        
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.1'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
        classpath "androidx.navigation:navigation-safe-args-gradle-plugin:2.2.1" // here
    }
}
```
```
// App/build.gradle

apply plugin: "androidx.navigation.safeargs"
```
