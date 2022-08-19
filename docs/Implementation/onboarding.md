# Onboarding Screens

- This document highlights the implementation process of the Onboarding Screens on Wavvy Wallet. 
- The front end of the onboarding screens was implemented uisng the Page View Widget in Flutter. 
- Each screen is based on a simple data model i.e. each has an image, header text and a description. Implementation entailed use of a simple class and a dynamic list generator for each page.

<div class="row">
  <div class="column">
    <img src="../images/designs/onboard1.png">
    <img src="../images/designs/onboard2.png">
    <img src="../images/designs/onboard3.png">
  </div>
</div>

## Notable Functions

### _storeOnboardInfo()

- This function stores information on whether a user has already view the onboarding screens, so as not to show them on the next app launch [1].
  
```dart title="onboard.dart" linenums="1"
 _storeOnboardInfo() async {
    debugPrint("Shared pref called");
    int isViewed = 0;
    SharedPreferences prefs = await SharedPreferences.getInstance();
    await prefs.setInt('onBoard', isViewed);
  }

```

### main()

- Integrations also have to be done in main.dart, since onbaording information needs to be resolved on each app launch [2].

```dart  hl_lines="1 7" title="main.dart" linenums="1"
int? isviewed;
void main() async {
  SystemChrome.setSystemUIOverlayStyle(const SystemUiOverlayStyle(
    statusBarColor: Colors.transparent,
  ));
  WidgetsFlutterBinding.ensureInitialized();
  SharedPreferences prefs = await SharedPreferences.getInstance();
  isviewed = prefs.getInt('onBoard');
  runApp(const MyApp());
  debugPrint('Hello there...');
}
```

!!! note
    Directory with all the onbboarding code : *[lib/app/screens/onboard.dart][1]*

  
## References
1. [Page View Widget - Flutter Official](https://www.youtube.com/watch?v=J1gE9xvph-A)

[1]: https://github.com/sisitech/expense_tracker/blob/ec0b399e4c5f3406ea9d6742e27b74e55bc3f7b9/lib/app/screens/onboard.dart
[2]: https://github.com/sisitech/expense_tracker/blob/6a60113dd7f39a2437574b924f3a9ee6970198e9/lib/main.dart

<style>
    .row {
  display: flex;
  flex-wrap: wrap;
  padding: 0 4px;
}

.column {
  flex: 50%;
  padding: 0 4px;
}

.column img {
  margin-right: 8px;
  vertical-align: middle;
}
</style>