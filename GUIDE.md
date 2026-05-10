# LoopieBot - Traveloop AI Integration Guide

This guide explains how to integrate the **LoopieBot** (Traveloop's custom AI Assistant) into both your React/Web Frontend and your Android Application.

The chatbot code is located in the `traveloop-bot` directory:
- `LoopieBot.jsx` (React Component)
- `LoopieBot.css` (Styles)

---

## 1. Web Frontend Integration (React)

To integrate LoopieBot into your existing React website (Traveloop Web Frontend):

### Step 1: Copy Files
Copy `LoopieBot.jsx` and `LoopieBot.css` into your frontend project's `src/components/Chatbot/` directory.

### Step 2: Import and Render
Import the component into your main layout file (e.g., `App.jsx`, `Layout.jsx`, or `index.js`) so that it is available globally on all screens.

```jsx
import React from 'react';
// Other imports...
import LoopieBot from './components/Chatbot/LoopieBot';

function App() {
  return (
    <div className="App">
      {/* Your main routing and components */}
      <Navigation />
      <MainContent />
      
      {/* Add LoopieBot here so it sits on top of your content */}
      <LoopieBot />
    </div>
  );
}

export default App;
```

### Features included:
- Built-in UI with Floating Action Button.
- Support logic handling via WhatsApp/Call integration (+91 9732395264).
- High-quality travel images from Unsplash.
- Interactive multi-step planning flow tailored to India.

---

## 2. Android Studio Integration (Mobile Application)

Since the chatbot is built with web technologies, the fastest and most reliable way to integrate it into your Android Application without duplicating the complex UI logic is to use an Android `WebView`.

### Step 1: Host the Web Version
If you have deployed your React web app (e.g., to Vercel/Netlify), the chatbot will be visible on the web. 
Alternatively, you can create a dedicated route for the bot (e.g., `https://your-traveloop.com/bot-mobile`) that *only* renders the `<LoopieBot />` in open state.

### Step 2: Create a Chatbot Activity in Android Studio
Create a new Activity in Android Studio (e.g., `ChatbotActivity.kt` or `.java`).

### Step 3: Add WebView to Layout (`activity_chatbot.xml`)
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <WebView
        android:id="@+id/chatbotWebView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### Step 4: Configure the WebView (`ChatbotActivity.kt`)
In your Kotlin file, enable JavaScript and load the URL where your chatbot is hosted.

```kotlin
import android.annotation.SuppressLint
import android.os.Bundle
import android.webkit.WebSettings
import android.webkit.WebView
import android.webkit.WebViewClient
import androidx.appcompat.app.AppCompatActivity

class ChatbotActivity : AppCompatActivity() {

    @SuppressLint("SetJavaScriptEnabled")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_chatbot)

        val webView: WebView = findViewById(R.id.chatbotWebView)
        val webSettings: WebSettings = webView.settings
        
        // Essential settings for React/JS to work
        webSettings.javaScriptEnabled = true
        webSettings.domStorageEnabled = true
        webSettings.loadsImagesAutomatically = true

        // Force links and redirects to open in the WebView instead of Chrome
        webView.webViewClient = WebViewClient()

        // Load the URL where your bot is hosted. 
        // Use 10.0.2.2 if testing locally via Android Emulator pointing to localhost
        webView.loadUrl("https://your-traveloop-domain.com/chatbot-route")
    }
}
```

### Step 5: Android Manifest Permissions
Ensure your `AndroidManifest.xml` has the required Internet permission.
```xml
<uses-permission android:name="android.permission.INTERNET" />
```

### Launching the Bot from the Android App
In your main Android dashboard (e.g., a Floating Action Button or Nav Menu), add a click listener to launch the `ChatbotActivity`:

```kotlin
val fabChatbot = findViewById<FloatingActionButton>(R.id.fab_chatbot)
fabChatbot.setOnClickListener {
    val intent = Intent(this, ChatbotActivity::class.java)
    startActivity(intent)
}
```

---

## 3. Customizing the Support Number
If you need to change the emergency support number, open `LoopieBot.jsx` and modify this line:
```javascript
const supportNumber = "+91 9732395264";
```
