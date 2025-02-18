#WebView Tutorial in Java for Android** on GitHub.

```markdown
# WebView Tutorial for Android in Java

This tutorial demonstrates how to implement a WebView in an Android app using Java. WebView allows you to display web content inside your application, making it useful for displaying websites or web-based content.

## Prerequisites
- Android Studio
- A basic understanding of Android development and Java

## Steps to Create WebView in Android

### 1. **Setting up your Android Project**

Open **Android Studio** and create a new project.

- Select "Empty Activity."
- Choose **Java** as the programming language.
- Name your project (e.g., `WebViewTutorial`).

### 2. **Add Permissions to AndroidManifest.xml**

Before using WebView, you may need to add the appropriate permission for accessing the internet. Open the `AndroidManifest.xml` file and add the following line inside the `<manifest>` tags:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

### 3. **Modify Your Layout File (activity_main.xml)**

Inside `res/layout/activity_main.xml`, add a WebView widget where you want to display the content.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <android.webkit.WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</RelativeLayout>
```

### 4. **Java Code for WebView (MainActivity.java)**

In `MainActivity.java`, initialize the WebView and load a URL:

```java
import android.os.Bundle;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private WebView webView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize WebView
        webView = findViewById(R.id.webview);
        
        // Enable JavaScript
        webView.getSettings().setJavaScriptEnabled(true);

        // Set WebViewClient to handle page loading within the app
        webView.setWebViewClient(new WebViewClient());

        // Load a URL (example: Google's homepage)
        webView.loadUrl("https://www.google.com");
    }
}
```

### 5. **Handling Invalid URL Input (Optional)**

To handle invalid URL input and perform a Google search if the URL is not valid, use the following logic in `MainActivity.java`:

```java
import android.webkit.WebView;
import android.webkit.WebViewClient;

import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MainActivity extends AppCompatActivity {

    private WebView webView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        webView = findViewById(R.id.webview);
        webView.getSettings().setJavaScriptEnabled(true);
        webView.setWebViewClient(new WebViewClient());

        String input = "https://www.example.com"; // Example input, this could come from user input
        loadUrlOrSearch(webView, input);
    }

    public void loadUrlOrSearch(WebView webView, String input) {
        String urlPattern = "^(https?:\\/\\/)?([\\w\\-]+\\.)+[\\w]{2,}(\\/[\\w\\-._~:/?#\\[\\]@!$&'()*+,;=]*)?$";
        Pattern pattern = Pattern.compile(urlPattern);
        Matcher matcher = pattern.matcher(input);

        String url;
        if (matcher.matches()) {
            url = input.startsWith("http") ? input : "https://" + input;
        } else {
            url = "https://www.google.com/search?q=" + input.replace(" ", "+");
        }

        webView.loadUrl(url);
    }
}
```

### 6. **Run Your App**

Once you've written the code, connect an Android device or start an emulator. Click the "Run" button in Android Studio to see your WebView in action.

### 7. **Handling WebView Settings**

You can customize your WebView further by enabling JavaScript, controlling navigation, handling redirects, etc. Here are some useful settings:

```java
// Enable JavaScript
webView.getSettings().setJavaScriptEnabled(true);

// Handle redirects within the WebView (default is external browser)
webView.setWebViewClient(new WebViewClient());

// Enable zoom controls
webView.getSettings().setBuiltInZoomControls(true);
webView.getSettings().setDisplayZoomControls(false);
```

### 8. **Common Errors**

- **WebView not loading:** Ensure that you have internet permissions (`INTERNET`) in your manifest.
- **WebView crashes:** Make sure to check for any potential issues with the URL format or unsupported JavaScript content.

### 9. **Useful Resources**
- [Android WebView Documentation](https://developer.android.com/reference/android/webkit/WebView)
- [Regex for URLs](https://www.regular-expressions.info/url.html)
