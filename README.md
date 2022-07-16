# What I've learned

- ## Chapter 3
  - How to handle StatusBar in both ios and android
  - How to import images
  - Image's sizes depend on device's ppi
  - How to style image's sizes
  - KeyboardAvoidingView
  - Touchable Components
  - OS detect

- ## Chapter 4
  - FlatList
  - Useful library for font and svg -> `react-native-vector-icons`
  - AsyncStorage is key-value paired storage that can be used in react-native
    - It is similar to localStorage on browser but it's an async. It returns a Promise.
    - If AsyncStorage handles large data, it decreases the performance.

- ## Chapter 5
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

  - ### Drawer Navigator
    - Drawer Navigator library -> `@react-navigation/drawer`
    - Better performance animation effect library than react-native built-in -> `react-native-reanimated`
    - To recognize user's gesture in drawer navigator library -> `react-native-gesture-handler`
    - `navigation.push` and `navigation.pop` doesn't work with drawer navigator
  
  - ### Bottom Tab Navigator
    - Bottom Tab navigator library -> `react-navigation/bottom-tabs`
    - Set ups for using Icons
      - ***IOS***: configure `ios/{projectName}/Info.plist`
      - ***Android***: configure `android/app/build.gradle`
    - If you use Native Stack and Bottom tab navigator at same time, make sure to put `options={{headerShown: false}}` in Native Stack Screen

  - ### Material Top Tab Navigator
    - Top tab navigator library -> `react-navigation/material-top-tabs`
      - Library for tab implementation in react native -> `react-native-tab-view`
      - `react-native-pager-view`
    - if you use top tab navigator, no need to put `options={{headerShown: false}}` in Native Stack Screen since it doesn't show another header.
  
  - ### Material Bottom Tab Navigator
    - `react-navigation/materials-bottom-tabs`
    - the key difference between material tob tab navigator and bottom is bottom tab navigator can change the background color of whole tab depends on which tab is activated
    - how to sync bottom tab's name with header title name

  - useNavigation, useRoute hooks to use navigation and route objects globally without passing props
  - Even if navigates to other screen, the next screen just stacks up on first screen and the first one doesn't get unmounted (so cannot use useEffect for mount/unmount). In this case, use `useFocusEffect` and make sure use it with `useCallback`.
  

 