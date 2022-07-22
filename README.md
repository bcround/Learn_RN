# What I've learned

***REMEMBER:*** If you install library that uses native code, then you need to restart your emulator. (e.g. `yarn android` or `npx pod-install` and `yarn ios`)

<details>
  <summary><h3>Chapter 3</h3></summary>

  - How to handle StatusBar in both ios and android
  - How to import images
  - Image's sizes depend on device's ppi
  - How to style image's sizes
  - KeyboardAvoidingView
  - Touchable Components
  - OS detect
</details>

<details>
  <summary><h3>Chapter 4</h3></summary>

  - FlatList
  - Useful library for font and svg -> `react-native-vector-icons`
  - AsyncStorage is key-value paired storage that can be used in react-native
    - It is similar to localStorage on browser but it's an async. It returns a Promise.
    - If AsyncStorage handles large data, it decreases the performance.
</details>

<details>
  <summary><h3>Chapter 5</h3></summary>

  - How to stack Screen(page) like web history using library
  - How to naviagate between screens
  - component that being used as a screen can receive objects such as `navigation` and `route`
  - `navigation.navigate` and `navigation.push`
    - They both can pass route parameter.
    - The difference between two is `navigate` doesn't stack the screen when screen is same and only parameter changes. `push` always stack the screen.
    - `push` is available only in native stack navigator.
  - How to customize screen header
    - Change title
    - Style header
  - #### Drawer Navigator
    - Drawer Navigator library -> `@react-navigation/drawer`
    - Better performance animation effect library than react-native built-in -> `react-native-reanimated`
    - To recognize user's gesture in drawer navigator library -> `react-native-gesture-handler`
    - `navigation.push` and `navigation.pop` doesn't work with drawer navigator
  
  - #### Bottom Tab Navigator
    - Bottom Tab navigator library -> `react-navigation/bottom-tabs`
    - Set ups for using Icons
      - ***IOS***: configure `ios/{projectName}/Info.plist`
      - ***Android***: configure `android/app/build.gradle`
    - If you use Native Stack and Bottom tab navigator at same time, make sure to put `options={{headerShown: false}}` in Native Stack Screen

  - #### Material Top Tab Navigator
    - Top tab navigator library -> `react-navigation/material-top-tabs`
      - Library for tab implementation in react native -> `react-native-tab-view`
      - `react-native-pager-view`
    - if you use top tab navigator, no need to put `options={{headerShown: false}}` in Native Stack Screen since it doesn't show another header.
  
  - #### Material Bottom Tab Navigator
    - `react-navigation/materials-bottom-tabs`
    - the key difference between material tob tab navigator and bottom is bottom tab navigator can change the background color of whole tab depends on which tab is activated
    - how to sync bottom tab's name with header title name

  - useNavigation, useRoute hooks to use navigation and route objects globally without passing props
  - Even if navigates to other screen, the next screen just stacks up on first screen and the first one doesn't get unmounted (so cannot use useEffect for mount/unmount). In this case, use `useFocusEffect` and make sure use it with `useCallback`.
</details>
  
<details>
  <summary><h3>Chapter 6</h3></summary>

  - how to plan out screen structure (for small app)
  - uuid library uses Node.js' crypo function which is not included in react-native, so need to install `react-native-get-random-values` library to make uuid work.
  - Useful library for date -> `date-fns`
  - How to use Animation
    - `useNativeDriver` is one of options that can passeed in `Animated.timing` 's second argument.
      - if it's set to true, then the process of animation is handled on native level, not in javascript engine
      - It has to be set false, if the animation affects the layout such as left, width, paddingLeft, marginLeft, etc.
    - use transfrom instead of left or top for better performance
    - use `animation.interpolate()` for appling multipe styles at once using inputRange and outputRange
  - FlatList has `onEndReached` and `onEndReachedThreshold`, and those are for implementing infinite scroll
  - For bouncing animation, use `Animated.spring()`
    - There is several options: tension, friction, speed, bounciness, etc.
    - tension and friction must be used together and speed and bounciness must be used together but cannot combine interchangeably
</details>

<details>
  <summary><h3>Chapter 7</h3></summary>

  - `headerTitle` which is one of options in options props in `Tab.Screen` can take not only string but also jsx.
  - There is two ways to get screen size in dp
    - import `Dimensions` from react-native
      - `Dimensions.get()` can take either 'window' or 'screen'. 'window' gets the size of app's available area. 'screen' gets the size of full screen. In IOS, there's no difference using both, but in Android, 'window' gets the size of area that excludes top status bar and soft menu bar at the bottom.
      - `Dimensions` can work outside of the component so you can use it in StyleSheet.
      - For device rotation or foldable devices, you might need to use addEventListener(listen on change event) and removeEventListener for size changing
    - Or use `useWindowDimensions` hook.
      - no need to handle size changing like `Dimensions`
      - If you need to get the full size of the screen, you have to use `Dimensions.get('screen')`
  - For Calender, you can use library called `react-native-calendars`
  - use `ListHeaderComponent` props in `FlatList` to show the specific component on top of FlatList
  - For date picker, use library -> `react-native-modal-datetime-picker` and `@react-native-community/datetimepicker`
    - `@react-native-community/datetimepicker` gives you date/time picker  that is specialized to each IOS and Android platform.
    - `react-native-modal-datetime-picker` lets you use date/time picker modal component in a convenient way.
  
</details>