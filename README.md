# faf

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
#   B u b b l e S h i e l d 
 
# This app is security based app. It is espically made for University and high school students for their safety.

We have used firebase for the backend. You need to download some package:
firebase_auth_version
firebase_option_version
firbase_core_Verison (if needed)

Remember: Minimum SDK version should be less then 21(android/app/build.gradle). Don't forgot to download firebase_options.dart form firebase while initializing.

insert : dependencies {
implementation(platform("com.google.firebase:firebase-bom:32.5.0"))
implementation("com.google.firebase:firebase-analytics")
}

apply plugin: 'com.google.gms.google-services'

you will get plugins in your firebase.

at your build.gradle inside android/app/build.gradle.

Check the latest version of Kotlin : ext.kotlin_version = '1.9.20' location: android/build.gradle and check the dependency in the same location :

dependencies {
classpath 'com.android.tools.build:gradle:7.3.0'
classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
classpath 'com.google.gms:google-services:4.4.0'

    }

You will get one of the dependency from firebase.

For Authentication process add this in your main.dart. IT checks if the user is login or not and initialize firebase into your app.

final FirebaseAuth \_auth = FirebaseAuth.instance;

void main() async {
WidgetsFlutterBinding.ensureInitialized();
await Firebase.initializeApp(
options: DefaultFirebaseOptions.currentPlatform,
);

// listen for authentication state changes
FirebaseAuth.instance.userChanges().listen((User? user) {
if (user == null) {
print('User is currently signed out!');
} else {
print('User is signed in!');
}
});

runApp(MyApp());
}

This code if the user has already created account or not. If the User inforamtion is correct you can nagigate to neaxt screen or you can ask user to create new account.

Future<void> \_createUserWithEmailAndPassword() async {
try {
UserCredential userCredential =
await \_auth.createUserWithEmailAndPassword(
email: \_emailController.text,
password: \_passwordController.text,
);

      // User created successfully, navigate to the next screen or perform other actions.
      print('User created successfully! UID: ${userCredential.user?.uid}');

      // Navigate to the next screen.
      Navigator.pushReplacement(
        context,
        MaterialPageRoute(
            builder: (context) =>
                NextScreen()), // Change NextScreen to the actual next screen
      );
    } catch (e) {
      // Handle errors, such as displaying an error message to the user.
      print('Error creating user: $e');
      _showErrorAlert(context, 'Error: $e');
    }

}

You can ask user to create new account and allow them to login intp your app.

Future<void> \_signIn() async {
try {
await \_auth.signInWithEmailAndPassword(
email: \_emailController.text,
password: \_passwordController.text,
);
Navigator.pushReplacement(
context,
MaterialPageRoute(builder: (context) => DrawerScreen()),
);
} catch (e) {
print('Error: $e');
\_showErrorAlert(context, 'Error: $e');
}
}

For change notifier. download the packager provider and edit this in you main the dart

class MyApp extends StatelessWidget {
const MyApp({super.key});

@override
Widget build(BuildContext context) {
return MultiProvider(
providers: [
ChangeNotifierProvider(create: (_) => messageScreenProider())
],
child: MaterialApp(
debugShowCheckedModeBanner: false,
title: 'Bubble_Shield',
theme: ThemeData(
colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
useMaterial3: true,
),
home: SignInScreen(),
));
}
}

Check message_Screen_Provider.dart for ChangeNotifier.

Other are just implimenting the change notifier. Check the code to learn more.

Follow me on : Linkedin: https://www.linkedin.com/in/sambhav-poudel-70688b291/
GitHub: https://github.com/poudelef
Instagram: https://www.instagram.com/sambhavpoudel/

 
