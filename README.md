# COM527 Mobile Application Development

An Android app for browsing, adding, and booking accommodation landmarks on an interactive map. Built with Jetpack Compose and MapLibre for the COM527 Mobile Application Development module.

## Features

- **Interactive map** — displays accommodation landmarks as markers using MapLibre (OpenFreeMap tiles)
- **Search** — filter landmarks by location name, pulling results from both local Room database and a remote REST API
- **Add landmarks** — save new accommodation entries (name, type, location, rooms, meals) with GPS coordinates auto-filled from your current position
- **Book rooms** — tap a map marker to view details and book a room; tracks remaining availability
- **Proximity notifications** — sends a notification when you are within 50 metres of a saved landmark
- **Navigation drawer + bottom nav** — navigate between Map and Add Landmark screens

## Architecture

| File | Responsibility |
|------|---------------|
| `MainActivity.kt` | UI (Compose), GPS listener, notifications, network calls |
| `LocationModel.kt` | ViewModel — holds GPS state, landmarks list, zoom level, proximity detection |
| `Landmark.kt` | Data class with room-booking logic |
| `LandmarksDatabase.kt` | Room database singleton |
| `LandmarksDataEntity.kt` | Room entity |
| `LandmarksDataAccessObject.kt` | Room DAO |

## Requirements

- Android API 26+ (minSdk 26), targetSdk 35
- Location permission (`ACCESS_FINE_LOCATION`)
- Notifications permission (`POST_NOTIFICATIONS`)
- Internet access

## Backend / Web API

The app expects a local REST server at `http://10.0.2.2:3000` (the Android emulator's loopback to the host machine):

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/accommodation/all` | Returns all accommodation records as JSON |
| POST | `/accommodation/create` | Creates a new accommodation record |

The app functions without the server — landmarks saved locally via Room will still load.

## Building

Open in Android Studio and sync Gradle. Run on an emulator or physical device with API 26+.

## Key Dependencies

- **Jetpack Compose + Material3** — UI
- **MapLibre / Ramani Maps** — map rendering
- **Room** — local database
- **Fuel** — HTTP networking
- **Navigation Compose** — screen navigation
