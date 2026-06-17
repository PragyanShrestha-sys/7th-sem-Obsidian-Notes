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
            flowPane.add(new Button("Button " + i));
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
│                BOTTOM                   │
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
        //Scene scene = new Scene(root, width, height);
        Scene scene = new Scene(borderPane, 600, 400);
        stage.setTitle("BorderPane Demo");
        stage.setScene(scene);
        stage.show();//**Without `stage.show()`**, everything exists in memory (the house is built, painted, and furnished), but **the lights are off and the doors are locked** – you can't see it on your monitor!
        
        
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

note: 

|Component|Job|What it does|
|---|---|---|
|**`Scene`**|**Adding stuff**|Holds all your UI components (buttons, labels, layouts)|
|**`Stage`**|**Modifying stuff**|Controls the window itself (title, size, position, behavior|

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
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

public class GridPaneShortened extends Application {
    
    @Override
    public void start(Stage stage) {
        GridPane grid = new GridPane();
        
        // Essential GridPane settings
        grid.setHgap(10);      // Horizontal gap between cells
        grid.setVgap(10);      // Vertical gap between cells
        
        // Adding components: grid.add(node, column, row)
        grid.add(new Label("Name:"), 0, 0);      // col 0, row 0
        grid.add(new TextField(), 1, 0);         // col 1, row 0
        
        grid.add(new Label("Email:"), 0, 1);     // col 0, row 1
        grid.add(new TextField(), 1, 1);         // col 1, row 1
        
        // Span: grid.add(node, col, row, colspan, rowspan)
        grid.add(new Label("Full width:"), 0, 2, 2, 1);  // spans 2 columns
        
        Scene scene = new Scene(grid, 400, 150);
        stage.setScene(scene);
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

Code example (with only spanning):

```java
	grid.add(Node node, int columnIndex, int rowIndex, int colspan, int rowspan);
```

```java 
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

public class GridPaneMultiSpans extends Application {
    
    @Override
    public void start(Stage stage) {
        GridPane grid = new GridPane();
        grid.setHgap(10);
        grid.setVgap(10);
        
        // Row 0: Full width header (spans 3 columns)
        grid.add(new Label("User Profile"), 0, 0, 3, 1);
        
        // Row 1: Labels and fields (3 columns)
        grid.add(new Label("First Name:"), 0, 1);
        grid.add(new TextField(), 1, 1);
        grid.add(new Label("Last Name:"), 2, 1);
        
        // Row 2: Full width email (spans 3 columns)
        grid.add(new Label("Email:"), 0, 2);
        grid.add(new TextField(), 1, 2, 2, 1);  // spans 2 columns
        
        // Row 3: Tall button (spans 2 rows)
        Button tallButton = new Button("TALL\nBUTTON");
        tallButton.setPrefHeight(60);
        grid.add(tallButton, 0, 3, 1, 2);  // spans 2 rows
        
        // Row 3: Address (spans 2 columns)
        grid.add(new Label("Address:"), 1, 3);
        grid.add(new TextField(), 2, 3);
        
        // Row 4: City and State (2 columns)
        grid.add(new Label("City:"), 1, 4);
        grid.add(new TextField(), 2, 4);
        
        // Row 5: Save button (spans 3 columns)
        Button save = new Button("Save Profile");
        grid.add(save, 0, 5, 3, 1);
        
        Scene scene = new Scene(grid, 500, 300);
        stage.setTitle("Multi Spans Example");
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



