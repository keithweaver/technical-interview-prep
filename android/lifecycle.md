# What's the Android lifecycle?

*Probably will tell you to draw it*


- onCreate
- onStart
- onResume
- onPause
- onStop
- onDestroy


`onCreate` is called when app opens. Loads the UI. `onStart` is next, I'll get back to this. `onResume` is then called. Then your user is in the app. `onPause` activity leaves the foreground, ex. hit the view open applications but don't minimize or close it. `onStop` is called if you minimize the activity. `onStart` is called if the app is unminized or brought to the front. `onDestroy` is called when you kill the app.


# How do you call onDestroy without calling onPause or onStop?

Call `finish()` from the `onCreate`.


# Difference between a fragment and activity?

An activity is a single focus (sometimes thought as of a window). Activities can implement a fragment. A fragment is a modular component of an activity. Think of the Gmail app, they have an "SingleEmailActivity" with fragment inside that contains aspects for one email. But when you swipe right, a new fragment is created that acts and the same way but is a new instance.


# What are “launch modes”? What are the two mechanisms by which they can be defined? What specific types of launch modes are supported?

- Android Manifest (include the flags as a child)
- On the intent call (add flags)

Some of the launch modes are:
- standard (create a new instance of the activity)
- singleTop (exists, move it to the top)
- singleTask
- clearTop

# Can you create an activity without a UI?

Yes, these are thought as a abstract activities.

# What is the fragment lifecycle?

- onAttach -> onCreateView
- onCreate
- onCreateView
- onActivityCreated
- onStart
- onResume
- onPause
- onStop -> onStart
- onDestroyView -> onCreateView or onDetach
- onDestroy
- onDetach

# What method is only called once during a fragments lifecycle?

`onAttached`

# What is ADB?
ADB stands for Android Debug Bridge. It is a command line tool that is used to communicate with the emulator instance.

# What is ANR?
Application not responding


Source:
- https://www.ntu.edu.sg/home/ehchua/programming/android/images/Android_ActivityLifeCycle.png
- https://www.toptal.com/android/interview-questions
- https://www.javatpoint.com/android-interview-questions
- https://developer.xamarin.com/guides/android/platform_features/fragments/creating-a-fragment/Images/fragment_lifecycle.png
