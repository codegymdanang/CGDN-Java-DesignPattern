### Builder Pattern
### Khi nào nên dùng Builder
#### Object có nhiều constructor
+ Sẽ có những trường hợp ta lấy 1 Class có rất nhiều constructor khởi tạo đối tượng. Ví dụ như lớp Pizza Sau đây
```
Pizza(int size) { ... }        
Pizza(int size, boolean cheese) { ... }    
Pizza(int size, boolean cheese, boolean pepperoni) { ... }    
Pizza(int size, boolean cheese, boolean pepperoni, boolean bacon) { ... }
```
+ 1 class có nhiều constructor với có nhiều parameter trong constructor sẽ gây khó khăn cho người lập trình để nhớ và sử dụng cái nào cho đúng. Cái này thì gọi là Telescoping Constructor

+ Có một cách để tránh Telescope là minh tạo tạo một object từ một constructor mặc định , sau đó dùng các hàm setter để set giá trị như ví dụ sau:
```
Pizza pizza = new Pizza(12);
pizza.setCheese(true);
pizza.setPepperoni(true);
pizza.setBacon(true);
```
+ Vấn đề trên có vấn đề ở chổ là Object được tạo ra qua quá nhiều bước setter 
+ Để giải quyết được vấn đề thì Builder Pattern sẽ là cách tốt nhất 

```
public class Pizza {
  private int size;
  private boolean cheese;
  private boolean pepperoni;
  private boolean bacon;

  public static class Builder {
    //required
    private final int size;

    //optional
    private boolean cheese = false;
    private boolean pepperoni = false;
    private boolean bacon = false;

    public Builder(int size) {
      this.size = size;
    }

    public Builder cheese(boolean value) {
      cheese = value;
      return this;
    }

    public Builder pepperoni(boolean value) {
      pepperoni = value;
      return this;
    }

    public Builder bacon(boolean value) {
      bacon = value;
      return this;
    }

    public Pizza build() {
      return new Pizza(this);
    }
  }

  private Pizza(Builder builder) {
    size = builder.size;
    cheese = builder.cheese;
    pepperoni = builder.pepperoni;
    bacon = builder.bacon;
  }
}
```

+ Bây giờ chúng ta dùng builder để tránh việc setter quá nhiều 
```
Pizza pizza = new Pizza.Builder(12)
                       .cheese(true)
                       .pepperoni(true)
                       .bacon(true)
                       .build();
```
+ Đoạn code ở trên rất dể viết va dể hiểu.
#### Khi chúng ta muốn tạo object được cấu thành từ nhiều phần khác nhau. Khác với abstract factory chúng ta muốn build 1 bộ sản phẩm giống như xe Toyota gồm có lốp Toyota, phanh Toyota. ect Toyota. Thì Builder được sử dụng khi ta muốn build 1 sản phẩm từ nhiều bộ phận khác nhau như xe Toyota, phay Huynhdai , lốp Ferrary

### Builder UML
![builder](https://user-images.githubusercontent.com/37821007/63422351-64ccd600-c434-11e9-96a8-5145e9698d53.png)


### Builder 
