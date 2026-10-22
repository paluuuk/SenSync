# SenSync

A Flutter prototype for caregiver support, developed for the Google Developer Solution Challenge 2023, alongside an offline wearable-stress classification experiment.

The intended product explores support for people who experience sensory overload. The implemented ML target is **WESAD stress classification**; it is not a clinically validated sensory-overload detector.

## Components and status

| Component | Implementation | Status |
| --- | --- | --- |
| Mobile client | Flutter/Dart screens, Firebase authentication, health-data access, location, and local notifications | Prototype |
| Offline data preparation | WESAD wrist-signal extraction, sampling alignment, and feature construction | Notebook experiment |
| Classifier | scikit-learn Random Forest using EDA, temperature, and heart-rate features | Offline model experiment |
| Deployment exploration | Firebase Admin, storage, and model-serialization notebook | Separate experiment |
| Mobile-to-inference integration | Background health collection connected to model predictions | Incomplete |

## ML workflow

The [modeling notebook](lib/Modeling.ipynb) reads WESAD participant files and wrist-device exports, aligns physiological signals, maps label 2 to stress and other labels to the comparison class, and downsamples the assembled records.

It uses a stratified 75/25 row split, resamples the training stress class, fits a Random Forest, and inspects accuracy, precision, recall, and a confusion matrix.

That row-based split mixes records from the participant pool. It does not establish performance on unseen people; subject-held-out evaluation and temporal leakage checks would be needed before making that claim. WESAD stress labels are a research proxy, not a clinical diagnosis.

## Repository map

- [`lib/screens/`](lib/screens): application screens and navigation.
- [`lib/reusable_widgets/`](lib/reusable_widgets): shared interface components.
- [`lib/Services/notifications.dart`](lib/Services/notifications.dart): local notification service.
- [Data extraction](lib/Data%20Extraction.ipynb), [modeling](lib/Modeling.ipynb), and [deployment](lib/Deployment.ipynb): separate Python experiments.
- [`pubspec.yaml`](pubspec.yaml): mobile dependencies.
- [`ml-requirements.txt`](ml-requirements.txt): packages imported by the Python notebooks.

## Running the mobile prototype

The original environment used Flutter 3.7.6 / Dart 2.19.3, with Xcode 14.2 for iOS. The Dart SDK constraint is recorded in `pubspec.yaml`.

```bash
git clone https://github.com/paluuuk/SenSync.git
cd SenSync
flutter pub get
flutter run
```

Use a compatible mobile SDK, your own Firebase project configuration, the relevant platform permissions, and iOS code signing for physical-device testing. A successful build alone does not complete the missing inference integration.

## Running the ML experiments

```bash
python -m venv .venv
# Activate .venv using the command for your shell.
python -m pip install -r ml-requirements.txt
jupyter notebook
```

The notebooks expect WESAD data under their configured `data/WESAD/` paths. Dataset downloads, cloud configuration, and external service access must be supplied separately. Dependencies are listed without claiming a newly validated training environment.

**Stack:** Flutter, Dart, Firebase, Python, pandas, NumPy, scikit-learn.

## Related engineering projects

- [Beehive mobile product](https://github.com/paluuuk/beehive)
- [Exoskeleton terrain perception](https://github.com/paluuuk/Vision-based-Terrain-Recognition-for-Lower-Limb-Exoskeletons)

[View all selected engineering work](https://github.com/paluuuk)

