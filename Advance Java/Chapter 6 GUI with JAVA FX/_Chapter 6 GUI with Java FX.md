## [[Introduction and differences Between Java FX and Swing]]

![[Pasted image 20260607104037.png]]
![[Pasted image 20260607104045.png]]

---
## Part 2: [[JavaFX Layout Panes (extends application)]]
**Memory trick:**
```
FlowPane = "Flows and wraps" (like text)
BorderPane = "Borders the screen" (north, south, east, west, center)
HBox = "Horizontal Box" (left to right)
VBox = "Vertical Box" (top to bottom)
GridPane = "Grid of cells" (rows and columns)
```

---

## The Golden Rule

> **JavaFX is the modern replacement for Swing. Use FlowPane for wrapping layouts, BorderPane for main window structure, HBox/VBox for simple horizontal/vertical arrangements, and GridPane for complex form layouts. Always combine multiple panes to create professional UIs.**

---
## [[Java FX UI Controls]]

---
# JavaFX UI Controls - Short Demonstration

note: Comparision to Swing (equivalent herne ho bhane)
- **`JFrame` ↔ `Stage`** (The top-level OS window)
- **`JPanel` ↔ `Scene`** (The container that holds all your UI components)

|Component|Job|What it does|
|---|---|---|
|**`Scene`**|**Adding stuff**|Holds all your UI components (buttons, labels, layouts)|
|**`Stage`**|**Modifying stuff**|Controls the window itself (title, size, position, behavior|
