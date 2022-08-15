# What I've learned

***REMEMBER:*** If you install library that uses native code, then you need to restart your emulator. (e.g. `yarn android` or `npx pod-install` and `yarn ios`)

### IOS BUILD ERROR
- Sometimes, `yarn ios` doesn't work due to bundle error. In this situation to fix,
    1. First open a project with Xcode, and go to preference. Then, in locations tab, you will see the directory path to Derived Data. Go there, and Delte whole Derived Data folder.
    2. Delete `ios/.xcworkspace`
    3. Delete `Podfile.lock`
    4. pod install again then `yarn ios`
- #### Pod install error
  - On M1 macbook sometimes it shows pod install error. In this case, you need to run all related applications(Xcode, iterm or terminal, and IDE(VScode for me)) in `Rosetta mode` (as far as I know). Still researching not to use in Rosetta mode since it's slow)
- #### Using firebase in ios
  - After you add `GoogleService-Info.plist` in your project folder and build, `FirebaseApp.configure() could not find a valid GoogleService-Info.plist in your project` error pops up. In this case, make sure you add `GoogleService-Info.plist` to ***Build Phases*** in the ***Compile Sources*** section.

- #### react-native-vector-icons ERROR
  - Even when add fonts to Info.plist doesn't work, you need to create Fonts directory under Project in your Xcode, and add .ttf files from `node_modules/react-native-vector-icons/Fonts/`. Then try to build ios again.

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

<details>
  <summary><h3>Chapter 8</h3></summary>
  
  - how to setup firebase for both ios and android
  - Useful library for firebase in react-native -> `@react-native-firebase` and add `/app`, `/firestore`, `/storage`, or what firebase service you wanna use at the end of `@react-native-firebase` but `app` is essential
  - Follow steps that are provided by firebase web page for Android, and for IOS, after you download `GoogleService-Info.plist` and put it into ios folder, follow steps in react native firebase official documentation.
  ---
  - ***Useful Info for Form, TextInput***
    - To hide password in `TextInput`, set `secureTextEntry` props to be true.
    - Better UX for email input, use ```autoCapitalize="none" autoCorrect={false} autoCompleteType="email" keyboardType="email-address"``` props.
      - Most of props' names above are self-explanatory. `keyboardType="email-address` shows `@` in keyboard so that user don't need to press special characters button to choose `@`.
    - `returnKeyType=` props on `TextInput` determines how the return key should look.
  ---
  - `ActivityIndicator` component shows a spinner.
  ---
  - ***FireStore***
    - collection reference has a method called `add` which creates an unique id automatically. If you want to set an id manually, you can use `yourCollectionReference.doc(yourId).set()`.
  ---
  - if login is successful, user would see MainTab screen first, but you can't just use `navigate` or `push` method to show MainTab screen. Because, in screen stack, there is still SignIn screen or SetUpProfile screen so if user swipe screen on IOS or press back button in Android, it will show previous screen.
    - To handle this situation, you can remove some unnecessary screen from RootStack, if some specific conditions are met.(e.g. if this state exists, then show this screen, otherwise show other screens.
  - Libraries for images(camera) -> `react-native-image-picker` or `@react-native-community/cameraroll`
    - In `@react-native-community/cameraroll`, it doesn't show native UI for picking images. You can build your own UI for picking images using react-native.
    - For IOS to use `react-native-image-picker`, you need to edit `ios/{projectname}/Info.plist` file.
  - In `react-native-image-picker`
    - Use `launchCamera(options, callback)`, when you need to use a photo taken by camera right away/
    - Use `launchImageLibrary(options, callback)`, when you need to pick images from gallery.
    - For Android, if you use Google Photo, you need to set `includeBase64` option to be true. Because, later when you upload a photo, there might be a permission error when reading a file from uri directly. Therefore, for andriod, encode image to base64 and when upload, use the value that is encoded in base64 to process uploading.
  - how to use firebase storage
</details>

<details>
  <summary><h3>Chapter 9</h3></summary>
  
  - In tab(either bottom or top), you might wanna put one stack each to tab, not just one screen component. Because in one tab, you usually have more than one screen.
  - When using firebase auth, you can persist login state by using `auth().onAuthStateChanged` instead of using AsyncStorage.
  - use `useSafeAreaInsets()` to know empty space's sizes
  - `ActionSheetIOS` is UI that let users to choose certain options only in IOS. For Android, you need to make either modal or use `@expo/react-native-action-sheet`. (for creating modal, you can use `Modal` component from react-native)
    - `onRequestClose` is one of Modal component props which gets called when you press back button in Android.
  - To launch image gallery or camera, use `launchImageLibrary` and `launchCamera` from `react-native-image-picker`
  - When layout is complex to use `KeyboardAvoidingView`
    - You can use `Animated` and `addListener` to Keyboard component. (Refer to UploadScreen.js)
    - Set delay to be different by 50 with duration so that it can give a little time not to overlap with keyboard appearing.
      ```
      Animated.timing(animation, {
        toValue: isKeyboardOpen ? 0 : width,
        useNativeDriver: false,
        duration: 150,
        delay: 100,
      })
      ```
  - To show top-right button or Icon, you can use 
    ```
      navigation.setOptions({
        headerRight: () => <IconRightButton onPress={onSubmit} name="send" />,
      });
    ```
    in useEffect, where navigation is from `useNavigation()`

  - In IOS, if you type Enter too much, sometimes texts are off the screen. Then you can use KeyboardAvoidingView with `keyboardVerticalOffset` props.
  - For swiping down refresh feature, you can use `refreshControl` props from FlatList component, and `RefreshControl` component from 'react-native'.
  - if you set `numColumns` props in FlatList component, it shows list in grid.

  - ***FireStore***
    - for `createdAt`, it's better to use `firestore.FieldValue.serverTimestamp()` for precise time.
    - When you call `get()` from collection, it returns QuerySnapshot object.
      - QuerySnapshot object has array called `docs`, an element of docs(one doc) have `data()` method that returns data in doc. However, it doesn't return unique id, so you might have to get it with `doc.id`.
    - you can sort collections by using `collection.orderBy(param1, param2)` where param1 is property name and param 2 is 'desc' or 'asc'.
    - you can limit the amount of 'get' by using `collection.limit(amount)`
    - `collection.startAfter(doc or number)` takes doc or number as a paramter. If it's a doc, it returns docs after the one that is put in parameter. If it's a number, then it returns docs after nth doc.
      - There's also `collection.startAt()`. The difference bewteen startAt and startAfter is if it includes the information given by parameter or not.
    - There's `endBefore` and `endAt` which is the opposite of startAfter and startAt.
    - You can use startAfter or startAt for infiniteScroll, and endBefore or endAt for swiping down for refresh feature.
    - To query with condition, you can use `where()` on collection.
    
  
</details>