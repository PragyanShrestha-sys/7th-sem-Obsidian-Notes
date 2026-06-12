**Layout Panes** are containers that automatically arrange child nodes (UI components) according to specific rules.

```
Parent (Layout Pane)
    │
    ├── Child 1 (Button)
    ├── Child 2 (Label)
    ├── Child 3 (TextField)
    └── Child 4 (ImageView)
```

---

### 1. FlowPane

**What it is:** Arranges nodes in a horizontal flow, wrapping to the next row when needed. Similar to FlowLayout in Swing.

```
FlowPane (Horizontal flow):
┌─────────────────────────────────────────┐
│ [Button1] [Button2] [Button3]           │
│ [Button4] [Button5]                     │
└─────────────────────────────────────────┘

When window resizes (smaller):
┌─────────────────────────┐
│ [Button1] [Button2]     │
│ [Button3] [Button4]     │
│ [Button5]               │
└─────────────────────────┘
```

**Key Properties:**

| Property | What it does |
|----------|--------------|
| `orientation` | Horizontal or vertical |
| `hgap` | Horizontal gap between nodes |
| `vgap` | Vertical gap between rows |
| `alignment` | How children are aligned |

**Code Example:**

```java
import javafx.application.Application;
import javafx.geometry.Orientation;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.FlowPane;
import javafx.stage.Stage;

public class FlowPaneDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create FlowPane with horizontal orientation
        FlowPane flowPane = new FlowPane();
        
        // Set gaps between components
        flowPane.setHgap(10);   // Horizontal gap
        flowPane.setVgap(10);   // Vertical gap
        
        // Set alignment (centered)
        flowPane.setAlignment(javafx.geometry.Pos.CENTER);
        
        // Add buttons (they will wrap automatically)
        for (int i = 1; i <= 10; i++) {
            flowPane.getChildren().add(new Button("Button " + i));
        }
        
        // Create scene and show
        Scene scene = new Scene(flowPane, 400, 300);
        stage.setTitle("FlowPane Demo");
        stage.setScene(scene);
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

**Use when:**
- Toolbars
- Button collections
- Dynamic component counts
- Responsive layouts that wrap

---

### 2. BorderPane

**What it is:** Divides the container into five regions: Top, Bottom, Left, Right, and Center. Similar to BorderLayout in Swing.

```
BorderPane Layout:
┌─────────────────────────────────────────┐
│                 TOP                     │
├───────────────┬─────────────────────────┤
│               │                         │
│     LEFT      │        CENTER           │
│               │                         │
├───────────────┴─────────────────────────┤
│                BOTTOM                    │
└─────────────────────────────────────────┘
```

**Key Properties:**

| Region | Purpose | Typical Content |
|--------|---------|-----------------|
| `top` | Top section | Menu bar, toolbar |
| `bottom` | Bottom section | Status bar |
| `left` | Left section | Navigation panel |
| `right` | Right section | Sidebar, properties |
| `center` | Center (main area) | Main content |

**Code Example:**

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.layout.BorderPane;
import javafx.stage.Stage;

public class BorderPaneDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create BorderPane
        BorderPane borderPane = new BorderPane();
        
        // Set different regions
        // TOP - Menu bar or toolbar
        Label topLabel = new Label("This is TOP section - Menu Bar");
        topLabel.setStyle("-fx-background-color: lightblue; -fx-padding: 10;");
        borderPane.setTop(topLabel);
        
        // BOTTOM - Status bar
        Label bottomLabel = new Label("This is BOTTOM section - Status Bar");
        bottomLabel.setStyle("-fx-background-color: lightgray; -fx-padding: 10;");
        borderPane.setBottom(bottomLabel);
        
        // LEFT - Navigation panel
        Label leftLabel = new Label("LEFT - Navigation");
        leftLabel.setStyle("-fx-background-color: lightgreen; -fx-padding: 10;");
        borderPane.setLeft(leftLabel);
        
        // RIGHT - Sidebar
        Label rightLabel = new Label("RIGHT - Properties");
        rightLabel.setStyle("-fx-background-color: lightyellow; -fx-padding: 10;");
        borderPane.setRight(rightLabel);
        
        // CENTER - Main content
        Label centerLabel = new Label("CENTER - Main Content Area");
        centerLabel.setStyle("-fx-background-color: white; -fx-padding: 50;");
        borderPane.setCenter(centerLabel);
        
        // Create scene
        Scene scene = new Scene(borderPane, 600, 400);
        stage.setTitle("BorderPane Demo");
        stage.setScene(scene);
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

**Use when:**
- Main application window
- Classic IDE layout (menu on top, status on bottom, navigation on left, content in center)
- Any application needing clear region separation

---

### 3. HBox (Horizontal Box)

**What it is:** Arranges nodes in a single horizontal row. All children are placed side by side.

```
HBox:
┌─────────────────────────────────────────┐
│ [Button1] [Button2] [Button3] [Button4] │
└─────────────────────────────────────────┘
```

**Key Properties:**

| Property | What it does |
|----------|--------------|
| `spacing` | Space between children |
| `alignment` | How children align vertically |
| `fillHeight` | Whether children fill height |

**Code Example:**

```java
import javafx.application.Application;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.HBox;
import javafx.stage.Stage;

public class HBoxDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create HBox
        HBox hbox = new HBox();
        
        // Set spacing between buttons (10 pixels)
        hbox.setSpacing(10);
        
        // Set alignment (center buttons vertically)
        hbox.setAlignment(Pos.CENTER);
        
        // Add buttons
        Button btn1 = new Button("Save");
        Button btn2 = new Button("Load");
        Button btn3 = new Button("Delete");
        Button btn4 = new Button("Cancel");
        
        hbox.getChildren().addAll(btn1, btn2, btn3, btn4);
        
        // Set padding around the HBox
        hbox.setStyle("-fx-padding: 20; -fx-background-color: lightgray;");
        
        Scene scene = new Scene(hbox, 500, 100);
        stage.setTitle("HBox Demo");
        stage.setScene(scene);
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

**Use when:**
- Button bars (OK, Cancel, Apply)
- Toolbars (horizontal)
- Form row with label and field side by side
- Any horizontal arrangement

---

### 4. VBox (Vertical Box)

**What it is:** Arranges nodes in a single vertical column. All children are stacked top to bottom.

```
VBox:
┌─────────────────────────────────────────┐
│               [Button1]                 │
│               [Button2]                 │
│               [Button3]                 │
│               [Button4]                 │
└─────────────────────────────────────────┘
```

**Key Properties:**

| Property | What it does |
|----------|--------------|
| `spacing` | Space between children |
| `alignment` | How children align horizontally |
| `fillWidth` | Whether children fill width |

**Code Example:**

```java
import javafx.application.Application;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class VBoxDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create VBox
        VBox vbox = new VBox();
        
        // Set spacing between elements (15 pixels)
        vbox.setSpacing(15);
        
        // Set alignment (center buttons horizontally)
        vbox.setAlignment(Pos.CENTER);
        
        // Create form elements
        Label nameLabel = new Label("Name:");
        TextField nameField = new TextField();
        nameField.setMaxWidth(200);
        
        Label emailLabel = new Label("Email:");
        TextField emailField = new TextField();
        emailField.setMaxWidth(200);
        
        Button submitBtn = new Button("Submit");
        Button cancelBtn = new Button("Cancel");
        
        // Add all elements to VBox
        vbox.getChildren().addAll(nameLabel, nameField, 
                                   emailLabel, emailField, 
                                   submitBtn, cancelBtn);
        
        // Set padding
        vbox.setStyle("-fx-padding: 30; -fx-background-color: lightblue;");
        
        Scene scene = new Scene(vbox, 300, 350);
        stage.setTitle("VBox Demo - Registration Form");
        stage.setScene(scene);
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

**Use when:**
- Form layouts (labels above fields)
- Vertical menu or navigation
- List of items stacked
- Dialog with buttons at bottom

---

### 5. GridPane

**What it is:** Arranges nodes in a flexible grid of rows and columns. Similar to GridLayout but more powerful (different row/column sizes, spanning).

```
GridPane (3x3):
┌─────────┬─────────┬─────────┐
│ (0,0)   │ (0,1)   │ (0,2)   │
├─────────┼─────────┼─────────┤
│ (1,0)   │ (1,1)   │ (1,2)   │
├─────────┼─────────┼─────────┤
│ (2,0)   │ (2,1)   │ (2,2)   │
└─────────┴─────────┴─────────┘

With column span:
┌───────────────────┬─────────┐
│   SPANS 2 COLUMNS │ (0,2)   │
├─────────┬─────────┴─────────┤
│ (1,0)   │   SPANS 2 ROWS    │
├─────────┤                    │
│ (2,0)   │                    │
└─────────┴────────────────────┘
```

**Key Properties:**

| Property | What it does |
|----------|--------------|
| `hgap` | Horizontal gap between columns |
| `vgap` | Vertical gap between rows |
| `alignment` | Overall alignment |
| `gridLinesVisible` | Show grid lines (debugging) |

**Static Methods for Constraints:**

| Method | Purpose |
|--------|---------|
| `setColumnIndex(node, col)` | Set column position |
| `setRowIndex(node, row)` | Set row position |
| `setColumnSpan(node, span)` | Span multiple columns |
| `setRowSpan(node, span)` | Span multiple rows |
| `setHalignment(node, value)` | Horizontal alignment |
| `setValignment(node, value)` | Vertical alignment |

**Code Example:**

```java
import javafx.application.Application;
import javafx.geometry.HPos;
import javafx.geometry.Insets;
import javafx.geometry.VPos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

public class GridPaneDemo extends Application {
    
    @Override
    public void start(Stage stage) {
        // Create GridPane
        GridPane grid = new GridPane();
        
        // Set gaps
        grid.setHgap(10);  // Horizontal gap
        grid.setVgap(10);  // Vertical gap
        grid.setPadding(new Insets(20));  // Padding around grid
        
        // Add components with their positions
        
        // Row 0: First Name
        Label firstNameLabel = new Label("First Name:");
        grid.add(firstNameLabel, 0, 0);  // column 0, row 0
        
        TextField firstNameField = new TextField();
        grid.add(firstNameField, 1, 0);  // column 1, row 0
        firstNameField.setPrefWidth(200);
        
        // Row 1: Last Name
        Label lastNameLabel = new Label("Last Name:");
        grid.add(lastNameLabel, 0, 1);  // column 0, row 1
        
        TextField lastNameField = new TextField();
        grid.add(lastNameField, 1, 1);  // column 1, row 1
        
        // Row 2: Email
        Label emailLabel = new Label("Email:");
        grid.add(emailLabel, 0, 2);  // column 0, row 2
        
        TextField emailField = new TextField();
        grid.add(emailField, 1, 2);  // column 1, row 2
        
        // Row 3: Phone (spanning 2 columns)
        Label phoneLabel = new Label("Phone Number:");
        grid.add(phoneLabel, 0, 3);
        
        TextField phoneField = new TextField();
        grid.add(phoneField, 1, 3);
        
        // Row 4: Buttons (spanning 2 columns)
        Button saveBtn = new Button("Save");
        Button cancelBtn = new Button("Cancel");
        
        // Create HBox for buttons
        javafx.scene.layout.HBox buttonBox = new javafx.scene.layout.HBox(10);
        buttonBox.getChildren().addAll(saveBtn, cancelBtn);
        
        grid.add(buttonBox, 0, 4, 2, 1);  // span 2 columns, 1 row
        
        // Set column constraints (make column 1 expand)
        javafx.scene.layout.ColumnConstraints col1 = new javafx.scene.layout.ColumnConstraints();
        col1.setPercentWidth(30);  // 30% of width
        
        javafx.scene.layout.ColumnConstraints col2 = new javafx.scene.layout.ColumnConstraints();
        col2.setPercentWidth(70);  // 70% of width
        
        grid.getColumnConstraints().addAll(col1, col2);
        
        Scene scene = new Scene(grid, 500, 300);
        stage.setTitle("GridPane Demo - Registration Form");
        stage.setScene(scene);
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

**Use when:**
- Data entry forms (labels in one column, fields in another)
- Calculator layout
- Dashboard with multiple panels
- Any structured grid layout

---

## Layout Panes Comparison Table

| Layout | Orientation | Wrap? | Span? | Best for |
|--------|-------------|-------|-------|----------|
| **FlowPane** | Horizontal (default) or vertical | ✅ Yes | ❌ No | Toolbars, button collections |
| **BorderPane** | 5 regions (top/bottom/left/right/center) | ❌ No | ❌ No | Main application window |
| **HBox** | Single horizontal row | ❌ No | ❌ No | Button bars, horizontal groups |
| **VBox** | Single vertical column | ❌ No | ❌ No | Forms, vertical menus |
| **GridPane** | Rows and columns grid | ❌ No | ✅ Yes | Complex forms, structured layouts |

---

## Nested Layouts (Combining Panes)

**Most real applications combine multiple layout panes:**

```java
// Example: Complex layout using nested panes
BorderPane mainLayout = new BorderPane();

// Top: HBox for toolbar
HBox toolbar = new HBox(10);
toolbar.getChildren().addAll(
    new Button("New"), 
    new Button("Open"), 
    new Button("Save")
);
mainLayout.setTop(toolbar);

// Left: VBox for navigation
VBox navMenu = new VBox(10);
navMenu.getChildren().addAll(
    new Button("Home"),
    new Button("Products"),
    new Button("Settings")
);
mainLayout.setLeft(navMenu);

// Center: GridPane for content
GridPane content = new GridPane();
// ... add content to grid
mainLayout.setCenter(content);

// Bottom: HBox for status
HBox statusBar = new HBox(10);
statusBar.getChildren().add(new Label("Ready"));
mainLayout.setBottom(statusBar);
```
