# What is an intent?

The `Intent` object is a common mechanism for starting new activity and transferring data from one activity to another.

# 3 common cases for using an intent?

- Starting a activity
- Starting a service
- Delivering a broadcast to a receiver

# Can an intent be used to provide data to the content provider? Why?

However, you cannot start a `ContentProvider` using an Intent.

When you want to access data in a ContentProvider, you must instead use the ContentResolver object in your application’s Context to communicate with the provider as a client. The ContentResolver object communicates with the provider object, an instance of a class that implements ContentProvider. The provider object receives data requests from clients, performs the requested action, and returns the results.

In short: No, you need to request access to data from other content providers (other apps) and wait for the response.

# What's the difference between an intent and pending intent?


# What is an implicit intent used for?

An implicit intent specifies an action that can invoke any app on the device able to perform the action. Using an implicit intent is useful when your app cannot perform the action, but other apps probably can. If there is more than one application registered that can handle this request, the user will be prompted to select which one to use.

```
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType(HTTP.PLAIN_TEXT_TYPE); // "text/plain" MIME type
startActivity(sendIntent);
```

Above crashes cause there is no check for an application.

```
// Verify that there are applications registered to handle this intent
// (resolveActivity returns null if none are registered)
if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(sendIntent);
}
```
