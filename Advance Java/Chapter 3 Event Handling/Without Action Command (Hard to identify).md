```java
JButton saveButton = new JButton("Save");
JButton loadButton = new JButton("Load");
JButton deleteButton = new JButton("Delete");

// ONE listener for all buttons (problem: how to tell which was clicked?)
ActionListener listener = new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        // Need to check source or command
        if (e.getSource() == saveButton) {
            save();
        } else if (e.getSource() == loadButton) {
            load();
        } else if (e.getSource() == deleteButton) {
            delete();
        }
    }
};
```
