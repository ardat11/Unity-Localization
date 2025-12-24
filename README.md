# 🌍 ardat11 Localization System for Unity 6

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Unity 6+](https://img.shields.io/badge/Unity-6000.x-blue.svg)](https://unity.com/)

A lightweight, asynchronous, and memory-optimized localization system for Unity 6 (6000.x) that syncs directly with Google Sheets.

---

## 🚀 Unity 6 Features

* **Multi-Sheet Support:** Seamlessly merge multiple Google Sheets tabs into one local database.
* **Async Synchronization:** Non-blocking download process using Editor update callbacks.
* **Memory Efficient:** High-performance `Dictionary<string, string[]>` architecture for low RAM overhead.
* **Regex-Safe Parsing:** Supports cells containing commas and quotes without breaking the CSV structure.

---

## 🛠️ Setup Instructions

### 1. Google Sheets Preparation
1. Organize your sheet with headers: `Key`, `Turkish`, `English`, etc.

   <img width="512" height="399" alt="image" src="https://github.com/user-attachments/assets/bf05ac8f-e8bf-4b1c-b8cd-409e1d230e85" />

2. Navigate to **File > Share > Publish to web**.

   <img width="512" height="400" alt="image" src="https://github.com/user-attachments/assets/a6fb453c-a752-4b02-a5d3-86f85637ebde" />


3. Select the desired tab and choose **Comma-separated values (.csv)**. Copy the link (that I've cencored). Repeat this process to obtain a link for each tab. 

   <img width="350" height="520" alt="image" src="https://github.com/user-attachments/assets/2d569ff9-0cb5-4886-a732-1602f3da187d" />


### 2. Unity Configuration (.unitypackage)

1. **Import the Package:** - Download the `ardat11_Localization.unitypackage` from the [Releases](#) section.
   - Drag and drop the package into your Unity Project or go to `Assets > Import Package > Custom Package`.
   - Ensure all scripts, prefabs, and the Resources folder are selected.

2. **Locate & Configure Settings:**
   - After importing, navigate to `Assets/ardat11_Localization/Resources/`.
   - Select the `LocalizationSettings.asset` file.
   - In the Inspector, find the **Google Sheets Configuration** section.
   - Add your copied CSV URLs to the `Google Sheets Urls` list.
   - Define your `Language Codes` (e.g., en, tr, de) to match your sheet columns. They don't necessarily need to be the same. We will be using these language codes in the script to handle language switching.
  
   This is the configured version of the LocalizationSettings for the sample spreadsheet.

     <img width="234" height="415" alt="image" src="https://github.com/user-attachments/assets/6bf9b54e-d48c-4988-888e-6a2ec5710aaa" />


### 3. Syncing Data

1. Go to **Tools > Localization > Sync Window**.
2. Select LocalizationSettings and click **Download & Merge Sheets**.
3. If you make changes on the sheet after downloading it you need to re-download it and also click **Reset Static Manager & Cache**.

    <img width="238" height="454" alt="image" src="https://github.com/user-attachments/assets/c6028d2b-d1be-4c58-8067-fae9d3bddd0a" />

---

## 📖 Usage

### UI Setup
1. Use the LocalizedText/LocalizedButton Prefabs(Recommended) **or** Add the `LocalizedText` component to a desired object and assign Tmp value.
2. Set key value. In the example instance if I set it "key1" the english version written would be "Hello"
3. The text area will be overwritten and translated into selected language every time the game starts, the language is changed, or the 'Reset Static Manager & Cache' button is pressed.

    <img width="230" height="581" alt="image" src="https://github.com/user-attachments/assets/9b6a345c-356f-4858-a1d0-5765fb43bb77" />

### Code Examples
```csharp
using ardat11_Localization;

// Sets the language globally. This automatically updates all UI elements associated with a LocalizedText script.
LocalizationManager.CurrentLanguage = "tr";

// Retrieves a translation manually. Use this for dynamic content, such as item listings or hover tooltips.
string val = LocalizationManager.Localize("start_game_key");
