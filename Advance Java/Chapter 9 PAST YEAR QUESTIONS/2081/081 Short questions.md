 n 
How does JavaFX hyperlink control format text that functions as button? Illustrate with an example.

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Hyperlink;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class HyperlinkDemo extends Application {
    public void start(Stage stage) {
        Hyperlink link = new Hyperlink("Click me!");
        link.setOnAction(e -> link.setText("Clicked! ✅"));
        stage.setScene(new Scene(new VBox(link), 300, 200));
        stage.show();
    }
    public static void main(String[] args) { launch(args); }
}
```

for redirect

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Hyperlink;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class HyperlinkDemo extends Application {
    public void start(Stage stage) {
        Hyperlink link = new Hyperlink("Visit Google");
        
        // Redirect to URL
        link.setOnAction(e -> {
            getHostServices().showDocument("https://www.google.com");
        });
        
        stage.setScene(new Scene(new VBox(link), 300, 200));
        stage.show();
    }
    public static void main(String[] args) { launch(args); }
}
```

---

## DESCRIBE 2 TYPES OF EVENTS 
ANS > [[Handling Events]]

---
## [[WRITE IDL FILE AND GEENRATION THE STUB AND SKELETOP CODE FOR CORBA IMPLEMENTATION]]

---
## Create a form taking in input 
ans : [[Servlet and lifecycle (get request ko example nicha )]] and [[Processing Fourms in Servlet (Post request in servlet ko example yeai lekhda huncha)]]

---
## What do you mean by SQL escape? Describe about scrollble(kasto ways ma navigate garna milcha) and updateable result sets (update garne ki read only garne).
ans: [[ResultSet Types & Concurrency]]

---
## Explain the life cycle of Servlets
: [[Servlet and lifecycle (get request ko example nicha )]]

---
## How to insert pop up request? Distinguish between get and post request

|Feature|GET|POST|
|---|---|---|
|**Data location**|URL (query string)|Request body|
|**Visibility**|Visible in address bar|Hidden (not visible)|
|**Bookmarkable**|✅ Yes|❌ No|
|**Cached**|✅ Yes|❌ No|
|**Data size limit**|~2KB (URL limit)|No limit|
|**Security**|❌ Less secure|✅ More secure|
|**Idempotent**|✅ Yes (safe)|❌ No (changes data)|
|**Use for**|Retrieving data|Submitting data|

---
