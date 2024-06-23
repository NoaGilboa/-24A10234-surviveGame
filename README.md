# Survive Game

## Explanation of the Work Process:

### Initial Setup:
- **Decompile the APK:**
  - Used online decompilation tools to convert the APK file back into readable source code and resources.

### Review Decompiled Code:
- Analyzed the decompiled Java files and resource files to understand the structure and logic of the application.

  The APK has been decompiled, and a significant number of files have been extracted. To determine which files are relevant for reverse engineering and getting the application to work, we should focus on the following key components:
  
  1. **Manifest File:**
      - `AndroidManifest.xml`: This file contains essential information about the app, including its components, permissions, and other configurations.
    
  2. **Source Code:**
      - Java files in the `sources` directory: These files contain the logic of the application. Look for the main activity and other significant activities or fragments related to the gameplay.
      - Identify files related to user input (ID entry) and the game logic to "find the way to survive and reach your city."

  3. **Resources:**
      - `res` directory: Contains layouts, images, strings, and other resources used by the application.
      - `res/layout`: XML layout files that define the UI components.
      - `res/drawable`: Images and other drawable resources.
      - `res/values`: XML files defining strings, colors, and styles.

  The `AndroidManifest.xml` file provides a concise overview of the application's structure and essential components. Here are the key points:

  - **Package Name:** `com.classy.survivegame`
  - **SDK Versions:**
    - `minSdkVersion`: 24
    - `targetSdkVersion`: 30
  - **Permissions:** The app requests internet permission (`android.permission.INTERNET`).

  - **Activities:**
    - `com.classy.survivegame.Activity_Game`: This activity likely contains the main gameplay logic and user interface. It is set to portrait orientation.
    - `com.classy.survivegame.Activity_Menu`: This activity appears to be the entry point of the application (launcher activity) and is also set to portrait orientation.

  To proceed, the next steps include:
  - **Examining `Activity_Menu`:** This activity should handle the ID input when the game starts.
  - **Examining `Activity_Game`:** This activity contains the game logic and user interactions.
  - **Inspecting Resources:**
    - `res/layout`: Layout files defining the UI components.
    - `res/values`: Strings, colors, and styles.
### Identify and Fix Bugs:
#### `Activity_Game.java`
1. **Update Toast Messages:**

   Change:
   ```java
     Toast.makeText(this, "Survived in " + state, 1).show();
     } else {
     Toast.makeText(this, "You Failed ", 1).show();
   ```
     
   To:
    ```java
    Toast.makeText(this, "Survived in " + state, Toast.LENGTH_SHORT).show();
    } else {
    Toast.makeText(this, "You Failed ", Toast.LENGTH_SHORT).show();
   ```
   
2. **Update Integer Parsing:**

   Change:
    ```java 
      iArr[i] = Integer.valueOf(String.valueOf(id.charAt(i))).intValue() % 4;
    ```

    To:
    ```java
        iArr[i] = Integer.parseInt(String.valueOf(id.charAt(i))) % 4;
     ```

3. **Fix URL**


### Apply Necessary Changes:
Updated the Toast message display duration for better user experience.
Simplified integer parsing logic.

### Testing and Validation:
Ran the application on an emulator or device to test the changes.
Ensured the game logic works as expected, and the correct toast message is displayed upon successful completion.

#### Example ID and Steps:
1. **Enter a valid ID:**
    - Example ID: "123456789"
    - Derived Steps:
       - The `steps` array will be derived as follows:
          - Character at index 0 ('1') -> 1 % 4 = 1 (Right)
          - Character at index 1 ('2') -> 2 % 4 = 2 (Up)
          - Character at index 2 ('3') -> 3 % 4 = 3 (Down)
          - Character at index 3 ('4') -> 4 % 4 = 0 (Left)
          - Character at index 4 ('5') -> 5 % 4 = 1 (Right)
          - Character at index 5 ('6') -> 6 % 4 = 2 (Up)
          - Character at index 6 ('7') -> 7 % 4 = 3 (Down)
          - Character at index 7 ('8') -> 8 % 4 = 0 (Left)
          - Character at index 8 ('9') -> 9 % 4 = 1 (Right)
2. **Follow the steps:** 
   - Press the buttons in the correct order as derived from the ID.


### Video Demonstration:
Here is a video demonstration of the game:

https://github.com/NoaGilboa/surviveGame/assets/143444119/97f1074a-3a0b-4944-beea-4d419f62ffec

