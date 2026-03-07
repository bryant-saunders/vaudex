# Vaudex
Vaudex is a web application designed to store personal data like appointments, passwords, journal entries and other information in a end-to-end encypted database using IndexedDB 

<img width="375" height="666" alt="Screenshot 2026-03-01 142712" src="https://github.com/user-attachments/assets/ab67b4ed-ebc9-4155-abd7-1c7586aab1f6" />


# Features
1. End to end database encryption using PBKDF2 and AES-GCM with configurable iteration counts
3. Local database import/export with an optional cloud synchronization feature
4. Programmable auto-logout keeps unattended data safe
5. Dark/light mode toggle
6. Single file HTML page with vanilla JS allows easy hosting on your own server
7. Responsive to mobile and desktop layouts

# Usage
Vaudex provides four main interfaces for storing and editing data. Each one is designed for a particular purpose

1. **Collections:** Collections are a folder based structure where you put data like passwords, addresses, phone numbers and documents. This data is in the form of text, images or pictures taken from a built in camera. Vaudex will automatically compress images to save on space.
2. **Calendar:** This section allows you to create and view text items that are related to time. You would store information like birthdays, appointments, reminders and holidays here. You can create items with a specific date/time or create items that occur at daily, weekly, monthly or yearly intervals
3. **Tasks:** Here you can create simple reminders for things that you need to do, but don't have a specific date to complete it. Think of it like a "to do" list organized by when the task needs to be finished. You can also view previously completed items
4. **Journal:** With the journal you can write down anything that happens during your day. You could use this as a diary or just a simple log of important events

# Setup and installation
As mentioned above, Vaudex is a single enclosed HTML file. This allows you to simply run the file locally in your browser if you do not wish to host it. Your entire database is saved locally in your browser's storage. If you do wish to host the application, there are a couple of different methods and advantages,

1. **HTTP/HTTPS Server:** You can host Vaudex on any HTTP server so that you do not have to store a copy of the application on your device. This is necessary for certain enviroments that do not allow the user to open/run local HTML files
2. **Google Firebase:** Vaudex has a built in Firebase integration that allows authorized users to import/export their entire database to Firebase Storage. The data that is sent to Firebase is still encrypted with your master key, so no one can read your data except for you. This feature lets you import your database to any device with a internet connection. See the Firebase section below for details

# Why use Vaudex?
Vaudex is designed to be a very lightweight and secure data storage application that can run in any browser without installing anything. There are dedicated programs that perform the individual tasks like calendars and journals better, but Vaudex was created to keep your data private and fully under your control. If you are concerned about security and do not have another secure secrets application, Vaudex might be right for you.

# Firebase setup (Optional)
## Prerequisites
1. A Google Firebase account/project. A billing (Paid) account is necessary if this is not your only project!
2. Firebase Authentication, Storage and Hosting service activated
3. Firebase CLI installed and configured for your project. See here for more information https://firebase.google.com/docs/cli
4. A newly created or existing web app configured in Firebase

## Configuration
Replace the empty firebaseConfig string in the Vaudex source code with the account config from Firebase console. This can be found under Gear Icon>General>Your Apps

## Storage Rules
You will need to update the rules for Firebase Storage to support the paths that Vaudex uses to export/import database files. Below is a sample of a standalone rule that does the trick,

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    // Matches: vaudex_data / <user-id> / <filename>
    match /vaudex_data/{userId}/{allPaths=**} {
      // Only allow access if the authenticated user's ID matches the folder name
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## Authentication
You will need at least one user email/password combination configured in the Authentication menu

# Dependencies and credits
Vaudex uses the following libraries for core functionality,
1. **Pico CSS (MIT):** https://picocss.com/
2. **IDB-Keyval (APACHE 2.0):** https://github.com/jakearchibald/idb-keyval/tree/main
3. **Google Fonts/Material Icons (OFL):** https://fonts.google.com/

# Gallery
<div class="grid" markdown>
  <img width="24%" height="auto" alt="image" src="https://github.com/user-attachments/assets/c2397035-7f2e-453d-b82e-4fbc59b80aad" />
  <img width="24%" height="auto" alt="image" src="https://github.com/user-attachments/assets/619cab20-7340-46fe-8bb0-7ddf3860f1fe" />
  <img width="24%" height="auto" alt="image" src="https://github.com/user-attachments/assets/52e5e2d8-ffde-45f0-ac19-83a15250211f" />
  <img width="24%" height="auto" alt="image" src="https://github.com/user-attachments/assets/c69b2cd6-8f2c-45a8-a88a-4b553adb5ab2" />
</div>



