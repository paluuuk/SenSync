# SenSync

Cross-platform Flutter application exploring **sensory-overload prediction for individuals with autism** using wearable/health signals, with caregiver-facing alerts and supporting mobile features.

Built for the **Google Developer Solution Challenge 2023**, the project combines a Flutter mobile application with an ML experimentation pipeline and notification/location capabilities.

## Product Concept

SenSync is designed around a simple workflow:

```text
Wearable / Health Signals
          ↓
Data Extraction
          ↓
Feature Processing
          ↓
Random Forest Model
          ↓
Sensory-Overload Prediction
          ↓
Mobile App / Caregiver Alert
```

The goal is to identify patterns associated with sensory overload and surface useful information to the user or caregiver through the mobile application.

## Engineering Highlights

### Cross-platform mobile application

The application is implemented with **Flutter / Dart** and includes native iOS and Android project targets.

The repository contains:

- reusable Flutter UI components
- application screens and navigation
- Firebase configuration
- location functionality
- notification services
- background-processing experimentation for health-data collection

### ML experimentation

The repository includes notebooks covering:

- data extraction
- model development
- deployment experimentation

A serialized **Random Forest model** is also included in the current repository. The ML work uses wearable/physiological signals to explore sensory-overload prediction.

### Notifications and location

The Flutter application contains a dedicated notification service and location functionality, supporting the broader caregiver-alert workflow envisioned for the product.

## Repository Structure

```text
SenSync/
├── lib/
│   ├── screens/               # Application screens
│   ├── reusable_widgets/      # Shared UI components
│   ├── widgets/               # App widgets
│   ├── Services/
│   │   └── notifications.dart
│   ├── main.dart
│   ├── firebase_options.dart
│   ├── get_location.dart
│   ├── Data Extraction.ipynb
│   ├── Modeling.ipynb
│   ├── Deployment.ipynb
│   └── rf_model.pkl
├── android/
├── ios/
├── test/
├── pubspec.yaml
└── README.md
```

## Tech Stack

**Mobile**  
Flutter · Dart · iOS · Android

**Backend / Platform**  
Firebase · notifications · location services

**Machine Learning**  
Python experimentation · Random Forest · wearable / physiological signal analysis

## Running the Mobile App

The project was developed with Flutter 3.7.6 / Dart 2.19.3 and was tested on iOS using Xcode 14.2.

```bash
flutter clean
flutter pub get
flutter run
```

For physical iOS-device testing, open the `ios` project in Xcode, configure code signing, select the connected device, and run the application.

## Current Integration Status

The mobile-side health-data collection workflow and the ML prediction workflow were developed and validated as separate components, but the original project did **not complete the end-to-end integration between those components**.

The repository is therefore best viewed as a functional mobile prototype plus an ML proof of concept rather than a production-ready medical system.

## What I Would Improve Next

From a software-engineering perspective, the next iteration would:

1. move the ML notebooks into a dedicated `ml/` or `notebooks/` directory;
2. expose model inference through a clean service/API boundary rather than storing the model inside `lib/`;
3. remove generated Flutter/build artifacts from version control;
4. add automated Flutter tests and CI;
5. formalize the data contract between mobile health-data ingestion and model inference;
6. add model evaluation, monitoring, and explicit privacy controls before any real-world health deployment.

## Project Context

SenSync was created as a student solution for the **Google Developer Solution Challenge 2023**. It explores how mobile engineering and machine learning can be combined to support people who experience sensory overload and their caregivers.

> **Important:** This is an experimental student project and not a clinically validated diagnostic or medical device.