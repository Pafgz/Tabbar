# Tab bar

A tab bar controller to manage navigation using fragments.

## How to start

### Link the view with the controller
#### In the activity

```kotlin
class MyActivity : Activity(), TabBarController.Delegate {  
    val mTabBarController: TabBarController()
        
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
      
        mTabBarView.listener = tabBarController
    }
}
```
##### Exemple of initialization
```kotlin
private fun initTabBarController() {
        mHomeFragment = HomeFragment()
        
        mOtherFragment = OtherFragment()

        mTabBarController?.clearHistory()
        mTabBarController = TabBarController(
                rootFragments(),
                supportFragmentManager,
                R.id.fragmentContainer)

        mTabBarController?.delegate = this

        mTabBarView.listener = mTabBarController

        tabBarControllerDidShowFragment(homeFragment)
}

private fun rootFragments(): List<Fragment> {
        return listOf(
                mHomeFragment,
                mOtherFragment)
    }
```

#### In the view
```kotlin
class TabBarView(context: Context) : LinearLayout(context) {

    var listener: TabBarViewListener? = null
```

## How to use it

### To switch tab
```kotlin
enum class TabBarState(val index: Int) {
    HOME(0),
    SUGGESTION(1),
    CAMERA(2),
    NOTIFICATION(3),
    PROFILE(4),
}

//In the activity/fragment
tabBarController.switchTab(tabState.index)
```

### To switch fragment 
```kotlin
tabBarController.pushFragment(fragment)
```


### To manage the back button
```kotlin
override fun onBackPressed() {
        if (tabBarController != null && !tabBarController!!.back()) {
            super.onBackPressed()
        }
}
```

