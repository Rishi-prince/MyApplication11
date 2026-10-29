# Experiment 11: Develop an Android Application to Display Google Maps

## 📌 Experiment Title

**Develop an Android Application to Display Google Maps**

---

## 🎯 Aim

To develop an Android application using **Android Studio** that integrates **Google Maps** and displays an interactive map on the application screen. The application allows users to view the map, zoom in and out, move around the map, and identify a specific location using a marker.

---

## 📖 Introduction

Google Maps is a widely used mapping service that provides geographical information, navigation, location searching, satellite imagery, and many other location-based services.

Android provides the **Google Maps SDK for Android**, which allows developers to integrate Google Maps directly into Android applications.

In this experiment, an Android application is developed that displays Google Maps inside the application. A marker is also added to a specific location to demonstrate how locations can be represented on the map.

The application demonstrates the basic integration of a third-party location-based service into an Android application.

---

## 💡 Objectives

The main objectives of this experiment are:

- To understand Google Maps integration in Android applications.
- To learn how to use the Google Maps SDK for Android.
- To understand the use of Google Maps API keys.
- To display an interactive map inside an Android application.
- To add a marker to a particular geographical location.
- To move the camera to a specific location.
- To understand latitude and longitude coordinates.
- To perform basic map operations such as zooming and scrolling.
- To understand the basic implementation of location-based services.

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Android Studio | Development Environment |
| Java | Application Programming Language |
| XML | User Interface |
| Google Maps SDK | Displaying Google Maps |
| Google Maps API | Accessing Google Maps services |
| Android SDK | Android Application Development |
| Gradle | Project Build System |

---

## 💻 Software Requirements

- Android Studio
- JDK
- Android SDK
- Google Cloud Console Account
- Internet Connection
- Android Emulator or Android Smartphone

---

## 📱 Hardware Requirements

- Computer/Laptop
- Minimum 4 GB RAM
- Android Device or Emulator
- Internet Connection

---

# 🔑 Google Maps API Key

To display Google Maps in an Android application, a **Google Maps API key** is required.

The API key is generated using **Google Cloud Console**.

### Basic Steps

1. Open Google Cloud Console.
2. Create or select a project.
3. Enable the **Maps SDK for Android**.
4. Create an API key.
5. Restrict the API key to the Android application.
6. Add the API key to the Android project.
7. Run the application.

> ⚠️ **Security Note:** Do not upload an unrestricted API key to a public GitHub repository. API keys should be properly restricted.

---

# 📂 Project Structure

A basic project structure is:

```text
GoogleMapsApp/
│
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/
│   │       │   └── MainActivity.java
│   │       │
│   │       ├── res/
│   │       │   ├── layout/
│   │       │   │   └── activity_main.xml
│   │       │   │
│   │       │   └── values/
│   │       │
│   │       └── AndroidManifest.xml
│   │
│   └── build.gradle
│
├── gradle/
├── build.gradle
├── settings.gradle
└── README.md
```

---

# ⚙️ Procedure

### Step 1: Create Android Project

Open Android Studio and create a new Android project.

Select an appropriate project name such as:

```text
GoogleMapsApp
```

Select Java as the programming language if required.

---

### Step 2: Configure Google Maps

Configure the Google Maps SDK for the Android project and provide the required API key.

The API key allows the application to communicate with Google Maps services.

---

### Step 3: Configure the Manifest

The application requires Internet access to load map data.

Add:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

inside the `AndroidManifest.xml` file.

---

### Step 4: Create Map Layout

The application uses a `SupportMapFragment` to display the map.

Example:

```xml
<fragment
    android:id="@+id/map"
    android:name="com.google.android.gms.maps.SupportMapFragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

---

### Step 5: Initialize Google Map

The map is initialized using `SupportMapFragment`.

```java
SupportMapFragment mapFragment =
        (SupportMapFragment) getSupportFragmentManager()
        .findFragmentById(R.id.map);

if (mapFragment != null) {
    mapFragment.getMapAsync(this);
}
```

---

### Step 6: Add Marker

A marker can be added using latitude and longitude.

For example, Bangalore coordinates:

```text
Latitude  = 12.9716
Longitude = 77.5946
```

Java code:

```java
LatLng bangalore = new LatLng(12.9716, 77.5946);

mMap.addMarker(
        new MarkerOptions()
        .position(bangalore)
        .title("Bangalore")
);
```

---

### Step 7: Move Camera

The map camera can be moved to the selected location.

```java
mMap.moveCamera(
        CameraUpdateFactory.newLatLngZoom(bangalore, 12)
);
```

The zoom level determines how closely the location is displayed.

---

# 👨‍💻 MainActivity.java

```java
package com.example.googlemapsapp;

import android.os.Bundle;

import androidx.appcompat.app.AppCompatActivity;

import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.SupportMapFragment;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;

public class MainActivity extends AppCompatActivity
        implements OnMapReadyCallback {

    private GoogleMap mMap;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        SupportMapFragment mapFragment =
                (SupportMapFragment)
                        getSupportFragmentManager()
                        .findFragmentById(R.id.map);

        if (mapFragment != null) {
            mapFragment.getMapAsync(this);
        }
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {

        mMap = googleMap;

        // Location of Bangalore
        LatLng bangalore =
                new LatLng(12.9716, 77.5946);

        // Add marker
        mMap.addMarker(
                new MarkerOptions()
                        .position(bangalore)
                        .title("Bangalore")
        );

        // Move camera
        mMap.moveCamera(
                CameraUpdateFactory
                        .newLatLngZoom(bangalore, 12)
        );
    }
}
```

---

# 🖥️ Layout File

Example `activity_main.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>

<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <fragment
        android:id="@+id/map"
        android:name="com.google.android.gms.maps.SupportMapFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</FrameLayout>
```

---

# 🗺️ Working of the Application

The working of the application can be represented as:

```text
             Start Application
                    ↓
             Initialize Map
                    ↓
           Load Google Maps SDK
                    ↓
            Display Google Map
                    ↓
         Set Latitude & Longitude
                    ↓
             Add Map Marker
                    ↓
          Move Camera to Location
                    ↓
             Display Final Map
```

---

# 📍 Latitude and Longitude

Google Maps identifies geographical locations using two main coordinates:

### Latitude

Latitude represents the position of a location from north to south.

### Longitude

Longitude represents the position of a location from east to west.

For example:

```text
Bangalore

Latitude  : 12.9716
Longitude : 77.5946
```

These coordinates are used to place the marker accurately on the map.

---

# 🔍 Features of the Application

The application provides the following features:

- Displays Google Maps.
- Shows an interactive map.
- Supports map scrolling.
- Supports zoom in and zoom out.
- Displays a marker.
- Shows the title of the selected location.
- Moves the camera to a specific location.
- Uses latitude and longitude coordinates.
- Demonstrates integration of an external API/service.

---

# 🧪 Testing

The application can be tested using the following cases:

| Test Case | Expected Result |
|---|---|
| Launch application | Google Maps should appear |
| Internet available | Map should load successfully |
| Zoom in | Map should zoom in |
| Zoom out | Map should zoom out |
| Scroll map | Map should move |
| Marker displayed | Marker should appear |
| Click marker | Location title should appear |
| Camera movement | Camera should move to selected location |

---

# 📸 Expected Output

When the application is successfully executed:

1. The application opens.
2. Google Maps is displayed.
3. The map is centered on Bangalore.
4. A marker appears on the Bangalore location.
5. The user can zoom and move around the map.

Example:

```text
+--------------------------------------+
|                                      |
|             Google Maps              |
|                                      |
|                   📍                 |
|                Bangalore             |
|                                      |
|                                      |
|          +                    -      |
|                                      |
+--------------------------------------+
```

---

# ❗ Common Errors and Solutions

### 1. Map is not displaying

**Possible reason:**
- API key is missing.
- API key is incorrect.
- Maps SDK is not enabled.
- Internet connection is unavailable.

**Solution:**
- Check the API key.
- Enable Maps SDK for Android.
- Check the internet connection.

---

### 2. Blank/Gray Map

**Possible reasons:**

- Invalid API key.
- API key restrictions are incorrect.
- Google Maps SDK is not enabled.

**Solution:**

Verify the Google Cloud project and API key configuration.

---

### 3. Application Crashes

Check:

- Gradle dependencies.
- Package name.
- API configuration.
- Manifest configuration.
- Android SDK version.

---

# 📚 Learning Outcomes

After completing this experiment, we understand:

- How to create an Android application using Android Studio.
- How Google Maps can be integrated into an Android application.
- How API keys are used.
- How to initialize Google Maps.
- How to add markers.
- How latitude and longitude work.
- How to move the map camera.
- How external services can be integrated into Android applications.

---

# 🎓 Applications

Google Maps integration can be used in many real-world applications, such as:

- 📍 Location tracking applications
- 🚕 Cab booking applications
- 🍔 Food delivery applications
- 🏨 Hotel booking applications
- 🚚 Delivery tracking systems
- 🏥 Hospital locator applications
- 🏫 College/campus locator applications
- 🛒 Nearby shop finder applications
- 🗺️ Travel applications
- 🚗 Navigation applications

---

# 🔒 Security Considerations

The Google Maps API key should be protected properly.

For a production application:

- Restrict the API key.
- Restrict the key to the Android application.
- Use package name and SHA-1 restrictions.
- Enable only the APIs that are required.
- Do not expose unrestricted API keys publicly.

---

# 📌 Conclusion

The Android application was successfully developed to display **Google Maps** using the Google Maps SDK for Android.

The application demonstrates how to initialize Google Maps, display an interactive map, add a marker using latitude and longitude coordinates, and move the camera to a particular location.

This experiment provides a basic understanding of **Google Maps integration and location-based services in Android applications**.

---

# 👨‍🎓 Experiment Information

**Experiment No.:** 11

**Experiment Name:** Develop an Android Application to Display Google Maps

**Platform:** Android Studio

**Language:** Java

**Technology:** Google Maps SDK for Android

**Application Type:** Android Application

---

# 🔗 GitHub Submission

GitHub Repository:

```text
https://github.com/YOUR-USERNAME/GoogleMapsApp
```

Replace `YOUR-USERNAME` with your GitHub username.

Example:

```text
https://github.com/Rishi-prince/GoogleMapsApp
```

---

## ⭐ Author

**Prince Kumar**

MCA – Jain (Deemed-to-be University)

School of Computer Science & IT


<img width="1511" height="797" alt="Screenshot 2026-10-29 111926" src="https://github.com/user-attachments/assets/a224c145-e202-4fc3-9bca-f8444b2da886" />
