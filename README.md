# AI Live Wallpapers for iOS

An innovative iOS application, built entirely with **SwiftUI**, that empowers users to create, animate, and set unique Live Wallpapers using the power of generative AI. Integrating both text generation, image generation and video generation into one project.

## 🌟 Demo

![Image](https://github.com/user-attachments/assets/1a4176b7-05a3-4ae4-973f-9a184ca9089f)

## ✨ Key Features

* **🤖 AI-Powered Generation:** Describe your dream wallpaper and watch it come to life! The app integrates directly with **OpenAI's DALL-E API** to generate stunning, high-quality images from simple text prompts.
* **🎬 Instant Animation:** Bring your static creations to life. Using the **RunwayML API**, any generated image can be seamlessly transformed into a captivating video loop, perfect for a dynamic wallpaper.
* **📱 Live Photo Conversion:** Your creations aren't just videos; they are fully functional **Live Photos**. The app handles the entire conversion process, allowing users to save and set them directly as their iPhone's lock screen wallpaper.
* **🖼️ Curated Gallery:** For users seeking instant inspiration, the app features a gallery of beautiful, pre-made wallpapers and live videos fetched in real-time from a **Firebase** backend.

---

## 🛠️ Tech Stack & Architecture

This project was built using a modern, scalable, and maintainable tech stack.

* **UI Framework:** **SwiftUI** (100% programmatic UI)
* **Architecture:** **MVI (Model-View-Intent)**
    * This choice promotes a unidirectional data flow, making the app's state predictable and easy to debug. It isolates business logic from the view layer, significantly improving testability.
* **Concurrency:** **Swift Concurrency (`async/await`)** for managing all asynchronous operations and API calls cleanly and efficiently.
* **Backend & APIs:**
    * **OpenAI API:** For `DALL-E` text-to-image generation.
    * **RunwayML API:** For image-to-video animation.
    * **Firebase:** Utilizes `Firestore` for the pre-made wallpaper database and `Cloud Storage` for hosting the associated image and video assets.

---

## 🚀 Technical Highlights & Problem-Solving

This section details some of the interesting technical challenges and how they were solved.

### 1. The "Prompt-to-Live-Photo" Workflow

The core feature of the app is a multi-step pipeline that required careful orchestration of several asynchronous services.

1.  **Text Prompt (`View`) -> `Intent` -> `Model`**: The user's input triggers an intent.
2.  **OpenAI API Call**: The model sends a request to OpenAI to generate an image.
3.  **RunwayML API Call**: The resulting image data is forwarded to RunwayML to be animated into a video.
4.  **Live Photo Conversion**: The final video file is converted into the `PHLivePhoto` format. This was a key challenge. While leveraging a third-party GitHub package for the core conversion logic, I engineered the surrounding workflow to handle data preparation, error handling, caching, and seamless integration back into the UI.

### 2. Cost-Effective & Efficient Development

Working with pay-as-you-go APIs like OpenAI and Runway requires a development strategy that minimizes costs.

* **Protocol-Oriented Design**: The project heavily relies on protocols for its services and repositories (e.g., `WallpaperGenerating`, `WallpaperAnimating`).
* **Use Cases & Mocking**: I implemented a system of **Use Cases** to abstract the business logic. This, combined with the protocol-oriented design, allowed me to create **mock repositories** for testing. These mocks simulate API responses, enabling me to build and test the entire data flow and UI state management without making a single real API call, thus saving credits and enabling offline development.

---

## ⚙️ Installation

As I am too lazy to write a detailed guide to installation, you will have to wait for the version on App Store 😆

## 📦 Dependencies

* **[[Video2LivePhoto](https://github.com/TouSC/Video2LivePhoto)]**- The Swift and Obj-C Package used for the final video-to-Live-Photo conversion.

## 🔮 Future Enhancements

This project has a strong foundation that can be expanded with many exciting features:

* **Advanced Animation Controls:** Give users control over animation parameters like duration, motion intensity, and style.
* **Style Transfer:** Allow users to apply more artistic styles and better overall Ui and Ux of the app.
* **iCloud Sync:** Sync a user's generated wallpapers across devices *(although the user can save their wallpapers to photos app, which is synced, this could be a neat feature)*
