# Abstract Factory

### Abstract Factory Là gì ?

### Khi nào nên dùng Abstract Factory
+ Khi chúng ta muốn tạo một họ sản phẩm (FAMILY PRODUCT) liên quan đến . Ví dụ như mình muốn tạo một đối tượng là Xe hơi Toyota. Thì các thành phần cấu thành xe hơi Toyota phải từ chính Toyota mà ra . Ví dụ Xe hơi Toyota thì Tay laí Toyota , lốp xe Toyota. Khung xe được sản xuất tại Toyota. Nói tóm lại các thành phần cấu tạo nên chiếc xe phải từ Toyota mà ra cả 
### Abstract Factory UML
![Abstract Factory UML](https://user-images.githubusercontent.com/37821007/63338154-7b0f5f00-c36c-11e9-9809-56ebd2a54635.png)

### Abstract Factory Button và Checkbox
![abstractfactory](https://user-images.githubusercontent.com/37821007/63360952-7614d480-c399-11e9-8f15-dde4dae0b3ba.png)

++ Trong ví dụ  trên về xây dựng một ứng dụng Paint(vẽ) gồm có các phần như tạo button (nút) và tạo checkbox. Ứng với hệ điều hành Windows thì nó sẽ tạo ra bộ sản phẩm nút và check box của Windows. Nếu là hệ điều hành Mac thì nó sẽ tạo ra một bộ sản phẩm checkbox và nút bấm cho Mac. Như vậy phụ thuộc vào hệ điều hành mà mình đang dùng thì mình sẽ tạo các các thành phần tương ứng cho hệ điều hành đó. Không có trường hợp hệ điều hành Windows mà mình có thể tạo ra nút bấm Windows và Checkbox của Mac được.

+ GUI Factory trong thiết kế tương ứng với Abstract Facetory . Gui Factory gồm các method để tạo ra một sản phẩm . Mỗi method là tạo ra một phần của sản phẩm như button hay checkbox
+ MacOSFactory chính là ConcreatFactory1 : gồm các phương thức abstract để tạo ra button và checkbox tương ứng với Mac
+ WinOSFactory chính là ConcreatFactory 2 : gồm các phương thức abstract để tạo ra button và checkbox tương ứng với 
+ Interface Button : Chính là AbstractProductA . Gồm phương thức vẽ để mô tả cho hành động vẽ button  là vẽ như thế nào  với mỗi hệ điều hành Windows hay Mac
+ Interface Checkbox : Chính là AbstractProductB . Gồm phương thức vẽ để mô tả cho hành động vẽ checkbox  là vẽ như thế nào với mỗi hệ điều hành Windows hay Mac 
+ Windows Button : là ProductA2 . Đây là lớp định nghĩa Windows button là gì
+ Mac Button      : là ProductA1 . Đây là lớp định nghĩa Mac button là gì 
+ Windows Checkbox : là ProductB2 . Đây là lớp định nghĩa Windows checkbox  là gì
+ Mac Checkbox     : là Product B1 . Đây là lớp định nghĩa Mac checkbox  là gì
+ Application : Sử dụng Gui Factory và 2 lớp Interface Button và Interface Checkbox để tạo ra họ sản phẩm . Nếu windows thì button và checkbox Windows và ngược lại

```
public class Demo {

    /**
     * Application picks the factory type and creates it in run time (usually at
     * initialization stage), depending on the configuration or environment
     * variables.
     */
    private static Application configureApplication() {
        Application app;
        GUIFactory factory;
        String osName = System.getProperty("os.name").toLowerCase();
        if (osName.contains("mac")) {
            factory = new MacOSFactory();
            app = new Application(factory);
        } else {
            factory = new WindowsFactory();
            app = new Application(factory);
        }
        return app;
    }

    public static void main(String[] args) {
        Application app = configureApplication();
        app.paint();
    }
}
```
```
/**
 * Factory users don't care which concrete factory they use since they work with
 * factories and products through abstract interfaces.
 */
public class Application {
    private Button button;
    private Checkbox checkbox;

    public Application(GUIFactory factory) {
        button = factory.createButton();
        checkbox = factory.createCheckbox();
    }

    public void paint() {
        button.paint();
        checkbox.paint();
    }
}
```
```
/**
 * Abstract factory knows about all (abstract) product types.
 */
public interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}
```

```
/**
 * Each concrete factory extends basic factory and responsible for creating
 * products of a single variety.
 */
public class MacOSFactory implements GUIFactory {

    @Override
    public Button createButton() {
        return new MacOSButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacOSCheckbox();
    }
}
```

```
/**
 * Each concrete factory extends basic factory and responsible for creating
 * products of a single variety.
 */
public class WindowsFactory implements GUIFactory {

    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}
```

```
/**
 * Checkboxes is the second product family. It has the same variants as buttons.
 */
public interface Checkbox {
    void paint();
}

```

```
/**
 * All products families have the same varieties (MacOS/Windows).
 *
 * This is a variant of a checkbox.
 */
public class MacOSCheckbox implements Checkbox {

    @Override
    public void paint() {
        System.out.println("You have created MacOSCheckbox.");
    }
}

```

```
/**
 * All products families have the same varieties (MacOS/Windows).
 *
 * This is another variant of a checkbox.
 */
public class WindowsCheckbox implements Checkbox {

    @Override
    public void paint() {
        System.out.println("You have created WindowsCheckbox.");
    }
}
```

```
/**
 * Abstract Factory assumes that you have several families of products,
 * structured into separate class hierarchies (Button/Checkbox). All products of
 * the same family have the common interface.
 *
 * This is the common interface for buttons family.
 */
public interface Button {
    void paint();
}
```

```
/**
 * All products families have the same varieties (MacOS/Windows).
 *
 * This is a MacOS variant of a button.
 */
public class MacOSButton implements Button {

    @Override
    public void paint() {
        System.out.println("You have created MacOSButton.");
    }
}
```

```
/**
 * All products families have the same varieties (MacOS/Windows).
 *
 * This is another variant of a button.
 */
public class WindowsButton implements Button {

    @Override
    public void paint() {
        System.out.println("You have created WindowsButton.");
    }
}

```

```
public class Demo {

    /**
     * Application picks the factory type and creates it in run time (usually at
     * initialization stage), depending on the configuration or environment
     * variables.
     */
    private static Application configureApplication() {
        Application app;
        GUIFactory factory;
        String osName = System.getProperty("os.name").toLowerCase();
        if (osName.contains("mac")) {
            factory = new MacOSFactory();
            app = new Application(factory);
        } else {
            factory = new WindowsFactory();
            app = new Application(factory);
        }
        return app;
    }

    public static void main(String[] args) {
        Application app = configureApplication();
        app.paint();
    }
}
```
