Here's your **ultra-short** JavaFX controls demo - just the essentials:

---

## 1. Label
```java
Label label = new Label("Name:");
```

---

## 2. TextField
```java
TextField tf = new TextField();
tf.getText();  // Get value
```

---

## 3. Button
```java
Button btn = new Button("Click");
btn.setOnAction(e -> System.out.println("Clicked"));
```

---

## 4. RadioButton
```java
ToggleGroup group = new ToggleGroup();
RadioButton r1 = new RadioButton("Yes");
r1.setToggleGroup(group);
```

---

## 5. CheckBox
```java
CheckBox cb = new CheckBox("Accept");
cb.isSelected();  // Get state
```

---

## 6. Hyperlink
```java
Hyperlink link = new Hyperlink("Click here");
link.setOnAction(e -> System.out.println("Link clicked"));
```

---

## 7. Menu
```java
MenuBar bar = new MenuBar();
Menu menu = new Menu("File");
MenuItem item = new MenuItem("Exit");
item.setOnAction(e -> System.exit(0));
menu.getItems().add(item);
bar.getMenus().add(menu);
```

---

## 8. Tooltip
```java
btn.setTooltip(new Tooltip("Help text"));
```

---

## 9. FileChooser
```java
File file = new FileChooser().showOpenDialog(stage);
```

---

## One Complete Minimal Example
```java
public void start(Stage stage) {
    TextField tf = new TextField();
    Button btn = new Button("Submit");
    Label result = new Label();
    
    btn.setOnAction(e -> result.setText("Hello " + tf.getText()));
    
    VBox root = new VBox(10, tf, btn, result);
    stage.setScene(new Scene(root, 300, 200));
    stage.show();
}
```

---

**That's it!** Just 3-4 lines per control - nothing extra.