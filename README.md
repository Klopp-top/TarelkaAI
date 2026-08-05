# CalorieAI

iOS-приложение на SwiftUI для подсчёта калорий и нутриентов: распознаёт еду по фотографии,
сканирует штрихкоды, ищет продукты в базе и ведёт дневник питания с синхронизацией в Apple Health.

> ⚠️ Перед первым запуском укажи свой API-ключ — см. раздел [Настройка](#настройка).

<!-- Скриншоты сильно повышают шанс, что репозиторий посмотрят.
     Положи 2–3 картинки в папку docs/ и раскомментируй:
<p float="left">
  <img src="docs/screenshot-camera.png" width="240" />
  <img src="docs/screenshot-log.png"    width="240" />
  <img src="docs/screenshot-charts.png" width="240" />
</p>
-->

## Возможности

- **Три способа добавить еду** — фото, штрихкод, текстовый поиск (единый экран `CameraView`).
- **Распознавание блюда по фото** — снимок анализируется, возвращаются калории и БЖУ.
- **Сканер штрихкодов** — данные о продукте подтягиваются из Open Food Facts.
- **Дневник питания** — приёмы пищи за день, дневная норма и остаток.
- **Графики и статистика** — динамика калорий и нутриентов по дням.
- **Анализ дефицитов** — подсветка нутриентов, которых стабильно не хватает.
- **Apple HealthKit** — обмен данными о питании с приложением «Здоровье».
- **Стрики и напоминания** — серия дней без пропусков, локальные уведомления.
- **Рецепты** — подбор блюд под оставшуюся норму калорий.
- **Онбординг и мультиязычность** — расчёт нормы под пользователя, переключение языка в приложении.

## Стек

| | |
|---|---|
| UI | SwiftUI |
| Камера / штрихкоды | AVFoundation, UIKit (`UIImagePickerController`) |
| Здоровье | HealthKit |
| Уведомления | UserNotifications |
| Внешние данные | Open Food Facts API |
| Архитектура | MVVM (`DailyLogViewModel`, `UserViewModel`, сервисы) |

Минимальные требования: iOS 17+, Xcode 15+.

## Структура проекта

```
first-project/
├── first_projectApp.swift     точка входа
├── ContentView.swift          корневая навигация
├── OnboardingView.swift       первый запуск, расчёт нормы калорий
│
├── CameraView.swift           фото / штрихкод / поиск — добавление еды
├── ChartsView.swift           графики и статистика
├── Recipe.swift               рецепты
├── LanguagePickerView.swift   выбор языка
├── StreakBadge.swift          UI серии дней
│
├── FoodRecognitionService.swift  распознавание блюда по фото
├── OpenFoodFactsService.swift    поиск продукта по штрихкоду
├── FoodDatabase.swift            локальная база продуктов
├── HealthKitService.swift        интеграция с Apple Health
├── NotificationManager.swift     локальные уведомления
├── StreakManager.swift           логика серий
│
├── DailyLogViewModel.swift    дневник питания за день
├── UserViewModel.swift        профиль и цели пользователя
├── FoodAnalysisResult.swift   модель результата анализа
├── NutritionDeficiency.swift  анализ дефицита нутриентов
│
├── AppLanguage.swift          локализация
└── Extensions.swift           общие расширения
```

## Установка

```bash
git clone https://github.com/Klopp-top/CalorieAI.git
cd CalorieAI
open CalorieAI.xcodeproj
```

Дальше: выбрать симулятор (например, iPhone 17 Pro Max) и нажать ▶.

## Настройка

Ключ API в репозиторий не коммитится. Создай файл `first-project/Secrets.swift`
(он уже в `.gitignore`):

```swift
enum Secrets {
    static let foodRecognitionAPIKey = "ВАШ_КЛЮЧ"
}
```

и используй его в `FoodRecognitionService`:

```swift
let apiKey = Secrets.foodRecognitionAPIKey
```

Для работы камеры, галереи и HealthKit в `Info.plist` должны быть описания разрешений:
`NSCameraUsageDescription`, `NSPhotoLibraryUsageDescription`,
`NSHealthShareUsageDescription`, `NSHealthUpdateUsageDescription`.

## Статус

Проект в активной разработке. Планы:

- [ ] Виджет на домашний экран с остатком калорий
- [ ] Экспорт дневника в CSV
- [ ] Оффлайн-режим для базы продуктов
- [ ] Тесты для расчёта нормы калорий и БЖУ

## Лицензия

MIT — см. [LICENSE](LICENSE).
