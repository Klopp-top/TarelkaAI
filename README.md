# TarelkaAI

An iOS app built with SwiftUI for tracking calories and nutrients: recognizes food from
photos, scans barcodes, searches a product database, and keeps a food diary synced with
Apple Health.

> ⚠️ Set your API key before the first run — see the [Setup](#setup) section.

<!-- Screenshots significantly increase the chance people will check out the repo.
     Drop 2–3 images into the docs/ folder and uncomment:
<p float="left">
  <img src="docs/screenshot-camera.png" width="240" />
  <img src="docs/screenshot-log.png"    width="240" />
  <img src="docs/screenshot-charts.png" width="240" />
</p>
-->

## Features

- **Three ways to log food** — photo, barcode, or text search (all on one `CameraView` screen).
- **Photo food recognition** — snap a picture, get calories and macros back.
- **Barcode scanner** — product data pulled from Open Food Facts.
- **Food diary** — meals logged per day, with daily target and remaining allowance.
- **Charts and stats** — calorie and nutrient trends over time.
- **Deficiency analysis** — highlights nutrients you're consistently falling short on.
- **Apple HealthKit** — syncs nutrition data with the Health app.
- **Streaks and reminders** — track consecutive logging days with local notifications.
- **Recipes** — meal suggestions that fit your remaining calorie budget.
- **Onboarding and multi-language support** — personalized target calculation, in-app language switch.

## Tech Stack

| | |
|---|---|
| UI | SwiftUI |
| Camera / barcodes | AVFoundation, UIKit (`UIImagePickerController`) |
| Health | HealthKit |
| Notifications | UserNotifications |
| External data | Open Food Facts API |
| Architecture | MVVM (`DailyLogViewModel`, `UserViewModel`, services) |

Minimum requirements: iOS 17+, Xcode 15+.

## Project Structure

```
first-project/
├── first_projectApp.swift     entry point
├── ContentView.swift          root navigation
├── OnboardingView.swift       first launch, calorie target calculation
│
├── CameraView.swift           photo / barcode / search — adding food
├── ChartsView.swift           charts and stats
├── Recipe.swift               recipes
├── LanguagePickerView.swift   language picker
├── StreakBadge.swift          streak UI
│
├── FoodRecognitionService.swift  photo-based food recognition
├── OpenFoodFactsService.swift    barcode product lookup
├── FoodDatabase.swift            local product database
├── HealthKitService.swift        Apple Health integration
├── NotificationManager.swift     local notifications
├── StreakManager.swift           streak logic
│
├── DailyLogViewModel.swift    daily food diary
├── UserViewModel.swift        user profile and goals
├── FoodAnalysisResult.swift   analysis result model
├── NutritionDeficiency.swift  nutrient deficiency analysis
│
├── AppLanguage.swift          localization
└── Extensions.swift           shared extensions
```

## Installation

```bash
git clone https://github.com/Klopp-top/CalorieAI.git
cd CalorieAI
open CalorieAI.xcodeproj
```

Then pick a simulator (e.g. iPhone 17 Pro Max) and hit ▶.

## Setup

The API key is not committed to the repo. Create `first-project/Secrets.swift`
(already in `.gitignore`):

```swift
enum Secrets {
    static let foodRecognitionAPIKey = "YOUR_KEY"
}
```

and use it in `FoodRecognitionService`:

```swift
let apiKey = Secrets.foodRecognitionAPIKey
```

For the camera, photo library, and HealthKit to work, `Info.plist` needs these usage
descriptions: `NSCameraUsageDescription`, `NSPhotoLibraryUsageDescription`,
`NSHealthShareUsageDescription`, `NSHealthUpdateUsageDescription`.

## Status

Actively in development. Roadmap:

- [ ] Home screen widget showing remaining calories
- [ ] Export food diary to CSV
- [ ] Offline mode for the product database
- [ ] Tests for calorie/macro target calculations

## License

MIT — see [LICENSE](LICENSE).
