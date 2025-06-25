# 🎯 Unity AR App – Vuforia + Firebase (Lightweight)

A lightweight and modular Augmented Reality (AR) mobile application built with Unity. This project leverages **Vuforia** for marker-based AR tracking and **Firebase** for cloud messaging (notifications), dynamic module management, and potential future features like dynamic links and analytics.

---

## 📁 Project Structure

```plaintext
Assets/
├── _Project/              → Project notes, changelog
├── Art/                   → Models, Materials, Textures
├── Audio/                 → Game music, SFX
├── Firebase/              → Firebase SDK and feature modules
│   ├── Authentication/
│   ├── CloudMessaging/
│   ├── RemoteConfig/
│   ├── DynamicLinks/
│   └── Editor/
├── Plugins/               → Android/iOS libraries
├── Prefabs/               → Reusable GameObjects
├── Resources/             → Dynamic loading assets
├── Scenes/
│   └── Main.unity
├── Scripts/
│   ├── AR/
│   ├── FirebaseServices/
│   ├── Managers/
│   └── UI/
├── UI/
│   ├── Sprites/
│   └── Fonts/
└── StreamingAssets/
```

---

## ⚙️ Technologies Used

| Technology     | Purpose                             |
|----------------|-------------------------------------|
| Unity LTS 2021.3+ | Game Engine                     |
| Vuforia Engine | Marker-based AR tracking            |
| Firebase SDK   | Notifications, Remote Config        |
| C#             | Game scripting language             |

---

## 🔧 Unity Setup

- **Unity Version:** 2021.3.34f1 LTS or 2022.3.10f1 LTS
- **Scripting Backend:** IL2CPP
- **Target Architectures:** ARM64
- **Minimum API Level:** Android 7.0 (API 24)

Enable **Vuforia** via:
> Edit → Project Settings → XR Plug-in Management → Android → Enable Vuforia

---

## 🔌 Vuforia Setup

1. Go to [Vuforia Developer Portal](https://developer.vuforia.com)
2. Create a project and copy the license key
3. In Unity: Window → Vuforia Engine → Configuration → Paste License Key
4. Add `ARCamera` and `ImageTarget` to your scene from Vuforia Engine
5. Adjust Transform to `(0, 0, 0)` for camera and targets

---

## 🔥 Firebase Integration

### Step 1: Firebase Console Setup

1. Visit: https://console.firebase.google.com
2. Create a Firebase project
3. Add an Android app with your Unity package name (e.g., `com.company.arapp`)
4. Download `google-services.json`
5. Place it in:
   ```
   Assets/Plugins/Android/
   ```

### Step 2: Import Firebase SDK into Unity

Import the following `.unitypackage` files from Firebase Unity SDK:

- `FirebaseApp.unitypackage`
- `FirebaseMessaging.unitypackage`
- `FirebaseRemoteConfig.unitypackage`

> Import only what you need to minimize build size.

---

## 🧠 Firebase Initialization Script

```csharp
using UnityEngine;
using Firebase;
using Firebase.Extensions;

public class FirebaseInit : MonoBehaviour {
    void Start() {
        FirebaseApp.CheckAndFixDependenciesAsync().ContinueWithOnMainThread(task => {
            var status = task.Result;
            if (status == DependencyStatus.Available) {
                Debug.Log("Firebase is ready");
            } else {
                Debug.LogError($"Firebase setup error: {status}");
            }
        });
    }
}
```

Attach to a `FirebaseManager` GameObject.

---

## 📩 Firebase Cloud Messaging (FCM)

Enable Push Notifications:

```csharp
Firebase.Messaging.FirebaseMessaging.SubscribeAsync("news");
```

Send notifications via Firebase Console under **Cloud Messaging**.

---

## ⚙️ Firebase Remote Config Example

```csharp
FirebaseRemoteConfig.DefaultInstance.FetchAsync().ContinueWithOnMainThread(task => {
    if (task.IsCompleted) {
        FirebaseRemoteConfig.DefaultInstance.ActivateAsync();
        string flag = FirebaseRemoteConfig.DefaultInstance.GetValue("isARFeatureEnabled").StringValue;
        if (flag == "true") EnableARFeature();
    }
});
```

Manage values from Firebase Console → Remote Config.

---

## 🧪 Testing & Build Tips

- Use webcam in Play Mode for quick AR tests
- Keep scenes minimal and assets compressed
- Use IL2CPP and ARM64 to optimize build size
- Disable Post-Processing and reduce lighting effects for performance
- Use Firebase selectively to avoid bloat

---

## ✅ To-Do

| Feature               | Status     |
|------------------------|------------|
| Vuforia ImageTracking  | ✅ Complete |
| Firebase Messaging     | 🔄 In Progress |
| Remote Config Support  | 🔄 In Progress |
| Dynamic Links Support  | ⏳ Optional |
| Firebase Analytics     | ⏳ Optional |
| Firebase Auth          | ⏳ Optional |

---

## 📝 License

This project uses open technologies (Unity, Firebase, Vuforia). Refer to each SDK's official license. This project may be shared or modified under MIT or CC license (as needed).

---

## 👨‍💻 Maintainer

**Developer:** _Abhishek kumar majumdar_  
**Portfolio:** __https://abhishekkumarmajumdar.in_  
**Email:** _dev.abhishekmajumdar@gmail.com_ 
**GitHub:** _https://github.com/AbhishekKumarMajumdar_

