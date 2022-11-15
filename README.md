# Android-Chat-App

Android chat application developed with Java and Firebase. A hassle-free way to communicate. 
### Features : 
* message texts
* Add contacts
* edit profile credentials
* Notifications with firebase cloud messaging

Original source: https://github.com/Raj-m01/Android-Chat-App

Please note that you need to append your own google-services.json file to run the app.

There are 3 Firebase services necessary to run the app:

* Authentication
* Realtime Database
* Storage

On Firebase console use this project: **FirebaseChatApp** (fir-chatapp-a5632)

The content of the chat is encrypted but with an **unsecure AES mode** (it uses the ECB mode) so you 
should consider of using a more better one like CBC or GCM mode.

Works with Cloud Messaging: https://infyom.com/blog/send-device-to-device-push-notification-using-firebase-cloud-messaging

Firebase Console - project settings - Cloud Messaging

Server key for Cloud Messaging API (Legacy), add in FcmNotificationsSender.java:
```plaintext
AAAA1IYYfYY:APA91bGurFhX2EGXpjTdd2mRAjRaOO35WyeHXDHGNxJVm3j6ZkPh0pSGS_WqPwumpEMRM-q0MB_Osc7OiPi7qv5hfeEzZyNXNG3dyF_GPhnW3NDwchA77vAeTeA-Vh3yAba20AICdoSh
```

Sound files must reside in /res/raw/

Sound effect: Sound Effect from <a href="https://pixabay.com/sound-effects/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=music&amp;utm_content=14606">Pixabay</a>

Info about notification: https://developer.android.com/develop/ui/views/notifications/build-notification

Info about notification channels: https://developer.android.com/develop/ui/views/notifications/channels

AndroidManifest.xml:
```plaintext
        <service 
             android:name=".PushNotificationService" 
             android:exported="false">
            <intent-filter>
                <action 
                      android:name="com.google.firebase.MESSAGING_EVENT">
                 </action>
            </intent-filter>
        </service>
```

**Don't forget to give runtime permissions !**

```plaintext
AndroidManifest.xml:
  

    MainActivity onCreate:
    askNotificationPermission();

    private void askNotificationPermission() {
        // This is only necessary for API Level > 33 (TIRAMISU)
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {
            if (ContextCompat.checkSelfPermission(this, Manifest.permission.POST_NOTIFICATIONS) ==
                    PackageManager.PERMISSION_GRANTED) {
                // FCM SDK (and your app) can post notifications.
            } else {
                // Directly ask for the permission
                requestPermissionLauncher.launch(Manifest.permission.POST_NOTIFICATIONS);
            }
        }
    }
    
    private final ActivityResultLauncher<String> requestPermissionLauncher =
            registerForActivityResult(new ActivityResultContracts.RequestPermission(), isGranted -> {
                if (isGranted) {
                    Toast.makeText(this, "Notifications permission granted",Toast.LENGTH_SHORT)
                            .show();
                } else {
                    Toast.makeText(this, "FCM can't post notifications without POST_NOTIFICATIONS permission",
                            Toast.LENGTH_LONG).show();
                }
            });
    


```


Solve FirebaseMessagingService.java:63:
```plaintext
java.lang.IllegalArgumentException: com.example.chatapp: Targeting S+ (version 31 and above) requires that one of FLAG_IMMUTABLE or FLAG_MUTABLE be specified when creating a PendingIntent.
Strongly consider using FLAG_IMMUTABLE, only use FLAG_MUTABLE if some functionality depends on the PendingIntent being mutable, e.g. if it needs to be used with inline replies or bubbles.
at android.app.PendingIntent.checkFlags(PendingIntent.java:382)
at android.app.PendingIntent.getActivityAsUser(PendingIntent.java:465)
at android.app.PendingIntent.getActivity(PendingIntent.java:451)
at android.app.PendingIntent.getActivity(PendingIntent.java:415)
at com.example.chatapp.FirebaseMessagingService.onMessageReceived(FirebaseMessagingService.java:63)
```

## Screenshots : 

<table>
  <tr>
    <th>Authentication</th>
    <th>Adding Contact</th>
    <th>Contacts</th>
  </tr>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/79650580/195169217-ad08d0e6-23a3-4fad-874e-e68b3b828c32.png" alt="Authentication" style="width:250px;height:500px;"></td>
    <td><img src="https://user-images.githubusercontent.com/79650580/195169821-2efe67cc-718d-42b7-b510-d4004692cf3e.png" alt="Adding Contact" style="width:250px;height:500px;"></td>
    <td><img src="https://user-images.githubusercontent.com/79650580/195169874-6bbcaa95-6e8b-4e7e-abad-69021df4bde5.png" alt="Contacts activity" style="width:250px;height:500px;"></td>
  </tr>
   
</table>


<table>
  <tr>
    <th>Profile</th>
    <th>Messaging</th>
  </tr>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/79650580/195170439-1688801d-3f90-4ef3-a591-c45200c3d714.png" alt="Profile activity" style="width:250px;height:500px;"></td>
    <td><img src="https://user-images.githubusercontent.com/79650580/195171608-4b051690-59fa-4601-b1c6-db1e44c6bfd4.png" alt="messaging" style="width:250px;height:500px;"></td>
  </tr>
   
</table>

## Firebase Database Schema : 
![image](https://user-images.githubusercontent.com/79650580/195172072-bcbe77b4-84c2-4a6c-817d-836bb0572db6.png)


### Full demo : 
<div align="center">
  <a href="https://youtu.be/U-NWcV_tfd4"><img src="https://user-images.githubusercontent.com/79650580/147914116-8f3725ef-8206-47b1-8735-f562ce3088f2.png" alt="Click here to watch full demo"></a>
</div>
