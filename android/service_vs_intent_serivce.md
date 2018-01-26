# What is the difference between Service and Intent Service?

**Service** is a base class of service implementation. Service class is run in the application’s main thread which may reduce the application performance.


**IntentService**, which is a direct subclass of Service is borned to make things easier. The IntentService is used to perform a certain task in the background. Once done, the instance of IntentService terminate itself automatically. Examples for its usage would be to download a certain resources from the Internet.


So make background service calls with Intent Service.

IntentService creates a queue that passes one intent at a time to onHandleIntent(). Service would need to add multi threading and declare self stop but IntentService does not.


Source:
- https://www.linkedin.com/pulse/service-vs-intentservice-android-anwar-samir/
