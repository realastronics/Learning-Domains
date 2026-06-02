# Mobile Application Development
## 1) Basic Background

We are using JAVA instead of Kotlin or Flutter because Kotlin is very similar to JAVA and Flutter can be learnt anytime. JAVA is a pre-requisite for this course on Mobile App Development.

Android - is an environment which is comprised of mobile based Operating System (built on a Linux Kernel), an interface for development, and application ecosystem. It was built as open source project for digital cameras, later acquired by Google and put under the Open Handset Alliance (OHA), releasing in 2007.

Android Libraries is a reusable collection of code and resources (like layouts, images, and manifest files) that can be easily integrated into multiple Android application modules.

First android phone to be released was HTC Dream.

XML (eXtensible Markup Language) a language that is used to supply and store the data for designing of it in a text based document.

Gradle is the build automation tool that retries data from XML, parallelly complies the code data, fetches all the libraries.

**DVM vs. ART**

- **Dalvik Virtual Machine (DVM):** The original runtime environment for Android. It was designed to run multiple instances efficiently on low-memory devices.
- **Android Runtime (ART):** The modern successor that **replaced DVM**. ART improves app performance by using Ahead-of-Time (AOT) compilation, which compiles the app's code into machine code during installation rather than every time the app runs.

**DEX and the Compilation Process:** The path from code to a runnable app follows this sequence:

1. **Source Code:** Written in **Java or Kotlin**.
2. **Java Bytecode:** The code is compiled into `.class` files using `javac`.
3. **DEX Bytecode:** A tool called **D8 (or DEX)** converts `.class` files into `.dex` (**Dalvik Executable**) files. This format is highly optimized for Android's limited resources.

**APK and AAB**

- **APK (Android Package Kit):** A ZIP archive format used to distribute and install apps. It contains the `.dex` code files and all compiled resources (like `AndroidManifest.xml`).
- **AAB (Android App Bundle):** A newer publishing format introduced with Android Studio 3.2. Unlike an APK, an AAB is not directly installed. Google Play uses it to generate optimized APKs specifically tailored to a user's device configuration, reducing download sizes

**SDK Tools and AVD Manager**

- **SDK Manager:** Allows you to download different **API levels** (Android versions). You generally want to install the latest stable version and a few older ones to test compatibility.
- **AVD (Android Virtual Device) Manager:** This tool lets you create an **Emulator**. An emulator is a "virtual" phone that runs on your computer so you can test your app without a physical device

## 2) Components of An Android Application

1. Activity: the interactive screen which gets displayed to the user. Back Stack is the mechanism that switches one activity to another at the request of the user, the structure of it is similar to that of stack.
2. Service
3. Broadcast Receiver
4. Content Provider

## 3) Activities

**1. What is an Activity?**

**Activity** is a single screen in an application that provides a user interface. For example, a dialer screen or a Google Maps screen are individual activities. When you first open an app, the specific screen that appears is the **Main Activity** or default Activity.

**2. The Back Stack Mechanism**

Android manages activities using a **Back Stack**. When a new activity starts, the current activity is stopped and pushed onto the top of this stack. When the user taps the **Back button**, the current activity is popped off the stack and **destroyed**, allowing the previous activity to resume focus. As app complexity increases, the number of activities proportionally increases to handle different functionalities.

**3. Creating and Registering an Activity**

To create a functional activity, you must perform two essential steps:

- **The Java Class:** Your class must inherit from **AppCompatActivity**. This specific base class is preferred because it ensures **backward compatibility**, provides a consistent design, and allows you to leverage modern Android features effectively.
- **The Manifest Declaration:** You **must** register every activity in the **`AndroidManifest.xml`** file using the **`<activity>`** tag within the **`<application>`** tag. If you fail to register an activity, it will not display, and the system will trigger a **runtime error** when you try to run the application.
- **Entry Point:** In the Manifest, you declare which activity is the starting point using an **`<intent-filter>`** with the actions **`MAIN`** and **`LAUNCHER`**.

**4. Technical Setup: onCreate() and setContentView()**

The **onCreate()** method is the very first method called when an activity loads into memory. It acts similarly to the **`main()`** method in standard Java programs, serving as the static entry point for your code.

- **setContentView():** Inside **`onCreate()`**, this fundamental method connects your Java logic with its XML layout (e.g., **`R.layout.activity_main`**).
- **Static Setup:** This is where you perform "once-only" startup logic, such as creating views or binding data to lists.

**R.java** tells the system **where** the layout is, and **setContentView()** tells the system to actually **put it on the screen**

## **4) The Activity Lifecycle: The 3 Core States**

An Activity exists in one of three primary states as managed by the Android runtime:

1. **Resumed (Running):** The activity is in the foreground, fully visible, and has the user's focus.
2. **Paused:** Another activity is in the foreground, making the current activity partially visible but without focus. The activity object remains **alive in memory** and attached to the window manager.
3. **Stopped:** The activity is completely hidden in the background. It remains alive in memory but relinquishes its involvement with the window manager.

**6. The Lifecycle Callback Methods (Detailed)**

The "lifecycle" refers to the journey an activity takes from creation to destruction. Each stage has a specific **callback method**:

- **onCreate():** Called when the activity is first created. It receives a **Bundle** object that can store the previous state of the activity.
- **onStart():** Invoked as the activity becomes visible to the user. This initializes the code that maintains the UI.
- **onResume():** Called just before the activity enters the foreground and becomes interactive. The app stays here until focus is taken away (e.g., a phone call or screen turn-off).
- **onPause():** The first indication the user is leaving the activity. It does not always mean the activity is being destroyed; it may stay visible in multi-window mode.
- **onStop():** Called when the activity is no longer visible. This happens when a new activity covers the full screen or the activity finishes running.
- **onRestart():** If a stopped activity is coming back to the user, this is called before **`onStart()`**.
- **onDestroy():** The final call before the activity is removed from memory. This occurs if the user dismisses the activity (**`finish()`** is called) or due to a **configuration change** like rotating the device.

**7. Process Death and State Preservation**

If the system runs low on memory, the Android runtime can **kill** an activity process. The system is most likely to kill an activity after the **`onPause()`**, **`onStop()`**, or **`onDestroy()`** methods have executed.

- **Saving State:** To prevent data loss when an activity is killed by the system (not by the user), Android uses **onSaveInstanceState()**.
- **Bundle:** You can save information as **name-value pairs** inside a **`Bundle`** object using methods like **`putInt()`** or **`putString()`**.
- **Restoration:** When the user navigates back to a killed activity, the system passes that **`Bundle`** back into **`onCreate()`** or **onRestoreInstanceState()** to recover the data.

## 5) Intents

**Intent** is essentially an asynchronous message or a "request for action" that you send to the Android runtime. It allows your application to request functionality from other components, whether they are within your own app or part of another app on the device.

**2. Explicit Intents: Internal Navigation**

**Explicit Intents** are used when you know exactly which component you want to start. This is most common for navigating between screens inside your own application.

- **How it works:** You specify the current context (the current Activity) and the exact Class of the destination Activity.
- **The Code Path:**
    1. **Create the Intent:** **`Intent intent = new Intent(MainActivity.this, TargetActivity.class);`**.
    2. **Start the Activity:** Call **`startActivity(intent);`** which tells the system to push the new Activity onto the **Back Stack** and bring it to the foreground.

**3. Implicit Intents: External Actions**

**Implicit Intents** do not name a specific class. Instead, they declare a general **action** to be performed (like "opening a URL", "sharing a text", or "making a phone call").

- **The System Role:** The Android system looks at all installed apps to see which ones have declared they can handle that specific action. If multiple apps can do it (e.g., multiple browsers for a URL), the system presents a "chooser" to the user.
- **Common Actions:** Sharing data, opening the camera, or dialing a number.

**4. Intent Filters**

For an Activity to be able to receive Implicit Intents, it must declare its capabilities in the **`AndroidManifest.xml`** using **<intent-filter>** tags.

- **Structure:** An intent filter specifies the **Action** (what it can do) and the **Category** (additional details about the component).
- **The Launcher Example:** Every app's main entry point has an intent filter with the action **`android.intent.action.MAIN`** and the category **`android.intent.category.LAUNCHER`**. This tells the Android OS that this Activity is the one to start when the user taps the app icon.

**5. Passing Data Between Activities**

Intents are not just for navigation; they are also data carriers.

- **Extras:** You can attach simple data (like strings, integers, or Booleans) to an Intent using "Extras" before starting the activity.
- **Mechanism:** Data is stored as **name-value pairs**.
    - **Sending:** **`intent.putExtra("USER_NAME", "Nikhil");`**
    - **Receiving:** In the destination Activity, you use **`getIntent().getStringExtra("USER_NAME");`** to retrieve the value.
- **Bundles:** For more complex data sets, you can wrap multiple pieces of information into a **Bundle** object and attach the entire bundle to the Intent.

## 6) Views

- **View:** A View is a rectangular area on the screen that draws something and handles user events (like a button or a text field). All UI components are subclasses of the base **`View`** class.
- **ViewGroup:** Also known as a **Layout Manager**, a ViewGroup is an invisible container that holds other Views or ViewGroups. It defines the structure and arrangement of its children on the screen.
- **Tree Structure:** An Android UI is essentially a "tree" where the root is a ViewGroup (like a RelativeLayout), and its branches are individual Views or nested ViewGroups.

**2. Essential Measurement Units**

When defining the size of your Views, choosing the right unit is critical for your quiz:

- **dp (Density-independent Pixel):** Recommended for specifying the **size of Views** (width, height, margins). It ensures the View looks the same size across different screen densities (e.g., 160 dp equals roughly one physical inch).
- **sp (Scale-independent Pixel):** Recommended specifically for **font sizes**. Like dp, it scales with density, but it also respects the user's system-wide font size preferences.
- **px (Pixel):** Represents a single physical pixel. **Not recommended**, as it does not scale, making UIs look tiny on high-resolution screens and huge on low-resolution ones.

**3. Size Constants: Controlling Layout Space**

Instead of hardcoding numbers, you typically use these two predefined constants:

- **match_parent:** The View grows to be as large as its parent container.
- **wrap_content:** The View shrinks to be just big enough to surround its own content (like the text inside a button).

**4. Core Android Views**

**TextView (Display Only)**

Used to display text to the user.

- **Key Attributes:** **`android:text`** (the message), **`android:textSize`** (in sp), **`android:textColor`** (referencing **`colors.xml`**), and **`android:textStyle`** (bold/italic).
- **Coding Tip:** To avoid warnings, strings should be stored in **`strings.xml`** rather than hardcoded in XML.

**EditText (User Input)**

A subclass of TextView that allows users to type information.

- **Hint:** Use **`android:hint`** to provide a placeholder (like "Enter your name") that disappears when the user starts typing.
- **Input Type:** You can restrict input using **`android:inputType`** (e.g., **`textPassword`**, **`phone`**, or **`textEmailAddress`**) to change the keyboard behavior.

**Buttons & ImageButtons**

- **Button:** A standard clickable component with a text label.
- **ImageButton:** Similar to a button but displays an image or icon instead of text.
- **Handling Clicks:** You can use the **`android:onClick`** attribute in XML or **`setOnClickListener()`** in Java.

**Binary Selection: ToggleButton, Switch, & CheckBox**

- **CheckBox:** Used when a user can select **multiple** options from a list (e.g., "Select your interests").
- **ToggleButton/Switch:** Used for binary "On/Off" states (e.g., "Enable Notifications").

**Mutually Exclusive Selection: RadioButton & RadioGroup**

- **RadioButton:** Used when a user must choose exactly **one** option from a set.
- **RadioGroup:** RadioButtons **must** be wrapped in a **`RadioGroup`** container to work correctly. Without the group, the system won't know they are related, allowing the user to select more than one.

**Pickers**

- **TimePicker & DatePicker:** Special views that provide a standard UI for users to select a time or date, ensuring a consistent experience across all Android apps.

## 7) Layouts

In Android development, the distinction between a **View** and a **Layout** (technically called a **ViewGroup**) is fundamental to how user interfaces are constructed and managed.

**1. The View: Individual Components**

A **View** is a single, rectangular graphical component on the screen that a user can see or interact with. Views are the building blocks of your UI and are often referred to as "widgets".

- **Purpose:** Its primary role is to **draw content** and **handle user events** (like clicks or text input).
- **Examples:** Common views include **TextView** (for displaying text), **Button** (for clickable actions), **EditText** (for user input), and **ImageView** (for displaying pictures).
- **Technical Root:** All UI components in Android are subclasses of the base **`android.view.View`** class.

**2. The Layout (ViewGroup): The Containers**

A **Layout**, or **ViewGroup**, is an invisible container that holds multiple **Views** and other **ViewGroups**. It is responsible for the **arrangement and structure** of the interface.

- **Purpose:** Its primary role is to **organize and position** its children views on the screen. Without a layout, views would simply overlap at the top-left corner of the screen (0,0 coordinate).
- **Examples:** Common layout managers include **LinearLayout** (arranges views in a single row or column), **RelativeLayout** (positions views relative to each other or the parent), and **ConstraintLayout** (uses constraints to create complex, flexible designs).
- **Technical Root:** A Layout is a subclass of **`android.view.ViewGroup`**, which itself inherits from the **View** class. This means a Layout is technically a special kind of View that can contain other views.

**3. Key Differences at a Glance**

|**Feature**|**View**|**Layout (ViewGroup)**|
|---|---|---|
|**Visibility**|**Visible** to the user (draws something).|Usually **invisible** (acts as a manager).|
|**Primary Job**|Displays information or captures interaction.|Arranges and holds components in a specific order.|
|**Nesting**|Cannot contain other components.|Can contain both **Views** and other **ViewGroups**.|
|**Hierarchy**|Represents the **leaves** of the UI tree.|Represents the **branches/roots** of the UI tree.|
|**Attributes**|Focused on content: **`text`**, **`src`**, **`hint`**.|Focused on positioning: **`orientation`**, **`below`**, **`constraints`**.|

**4. How They Work Together (The Hierarchy)**

Android UI is built using a **View Hierarchy**. When you call **`setContentView(R.layout.activity_main)`** in your Activity, the system "inflates" the XML file, creating a tree structure where a **Layout** is at the top (the root), and individual **Views** are placed inside it.

For example, if you have a **`LinearLayout`** containing a **`Button`**, the **`LinearLayout`** calculates where the **`Button`** should go, and the **`Button`** handles the actual drawing of its label and the logic for when it is tapped

## 8) UI Components

These are the individual building blocks (Views) that users see and interact with to provide data or trigger actions.

**1. Text Display and Input**

- **TextView:** Primarily used for displaying static or dynamic text that the user cannot edit. Key attributes include **`android:text`**, **`android:textSize`** (measured in **sp**), and **`android:textColor`**.
- **EditText:** A subclass of TextView that allows user input.
    - **Hint vs. Text:** Use **`android:hint`** to provide placeholder text (e.g., "Enter Email") that disappears when the user starts typing.
    - **Input Type:** The **`android:inputType`** attribute is vital for user experience; it defines whether the keyboard shows numbers, email symbols, or masks characters for a password.

**2. Buttons and Clickable Views**

- **Button:** A standard push-button with a text label.
- **ImageButton:** Functions like a button but displays an image instead of text.
- **Event Handling (Click Listeners):**
    - **XML Method:** You can define **`android:onClick="methodName"`** in the XML and create a matching public method in Java.
    - **Java Method:** More commonly, you use **`setOnClickListener()`** in your **`onCreate()`** method to handle logic directly in the code.

**3. Selection Components (Binary)**

- **CheckBox:** Used when a user can select **multiple options** from a set (e.g., "Choose your hobbies"). You can check its state in Java using the **`.isChecked()`** method.
- **ToggleButton and Switch:** These are used for binary "on/off" or "true/false" settings, such as enabling Wi-Fi or notifications.

**4. Mutually Exclusive Selection (RadioGroup)**

- **RadioButton:** Used when a user must choose exactly **one option** from a list.
- **RadioGroup:** This is a mandatory container for RadioButtons. If you do not wrap your RadioButtons in a **`RadioGroup`**, the system will allow the user to select more than one at a time, which breaks the logic of mutual exclusivity.
    - **Java Implementation:** You typically use an **`OnCheckedChangeListener`** on the **`RadioGroup`** to detect which specific button ID was selected.

**5. Specialized Pickers**

- **TimePicker and DatePicker:** These provide a standard, system-consistent interface for users to select times and dates. Using these ensures your app feels native to the Android ecosystem.

## Important Stuff

**1. What is a Toast?**

A **Toast** is a temporary message that pops up on the screen to provide execution feedback about an operation. It only fills the amount of space required for the message, and the current activity remains visible and interactive underneath it.

- **Syntax Breakdown:** **`Toast.makeText(MainActivity.this, "Message", Toast.LENGTH_SHORT).show();`**
    - **Context:** **`MainActivity.this`** identifies the current activity.
    - **Text:** The string you want to display (e.g., "Correct" or "onPause() is called").
    - **Duration:** **`Toast.LENGTH_SHORT`** or **`Toast.LENGTH_LONG`** determines how long it stays visible.
    - **Crucial Step:** You **must** call **`.show()`** at the end, or the Toast will never appear.

**2. Using Java Code to Track the Lifecycle**

The sources provide a **skeleton code** to help you visualize the order of method execution. By placing Toasts inside each callback method, you can see the sequence in real-time:

- **App Start:** Executing **`onCreate()`**, **`onStart()`**, and **`onResume()`** produces three consecutive toast messages.
- **App Close:** Executing **`onPause()`**, **`onStop()`**, and **`onDestroy()`** also triggers three consecutive toasts.

**3. Event Handling Logic**

**A. RadioButton Logic**

In this code, the Activity implements **`RadioGroup.OnCheckedChangeListener`**.

1. **Linking:** Elements are found using **`rg = findViewById(R.id.rg1)`**.
2. **Listener:** The **`rg.setOnCheckedChangeListener(this)`** tells the system to call the **`onCheckedChanged`** method when a selection changes.
3. **Logic:** Inside **`onCheckedChanged`**, the code gets the ID of the selected button, retrieves the text, and converts it to a string using **.toString()**.
4. **Comparison:** It uses **`s.compareToIgnoreCase(key)`** to check if the answer is "Correct" and displays the result via a **Toast**.

**B. String Concatenation Logic**

This shows how to manipulate text dynamically:

1. **Retrieving Input:** **`String s1 = t1.getText().toString();`** gets the text from a TextView or EditText.
2. **Logic:** **`String s3 = s1 + " " + s2;`** uses standard Java concatenation.
3. **Updating UI:** **`t3.setText(s3);`** pushes the new string back to the screen.

**4. Standard Java Operations in Android**

Java-specific steps required for Android development:

- **Finding Views:** **`findViewById(R.id.id_name)`** is the mandatory method to link a Java variable to an XML component.
- **The Bridge:** **R.java** is an auto-generated file that serves as a bridge, interpreting XML component references into unique integer IDs for the Java file.
- **Importing Classes:** You must import specific packages, such as **`android.widget.Toast`** or **`android.view.View`**, to use their functionality.
- **Inheritance:** Every Activity class **must** extend **`AppCompatActivity`** to inherit core Android features.