[[longer explanation with longer code]]
[[super short code]]
# JavaFX UI Controls - Short Demonstration

Here's a **condensed version** with shorter code for each control, keeping the explanations.

---

## 1. Label

**What it is:** Non-editable text display.

```java
Label label = new Label("User Name:");
label.setStyle("-fx-font-size: 14px; -fx-text-fill: blue;");
```

---

## 2. TextField

**What it is:** Single-line text input.

```java
TextField textField = new TextField();
textField.setPromptText("Enter your name");
String value = textField.getText();  // Get input
```

---
![[Pasted image 20260607103850.png]]

![[Pasted image 20260607103905.png]]

---

## 3. Button

**What it is:** Clickable control that performs an action.

```java
Button button = new Button("Click Me");
button.setOnAction(e -> System.out.println("Button clicked!"));
```

---

## 4. RadioButton

**What it is:** Circular button; only ONE in a group can be selected.

```java
ToggleGroup group = new ToggleGroup();
RadioButton option1 = new RadioButton("Yes");
RadioButton option2 = new RadioButton("No");
option1.setToggleGroup(group);
option2.setToggleGroup(group);
option1.setSelected(true);  // Default selection
```

---

## 5. CheckBox

**What it is:** Square box; multiple can be selected independently.

```java
CheckBox check1 = new CheckBox("Reading");
CheckBox check2 = new CheckBox("Music");
check1.setSelected(true);  // Initially checked
boolean isChecked = check1.isSelected();  // Get state
```

---

## 6. Hyperlink

**What it is:** Clickable text link (like web link).

```java
Hyperlink link = new Hyperlink("Click here");
link.setOnAction(e -> System.out.println("Link clicked!"));
```

---

## 7. Menu (MenuBar, Menu, MenuItem)

**What it is:** Drop-down menu system at top of window.

```java
MenuBar menuBar = new MenuBar();
Menu fileMenu = new Menu("File");
MenuItem newItem = new MenuItem("New");
newItem.setOnAction(e -> System.out.println("New file"));
fileMenu.getItems().add(newItem);
menuBar.getMenus().add(fileMenu);
```

---

## 8. Tooltip

**What it is:** Popup help text on mouse hover.

```java
Button button = new Button("Save");
Tooltip tooltip = new Tooltip("Save the file");
button.setTooltip(tooltip);
```

---

## 9. FileChooser

**What it is:** System dialog to select files/directories.

```java
FileChooser fileChooser = new FileChooser();
fileChooser.setTitle("Select a File");
File file = fileChooser.showOpenDialog(stage);
if (file != null) {
    System.out.println("Selected: " + file.getName());
}
```

---

## Complete Short Example (All Controls Together)

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;
import java.io.File;

public class ShortControlsDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create all controls
        Label nameLabel = new Label("Name:");
        TextField nameField = new TextField();
        nameField.setPromptText("Enter name");
        
        Button submitBtn = new Button("Submit");
        Label resultLabel = new Label();
        
        // RadioButtons
        ToggleGroup genderGroup = new ToggleGroup();
        RadioButton male = new RadioButton("Male");
        RadioButton female = new RadioButton("Female");
        male.setToggleGroup(genderGroup);
        female.setToggleGroup(genderGroup);
        
        // CheckBoxes
        CheckBox termsCheck = new CheckBox("Accept Terms");
        
        // Hyperlink
        Hyperlink helpLink = new Hyperlink("Need help?");
        
        // Tooltip
        submitBtn.setTooltip(new Tooltip("Click to submit"));
        
        // FileChooser
        Button fileBtn = new Button("Choose File");
        Label fileLabel = new Label("No file");
        fileBtn.setOnAction(e -> {
            File file = new FileChooser().showOpenDialog(stage);
            if (file != null) fileLabel.setText(file.getName());
        });
        
        // Menu
        MenuBar menuBar = new MenuBar();
        Menu fileMenu = new Menu("File");
        MenuItem exitItem = new MenuItem("Exit");
        exitItem.setOnAction(e -> stage.close());
        fileMenu.getItems().add(exitItem);
        menuBar.getMenus().add(fileMenu);
        
        // Submit action
        submitBtn.setOnAction(e -> {
            String gender = male.isSelected() ? "Male" : (female.isSelected() ? "Female" : "Not selected");
            resultLabel.setText("Name: " + nameField.getText() + 
                               ", Gender: " + gender + 
                               ", Terms: " + (termsCheck.isSelected() ? "Accepted" : "Not accepted"));
        });
        
        helpLink.setOnAction(e -> resultLabel.setText("Help: Enter name, select gender, accept terms"));
        
        // Layout
        GridPane grid = new GridPane();
        grid.setHgap(10);
        grid.setVgap(10);
        grid.setPadding(new javafx.geometry.Insets(20));
        
        grid.add(nameLabel, 0, 0);
        grid.add(nameField, 1, 0);
        grid.add(male, 0, 1);
        grid.add(female, 1, 1);
        grid.add(termsCheck, 0, 2, 2, 1);
        grid.add(helpLink, 0, 3);
        grid.add(fileBtn, 0, 4);
        grid.add(fileLabel, 1, 4);
        grid.add(submitBtn, 0, 5);
        grid.add(resultLabel, 0, 6, 2, 1);
        
        // Scene
        VBox root = new VBox(menuBar, grid);
        Scene scene = new Scene(root, 500, 400);
        stage.setTitle("JavaFX Controls Demo");
        stage.setScene(scene);
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

---

## Quick Reference Table

| Control | Creation | Key Method |
|---------|----------|------------|
| Label | `new Label("text")` | `setText()` |
| TextField | `new TextField()` | `getText()` |
| Button | `new Button("text")` | `setOnAction()` |
| RadioButton | `new RadioButton("text")` | `setToggleGroup()` |
| CheckBox | `new CheckBox("text")` | `isSelected()` |
| Hyperlink | `new Hyperlink("text")` | `setOnAction()` |
| MenuItem | `new MenuItem("text")` | `setOnAction()` |
| Tooltip | `new Tooltip("text")` | `setTooltip()` |
| FileChooser | `new FileChooser()` | `showOpenDialog()` |

---

## The Golden Rule

> **Labels display, TextFields input, Buttons act, RadioButtons group single choice, CheckBoxes allow multiple choices, Hyperlinks navigate, Menus organize, Tooltips help, FileChoosers select files. All combine with layouts to build JavaFX applications.**