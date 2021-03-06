# SHNotificationContent

### A Notification Content Extension class to display custom content interfaces for iOS 10 push notifications

Apple introduces push notification feature in iOS 10 and guess what these are more richer and interactional. Now we can view photos, gifs, watch videos, and listen to the audio from inside a notification without open that app.

When push notification have media content than its a higher chance to increase the open rate and more engagement in any app.

#### Configure your app for Rich Push Notification and add a Notification Service Extension target to your app

Go to your project target and click on Capabilities and ensure that ‘Push Notifications’ is enabled and that ‘Remote notifications’ is selected under Background Modes:

![Capabilities](images/Capabilities.png)

![EnablePushNotifications](images/enableRemoteNoti.png)

Go to AppDelegate.swift and import UserNotification.framework in appdelegate and add this code in didFinishLaunchingWithOptions:

```
UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        center.delegate = self;
        [[UNUserNotificationCenter currentNotificationCenter] setDelegate:self];
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge)
         
                              completionHandler:^(BOOL granted, NSError * _Nullable error){
                                  if(!error){
                                      dispatch_async(dispatch_get_main_queue(), ^{
                                          // UI UPDATE 1
                                          [[UIApplication sharedApplication] registerForRemoteNotifications];
                                      });
                                  }
                              }
         ];
```
You can enable Rich Push Notification via [Notification Service Extension](https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension):

Create a Notification Service Extension in your project. To do that, in Xcode, select File -> New -> Target and choose the Notification Service Extension template.

![EnableNotificationServiceExtension](images/NSE.png)

Once you’ve added the new target, you’ll have a new file called NotificationService.swift.Note: Notification Service Extension has a separate Apple App ID and Provisioning profile!
#### Note that notification extension has its own Bundle Id (ex: com.shephertz.demo.NotificationService) as well as its own Apple App ID and Provisioning profile which must be set up in Apple Developer Portal separately.

Replace NotificationService.h & NotificationService.m class with these classes and add SHNotification libSHNotificationContent.a, include folder & iCarousel folder.



### Configure your app for Rich Push Notification and add a Notification Content Extension target to your app

Create a Notification Content Service Extension in your project. To do that, in Xcode, select File -> New -> Target and choose the Notification Content Service Extension template.

![Notification Content Service](images/notificationContentService.png)

Once you’ve added the new target, you’ll have a new file called NotificationViewController.h, NotificationViewController.m & MainInterface.storyboard.Note: Notification Content Service Extension has a separate Apple App ID and Provisioning profile!

Replace NotificationViewController.h, NotificationViewController.m & MainInterface.storyboard class with these classes and add SHNotification libSHNotificationContent.a, include folder & iCarousel folder.


