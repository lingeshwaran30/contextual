# 3. Develop an Android Application Implementing Contextual Menus and Popup Menus

[← Back to Index](README.md)

## Project Name
`MenuDemo`

## Aim
To develop an Android application that implements **Contextual Menus** and **Popup Menus** using Android Studio.

## 1. File Name: `activity_main.xml`

**File Path:** `app/src/main/res/layout/activity_main.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="20dp">

    <TextView
        android:id="@+id/txtContext"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Long Press Me"
        android:textSize="24sp"
        android:padding="20dp" />

    <Button
        android:id="@+id/btnPopup"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Show Popup Menu"
        android:layout_marginTop="30dp" />

</LinearLayout>
```

## 2. Create a Menu Resource Directory

Follow these steps in Android Studio:

1. Right-click the `res` directory.
2. Select **New → Android Resource Directory**.
3. Set **Directory name** to `menu`.
4. Set **Resource type** to `menu`.
5. Click **OK**.

## 3. File Name: `menu_options.xml`

**File Path:** `app/src/main/res/menu/menu_options.xml`

Create a new Menu Resource File named `menu_options.xml` inside the `menu` directory.

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/menu_edit"
        android:title="Edit" />

    <item
        android:id="@+id/menu_delete"
        android:title="Delete" />

    <item
        android:id="@+id/menu_share"
        android:title="Share" />

</menu>
```

## 4. File Name: `MainActivity.java`

**File Path:** `app/src/main/java/com/example/menudemo/MainActivity.java`

```java
package com.example.menudemo;

import android.os.Bundle;
import android.view.ContextMenu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.PopupMenu;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    TextView txtContext;
    Button btnPopup;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        txtContext = findViewById(R.id.txtContext);
        btnPopup = findViewById(R.id.btnPopup);

        // Register Context Menu
        registerForContextMenu(txtContext);

        // Display Popup Menu when the button is clicked
        btnPopup.setOnClickListener(v -> {
            PopupMenu popupMenu =
                    new PopupMenu(MainActivity.this, btnPopup);

            popupMenu.getMenuInflater().inflate(
                    R.menu.menu_options,
                    popupMenu.getMenu()
            );

            popupMenu.setOnMenuItemClickListener(item -> {
                Toast.makeText(
                        MainActivity.this,
                        item.getTitle(),
                        Toast.LENGTH_SHORT
                ).show();

                return true;
            });

            popupMenu.show();
        });
    }

    // Context Menu Creation
    @Override
    public void onCreateContextMenu(
            ContextMenu menu,
            View v,
            ContextMenu.ContextMenuInfo menuInfo) {

        super.onCreateContextMenu(menu, v, menuInfo);

        menu.setHeaderTitle("Select Option");

        getMenuInflater().inflate(
                R.menu.menu_options,
                menu
        );
    }

    // Context Menu Click Handling
    @Override
    public boolean onContextItemSelected(
            @NonNull MenuItem item) {

        Toast.makeText(
                this,
                item.getTitle(),
                Toast.LENGTH_SHORT
        ).show();

        return true;
    }
}
```

**Important:** Ensure that the package name in `MainActivity.java` matches your app's package name. If your project uses a different package, update the `package` declaration accordingly.

## 5. Explanation

### Contextual Menu
- A Contextual Menu appears when the user **long-presses** the `TextView` displaying "Long Press Me".
- The menu contains three options: Edit, Delete, and Share.
- Selecting an option displays its title in a Toast message.

### Popup Menu
- A Popup Menu appears when the user clicks the **Show Popup Menu** button.
- It uses the same `menu_options.xml` resource file.
- Selecting Edit, Delete, or Share displays the selected option in a Toast message.

## 6. Expected Output

1. The application displays the text **Long Press Me** and a **Show Popup Menu** button.
2. Long-pressing the text opens a Contextual Menu containing Edit, Delete, and Share.
3. Clicking the button opens a Popup Menu containing the same three options.
4. Selecting any menu option displays a Toast message with the selected option's name.

## 7. Result

Thus, an Android application implementing **Contextual Menus and Popup Menus** was developed successfully.

## 8. Upload the Project to GitHub

1. Open your project folder.
2. Create or update the `README.md` file with this content.
3. Save the file.
4. Open your GitHub repository.
5. Commit and push your changes.

### Git Commands

```bash
git add README.md
git commit -m "Add Contextual and Popup Menus practical"
git push
```

**Note:** The Edit, Delete, and Share options currently display Toast messages only. They do not perform actual editing, deletion, or sharing operations.
