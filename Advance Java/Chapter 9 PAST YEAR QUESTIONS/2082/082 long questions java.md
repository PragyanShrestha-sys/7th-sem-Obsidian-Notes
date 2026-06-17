![[Pasted image 20260617132647.png]]

[[Handling Events]]
[[Socket Programming Using TCP and UDP]]

----

![[Pasted image 20260617133032.png]]

```java    
import javafx.application.*;
import javafx.scene.*;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.*;

public class Choice extends Application {
    public void start(Stage s) {
        ChoiceBox<String> c = new ChoiceBox<>();
        c.getItems().setAll("Red","Green","Blue");
        Label l = new Label();
        c.setOnAction(e -> l.setText(c.getValue()));
        l.setText(c.getValue());
        s.setScene(new Scene(new VBox(c,l), 200, 120));
        s.show();
    }
    public static void main(String[] a) { launch(a); }
}
```

[[CORBA Implementation (Common Object Request Broker Architecture)]]

CORBA IMPLEMENTATION MA YO 3 TA MOST IMPORTANT

ORB orb = ORB.init(args, null);
orb.connect(impl);  // ← Simple! No POA needed
orb.run();

---

![[Pasted image 20260617133037.png]]
[[Statement, ResultSet & Query Execution]]