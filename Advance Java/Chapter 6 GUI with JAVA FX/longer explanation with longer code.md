# JavaFX UI Controls - Complete Guide

Here's a **complete explanation** of JavaFX UI Controls, what they are, why they're needed, and how to implement them with detailed code comments.

---

## What are JavaFX UI Controls?

**UI Controls** are interactive graphical elements that users interact with in a JavaFX application. They are the building blocks of any GUI application.

```
┌─────────────────────────────────────────────────────────────┐
│                    USER INTERFACE                           │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ Name: [_______________]  ← TextField                │   │
│  │                                                     │   │
│  │ Gender: ○ Male  ● Female  ← RadioButtons           │   │
│  │                                                     │   │
│  │ Interests: ☑ Reading  ☐ Music  ☑ Sports ← CheckBox │   │
│  │                                                     │   │
│  │ [Click Me] ← Button                                 │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

## 1. Label

**What it is:** A non-editable text display component. Used to display instructions, labels for other controls, or static text.

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class LabelDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create a simple label
        Label label1 = new Label("This is a simple label");
        
        // Create a label with custom styling
        Label label2 = new Label("Styled Label");
        label2.setStyle("-fx-font-size: 20px; -fx-text-fill: blue; -fx-font-weight: bold;");
        
        // Create a label with icon (image)
        // ImageView icon = new ImageView(new Image("file:icon.png"));
        // Label label3 = new Label("Label with Icon", icon);
        
        VBox vbox = new VBox(10);
        vbox.getChildren().addAll(label1, label2);
        
        Scene scene = new Scene(vbox, 300, 200);
        stage.setTitle("Label Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

---

## 2. TextField

**What it is:** A single-line text input control where users can type text.

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class TextFieldDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Basic text field
        TextField textField1 = new TextField();
        textField1.setPromptText("Enter your name");  // Hint text
        textField1.setPrefWidth(200);
        
        // Text field with initial text
        TextField textField2 = new TextField("Initial value");
        
        // Add event listener to react to text changes
        TextField textField3 = new TextField();
        textField3.setPromptText("Type something...");
        textField3.textProperty().addListener((observable, oldValue, newValue) -> {
            System.out.println("Text changed from: " + oldValue + " to: " + newValue);
        });
        
        Label resultLabel = new Label();
        
        // Action event (when Enter key is pressed)
        TextField textField4 = new TextField();
        textField4.setPromptText("Press Enter to submit");
        textField4.setOnAction(event -> {
            resultLabel.setText("You entered: " + textField4.getText());
        });
        
        VBox vbox = new VBox(10);
        vbox.getChildren().addAll(textField1, textField2, textField3, textField4, resultLabel);
        vbox.setStyle("-fx-padding: 20;");
        
        Scene scene = new Scene(vbox, 350, 250);
        stage.setTitle("TextField Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**Common methods:**
| Method | What it does |
|--------|--------------|
| `getText()` | Get the text entered |
| `setText(String text)` | Set text programmatically |
| `setPromptText(String text)` | Set hint text |
| `clear()` | Clear the text field |
| `setEditable(boolean)` | Make read-only or editable |

---

## 3. Button

**What it is:** A clickable control that performs an action when pressed.

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class ButtonDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        Label counterLabel = new Label("0");
        int[] counter = {0};
        
        // Simple button
        Button button1 = new Button("Click Me!");
        button1.setOnAction(event -> {
            counter[0]++;
            counterLabel.setText(String.valueOf(counter[0]));
            System.out.println("Button clicked! Count: " + counter[0]);
        });
        
        // Button with styling
        Button button2 = new Button("Styled Button");
        button2.setStyle("-fx-background-color: lightblue; -fx-font-size: 16px; -fx-padding: 10px;");
        
        // Disabled button
        Button button3 = new Button("Disabled Button");
        button3.setDisable(true);
        
        // Button with icon
        // ImageView icon = new ImageView(new Image("file:icon.png"));
        // icon.setFitWidth(16);
        // icon.setFitHeight(16);
        // Button button4 = new Button("With Icon", icon);
        
        VBox vbox = new VBox(15);
        vbox.getChildren().addAll(button1, counterLabel, button2, button3);
        vbox.setStyle("-fx-padding: 20;");
        
        Scene scene = new Scene(vbox, 300, 250);
        stage.setTitle("Button Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**Common methods:**
| Method | What it does |
|--------|--------------|
| `setOnAction(EventHandler)` | Set what happens when clicked |
| `setDisable(boolean)` | Enable/disable button |
| `setText(String text)` | Change button text |
| `setStyle(String css)` | Apply CSS styling |

---

## 4. RadioButton

**What it is:** A circular button that is either selected or deselected. RadioButtons are typically grouped so only ONE can be selected at a time.

```java
import javafx.application.Application;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.control.RadioButton;
import javafx.scene.control.ToggleGroup;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class RadioButtonDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create a ToggleGroup (only one RadioButton can be selected)
        ToggleGroup group = new ToggleGroup();
        
        // Create RadioButtons
        RadioButton option1 = new RadioButton("Option 1");
        RadioButton option2 = new RadioButton("Option 2");
        RadioButton option3 = new RadioButton("Option 3");
        
        // Add them to the same group
        option1.setToggleGroup(group);
        option2.setToggleGroup(group);
        option3.setToggleGroup(group);
        
        // Set default selection
        option1.setSelected(true);
        
        // Label to show selection
        Label resultLabel = new Label("Selected: Option 1");
        
        // Add event handler to each RadioButton
        option1.setOnAction(event -> resultLabel.setText("Selected: Option 1"));
        option2.setOnAction(event -> resultLabel.setText("Selected: Option 2"));
        option3.setOnAction(event -> resultLabel.setText("Selected: Option 3"));
        
        // Alternative: Use listener on ToggleGroup
        group.selectedToggleProperty().addListener((observable, oldToggle, newToggle) -> {
            if (newToggle != null) {
                RadioButton selected = (RadioButton) newToggle;
                System.out.println("Selected via listener: " + selected.getText());
            }
        });
        
        VBox vbox = new VBox(10);
        vbox.getChildren().addAll(option1, option2, option3, resultLabel);
        vbox.setAlignment(Pos.CENTER_LEFT);
        vbox.setStyle("-fx-padding: 20;");
        
        Scene scene = new Scene(vbox, 250, 200);
        stage.setTitle("RadioButton Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**Key points:**
- RadioButtons in the same `ToggleGroup` are mutually exclusive
- Without a ToggleGroup, each RadioButton acts independently
- Use `setSelected(true)` to set default selection

---

## 5. CheckBox

**What it is:** A square box that can be checked or unchecked. Multiple CheckBoxes can be selected independently (no grouping required).

```java
import javafx.application.Application;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.CheckBox;
import javafx.scene.control.Label;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class CheckBoxDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create CheckBoxes
        CheckBox readCheck = new CheckBox("Reading");
        CheckBox musicCheck = new CheckBox("Music");
        CheckBox sportsCheck = new CheckBox("Sports");
        CheckBox codingCheck = new CheckBox("Coding");
        
        // Initially check some
        readCheck.setSelected(true);
        codingCheck.setSelected(true);
        
        // Label to show selections
        Label resultLabel = new Label("Selected: Reading, Coding");
        
        // Add event handler to each CheckBox
        CheckBox[] checkBoxes = {readCheck, musicCheck, sportsCheck, codingCheck};
        
        for (CheckBox cb : checkBoxes) {
            cb.setOnAction(event -> {
                StringBuilder selected = new StringBuilder("Selected: ");
                for (CheckBox c : checkBoxes) {
                    if (c.isSelected()) {
                        selected.append(c.getText()).append(", ");
                    }
                }
                if (selected.length() > 10) {
                    resultLabel.setText(selected.substring(0, selected.length() - 2));
                } else {
                    resultLabel.setText("Selected: None");
                }
            });
        }
        
        VBox vbox = new VBox(10);
        vbox.getChildren().addAll(readCheck, musicCheck, sportsCheck, codingCheck, resultLabel);
        vbox.setAlignment(Pos.CENTER_LEFT);
        vbox.setStyle("-fx-padding: 20;");
        
        Scene scene = new Scene(vbox, 250, 250);
        stage.setTitle("CheckBox Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**Common methods:**
| Method | What it does |
|--------|--------------|
| `isSelected()` | Check if selected |
| `setSelected(boolean)` | Set selected state |
| `selectedProperty()` | Listen to selection changes |

---

## 6. Hyperlink

**What it is:** A clickable text link that looks like a web hyperlink. Used to navigate to URLs or trigger actions.

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Hyperlink;
import javafx.scene.control.Label;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;
import java.awt.Desktop;
import java.net.URI;

public class HyperlinkDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Simple hyperlink that opens website
        Hyperlink webLink = new Hyperlink("Visit Google");
        webLink.setOnAction(event -> {
            try {
                Desktop.getDesktop().browse(new URI("https://www.google.com"));
            } catch (Exception e) {
                System.out.println("Cannot open browser: " + e.getMessage());
            }
        });
        
        // Hyperlink that performs application action
        Hyperlink actionLink = new Hyperlink("Load Data");
        Label statusLabel = new Label("");
        
        actionLink.setOnAction(event -> {
            statusLabel.setText("Data loaded successfully!");
            System.out.println("Hyperlink clicked - loading data...");
        });
        
        // Hyperlink with custom styling (no underline until hover)
        Hyperlink styledLink = new Hyperlink("Styled Link");
        styledLink.setStyle("-fx-underline: false; -fx-text-fill: darkgreen;");
        
        VBox vbox = new VBox(15);
        vbox.getChildren().addAll(webLink, actionLink, statusLabel, styledLink);
        vbox.setStyle("-fx-padding: 20;");
        
        Scene scene = new Scene(vbox, 300, 200);
        stage.setTitle("Hyperlink Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**Characteristics:**
- By default, underlined only on hover
- Changes color when visited (like web links)
- Can be used for web navigation or application actions

---

## 7. Menu (MenuBar, Menu, MenuItem)

**What it is:** A drop-down menu system at the top of the window (File, Edit, View, etc.).

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.BorderPane;
import javafx.stage.Stage;

public class MenuDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        BorderPane root = new BorderPane();
        Label statusLabel = new Label("Ready");
        root.setBottom(statusLabel);
        
        // Create MenuBar
        MenuBar menuBar = new MenuBar();
        
        // ========== FILE MENU ==========
        Menu fileMenu = new Menu("File");
        
        // Menu items
        MenuItem newItem = new MenuItem("New");
        newItem.setOnAction(e -> statusLabel.setText("New file created"));
        
        MenuItem openItem = new MenuItem("Open");
        openItem.setOnAction(e -> statusLabel.setText("Open file dialog"));
        
        MenuItem saveItem = new MenuItem("Save");
        saveItem.setOnAction(e -> statusLabel.setText("File saved"));
        
        // Separator (line)
        SeparatorMenuItem separator = new SeparatorMenuItem();
        
        MenuItem exitItem = new MenuItem("Exit");
        exitItem.setOnAction(e -> stage.close());
        
        fileMenu.getItems().addAll(newItem, openItem, saveItem, separator, exitItem);
        
        // ========== EDIT MENU ==========
        Menu editMenu = new Menu("Edit");
        
        MenuItem cutItem = new MenuItem("Cut");
        cutItem.setOnAction(e -> statusLabel.setText("Cut"));
        cutItem.setDisable(true);  // Disabled initially
        
        MenuItem copyItem = new MenuItem("Copy");
        copyItem.setOnAction(e -> statusLabel.setText("Copy"));
        
        MenuItem pasteItem = new MenuItem("Paste");
        pasteItem.setOnAction(e -> statusLabel.setText("Paste"));
        
        editMenu.getItems().addAll(cutItem, copyItem, pasteItem);
        
        // ========== HELP MENU ==========
        Menu helpMenu = new Menu("Help");
        
        MenuItem aboutItem = new MenuItem("About");
        aboutItem.setOnAction(e -> {
            Alert alert = new Alert(Alert.AlertType.INFORMATION);
            alert.setTitle("About");
            alert.setHeaderText("My Application");
            alert.setContentText("Version 1.0\nCreated with JavaFX");
            alert.showAndWait();
        });
        
        helpMenu.getItems().add(aboutItem);
        
        // Add all menus to menu bar
        menuBar.getMenus().addAll(fileMenu, editMenu, helpMenu);
        
        root.setTop(menuBar);
        
        Scene scene = new Scene(root, 500, 400);
        stage.setTitle("Menu Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**Menu Components:**
| Component | Purpose |
|-----------|---------|
| `MenuBar` | Container for menus (top of window) |
| `Menu` | Drop-down menu (File, Edit, Help) |
| `MenuItem` | Clickable item in menu (New, Open, Save) |
| `SeparatorMenuItem` | Line between items |
| `CheckMenuItem` | Menu item with checkbox |
| `RadioMenuItem` | Menu item with radio button |

---

## 8. Tooltip

**What it is:** A small popup that appears when user hovers mouse over a control, providing helpful information.

```java
import javafx.application.Application;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class TooltipDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Simple tooltip
        Button button = new Button("Hover over me");
        Tooltip buttonTooltip = new Tooltip("This is a button that does something");
        button.setTooltip(buttonTooltip);
        
        // TextField with tooltip
        TextField textField = new TextField();
        textField.setPromptText("Enter email");
        Tooltip textTooltip = new Tooltip("Enter your email address\nExample: user@example.com");
        textField.setTooltip(textTooltip);
        
        // CheckBox with styled tooltip
        CheckBox checkBox = new CheckBox("Accept terms");
        Tooltip checkTooltip = new Tooltip("You must accept the terms to continue");
        checkTooltip.setStyle("-fx-background-color: lightyellow; -fx-text-fill: darkblue;");
        checkBox.setTooltip(checkTooltip);
        
        // Tooltip with image
        // ImageView icon = new ImageView(new Image("file:info.png"));
        // Tooltip imageTooltip = new Tooltip("Information", icon);
        // button.setTooltip(imageTooltip);
        
        VBox vbox = new VBox(20);
        vbox.getChildren().addAll(button, textField, checkBox);
        vbox.setAlignment(Pos.CENTER);
        vbox.setStyle("-fx-padding: 50;");
        
        Scene scene = new Scene(vbox, 400, 250);
        stage.setTitle("Tooltip Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**Tooltip properties:**
| Method | What it does |
|--------|--------------|
| `setTooltip(Tooltip)` | Attach tooltip to control |
| `setText(String)` | Set tooltip text |
| `setStyle(String)` | Style the tooltip |
| `setShowDelay(Duration)` | Delay before showing |

---

## 9. FileChooser

**What it is:** A system dialog that lets users select files or directories from their file system.

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.VBox;
import javafx.stage.FileChooser;
import javafx.stage.Stage;
import java.io.File;

public class FileChooserDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        Label resultLabel = new Label("No file selected");
        
        // Open file button
        Button openBtn = new Button("Open File");
        openBtn.setOnAction(e -> {
            FileChooser fileChooser = new FileChooser();
            fileChooser.setTitle("Select a File");
            
            // Set initial directory
            fileChooser.setInitialDirectory(new File(System.getProperty("user.home")));
            
            // Add file filters
            FileChooser.ExtensionFilter textFilter = 
                new FileChooser.ExtensionFilter("Text Files", "*.txt", "*.text");
            FileChooser.ExtensionFilter allFilter = 
                new FileChooser.ExtensionFilter("All Files", "*.*");
            fileChooser.getExtensionFilters().addAll(textFilter, allFilter);
            
            // Show open dialog
            File selectedFile = fileChooser.showOpenDialog(stage);
            
            if (selectedFile != null) {
                resultLabel.setText("Opened: " + selectedFile.getName());
                System.out.println("File path: " + selectedFile.getAbsolutePath());
            } else {
                resultLabel.setText("Open cancelled");
            }
        });
        
        // Save file button
        Button saveBtn = new Button("Save File");
        saveBtn.setOnAction(e -> {
            FileChooser fileChooser = new FileChooser();
            fileChooser.setTitle("Save File");
            
            // Set default filename
            fileChooser.setInitialFileName("untitled.txt");
            
            // Show save dialog
            File fileToSave = fileChooser.showSaveDialog(stage);
            
            if (fileToSave != null) {
                resultLabel.setText("Saved: " + fileToSave.getName());
                System.out.println("Save path: " + fileToSave.getAbsolutePath());
            } else {
                resultLabel.setText("Save cancelled");
            }
        });
        
        // Directory chooser button
        Button dirBtn = new Button("Choose Directory");
        dirBtn.setOnAction(e -> {
            FileChooser fileChooser = new FileChooser();
            fileChooser.setTitle("Select Directory");
            
            // Show directory chooser
            File selectedDir = fileChooser.showDialog(stage);
            
            if (selectedDir != null && selectedDir.isDirectory()) {
                resultLabel.setText("Selected: " + selectedDir.getName());
            }
        });
        
        VBox vbox = new VBox(15);
        vbox.getChildren().addAll(openBtn, saveBtn, dirBtn, resultLabel);
        vbox.setStyle("-fx-padding: 30;");
        
        Scene scene = new Scene(vbox, 400, 250);
        stage.setTitle("FileChooser Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

**FileChooser methods:**
| Method | Purpose |
|--------|---------|
| `showOpenDialog(Window)` | Show dialog to select file to open |
| `showSaveDialog(Window)` | Show dialog to select location to save |
| `setInitialDirectory(File)` | Set starting directory |
| `setInitialFileName(String)` | Set default filename (save dialog) |
| `getExtensionFilters()` | Add file type filters |
| `setSelectedExtensionFilter(ExtensionFilter)` | Set default filter |

---

## Complete Example: Registration Form with All Controls

```java
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.stage.FileChooser;
import javafx.stage.Stage;
import java.io.File;

public class RegistrationForm extends Application {
    
    @Override
    public void start(Stage stage) {
        // ========== CREATE UI CONTROLS ==========
        
        // Labels and TextFields
        Label nameLabel = new Label("Full Name:");
        TextField nameField = new TextField();
        nameField.setPromptText("Enter your full name");
        
        Label emailLabel = new Label("Email:");
        TextField emailField = new TextField();
        emailField.setPromptText("Enter your email");
        
        Label phoneLabel = new Label("Phone:");
        TextField phoneField = new TextField();
        phoneField.setPromptText("Enter phone number");
        
        // Password Field
        Label passwordLabel = new Label("Password:");
        PasswordField passwordField = new PasswordField();
        passwordField.setPromptText("Enter password");
        
        // RadioButtons for Gender
        Label genderLabel = new Label("Gender:");
        ToggleGroup genderGroup = new ToggleGroup();
        RadioButton maleRadio = new RadioButton("Male");
        RadioButton femaleRadio = new RadioButton("Female");
        RadioButton otherRadio = new RadioButton("Other");
        maleRadio.setToggleGroup(genderGroup);
        femaleRadio.setToggleGroup(genderGroup);
        otherRadio.setToggleGroup(genderGroup);
        HBox genderBox = new HBox(15, maleRadio, femaleRadio, otherRadio);
        
        // CheckBoxes for Hobbies
        Label hobbiesLabel = new Label("Hobbies:");
        CheckBox readCheck = new CheckBox("Reading");
        CheckBox musicCheck = new CheckBox("Music");
        CheckBox sportsCheck = new CheckBox("Sports");
        CheckBox travelCheck = new CheckBox("Travel");
        VBox hobbiesBox = new VBox(8, readCheck, musicCheck, sportsCheck, travelCheck);
        
        // Hyperlink for Terms
        Hyperlink termsLink = new Hyperlink("View Terms and Conditions");
        termsLink.setTooltip(new Tooltip("Click to view terms"));
        
        // FileChooser for Resume Upload
        Button uploadBtn = new Button("Upload Resume");
        Label uploadLabel = new Label("No file selected");
        Tooltip uploadTooltip = new Tooltip("Upload your resume (PDF, DOC)");
        uploadBtn.setTooltip(uploadTooltip);
        
        uploadBtn.setOnAction(e -> {
            FileChooser fileChooser = new FileChooser();
            fileChooser.setTitle("Select Resume");
            fileChooser.getExtensionFilters().addAll(
                new FileChooser.ExtensionFilter("PDF Files", "*.pdf"),
                new FileChooser.ExtensionFilter("Word Files", "*.doc", "*.docx"),
                new FileChooser.ExtensionFilter("All Files", "*.*")
            );
            File file = fileChooser.showOpenDialog(stage);
            if (file != null) {
                uploadLabel.setText(file.getName());
            }
        });
        
        // Buttons
        Button submitBtn = new Button("Submit");
        submitBtn.setStyle("-fx-background-color: lightgreen; -fx-font-size: 14px;");
        
        Button resetBtn = new Button("Reset");
        resetBtn.setStyle("-fx-background-color: lightcoral; -fx-font-size: 14px;");
        
        // ========== LAYOUT ==========
        GridPane grid = new GridPane();
        grid.setHgap(15);
        grid.setVgap(12);
        grid.setPadding(new Insets(20));
        
        // Add controls to grid
        grid.add(nameLabel, 0, 0);
        grid.add(nameField, 1, 0);
        
        grid.add(emailLabel, 0, 1);
        grid.add(emailField, 1, 1);
        
        grid.add(phoneLabel, 0, 2);
        grid.add(phoneField, 1, 2);
        
        grid.add(passwordLabel, 0, 3);
        grid.add(passwordField, 1, 3);
        
        grid.add(genderLabel, 0, 4);
        grid.add(genderBox, 1, 4);
        
        grid.add(hobbiesLabel, 0, 5);
        grid.add(hobbiesBox, 1, 5);
        
        grid.add(termsLink, 1, 6);
        
        grid.add(uploadBtn, 0, 7);
        grid.add(uploadLabel, 1, 7);
        
        // Button box
        HBox buttonBox = new HBox(20, submitBtn, resetBtn);
        buttonBox.setAlignment(Pos.CENTER);
        grid.add(buttonBox, 0, 8, 2, 1);
        
        // ========== EVENT HANDLERS ==========
        
        // Tooltip for email field
        Tooltip emailTooltip = new Tooltip("Enter a valid email address\nExample: name@domain.com");
        emailField.setTooltip(emailTooltip);
        
        // Submit button action
        submitBtn.setOnAction(e -> {
            StringBuilder info = new StringBuilder();
            info.append("Name: ").append(nameField.getText()).append("\n");
            info.append("Email: ").append(emailField.getText()).append("\n");
            info.append("Phone: ").append(phoneField.getText()).append("\n");
            
            // Get selected gender
            RadioButton selectedGender = (RadioButton) genderGroup.getSelectedToggle();
            info.append("Gender: ").append(selectedGender != null ? selectedGender.getText() : "Not selected").append("\n");
            
            // Get selected hobbies
            info.append("Hobbies: ");
            StringBuilder hobbies = new StringBuilder();
            if (readCheck.isSelected()) hobbies.append("Reading ");
            if (musicCheck.isSelected()) hobbies.append("Music ");
            if (sportsCheck.isSelected()) hobbies.append("Sports ");
            if (travelCheck.isSelected()) hobbies.append("Travel ");
            info.append(hobbies.length() > 0 ? hobbies : "None").append("\n");
            
            info.append("Resume: ").append(uploadLabel.getText()).append("\n");
            
            Alert alert = new Alert(Alert.AlertType.INFORMATION);
            alert.setTitle("Registration Information");
            alert.setHeaderText("Submitted Data");
            alert.setContentText(info.toString());
            alert.showAndWait();
        });
        
        // Reset button action
        resetBtn.setOnAction(e -> {
            nameField.clear();
            emailField.clear();
            phoneField.clear();
            passwordField.clear();
            genderGroup.selectToggle(null);
            readCheck.setSelected(false);
            musicCheck.setSelected(false);
            sportsCheck.setSelected(false);
            travelCheck.setSelected(false);
            uploadLabel.setText("No file selected");
        });
        
        // Terms hyperlink action
        termsLink.setOnAction(e -> {
            Alert alert = new Alert(Alert.AlertType.INFORMATION);
            alert.setTitle("Terms and Conditions");
            alert.setHeaderText("Terms of Use");
            alert.setContentText("This is a demo registration form.\n\n" +
                                 "1. All data is for demonstration only\n" +
                                 "2. No data is stored permanently\n" +
                                 "3. This is for learning JavaFX\n");
            alert.showAndWait();
        });
        
        Scene scene = new Scene(grid, 550, 550);
        stage.setTitle("Registration Form - JavaFX Controls Demo");
        stage.setScene(scene);
        stage.show();
    }
}
```

---

## Quick Reference Table

| Control | Purpose | Key Event |
|---------|---------|-----------|
| `Label` | Display text | None |
| `TextField` | Single-line text input | `setOnAction` (Enter key) |
| `Button` | Clickable action | `setOnAction` |
| `RadioButton` | Single selection from group | `setOnAction` |
| `CheckBox` | Multiple independent selections | `setOnAction` |
| `Hyperlink` | Clickable link | `setOnAction` |
| `MenuBar/Menu/MenuItem` | Drop-down menus | `setOnAction` |
| `Tooltip` | Hover help text | Hover (automatic) |
| `FileChooser` | File/directory selection | Dialog result |

---

## The Golden Rule

> **JavaFX UI Controls are the building blocks of your application. Labels display text, TextFields get input, Buttons trigger actions, RadioButtons/CheckBoxes capture choices, Menus organize commands, Tooltips guide users, and FileChoosers handle file operations. Combine them with Layouts to create professional desktop applications.**

**Memory trick:**
```
Label = "Look at this text"
TextField = "Type something here"
Button = "Do something now"
RadioButton = "Pick ONE option"
CheckBox = "Pick ANY options"
Hyperlink = "Click to navigate"
Menu = "Organized commands"
Tooltip = "Help when hovering"
FileChooser = "Select a file"
```