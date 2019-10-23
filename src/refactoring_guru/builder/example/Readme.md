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
```
/**
 * Builder interface defines all possible ways to configure a product.
 */
public interface Builder {
    void setType(Type type);
    void setSeats(int seats);
    void setEngine(Engine engine);
    void setTransmission(Transmission transmission);
    void setTripComputer(TripComputer tripComputer);
    void setGPSNavigator(GPSNavigator gpsNavigator);
}

```

```
/**
 * Concrete builders implement steps defined in the common interface.
 */
public class CarBuilder implements Builder {
    private Type type;
    private int seats;
    private Engine engine;
    private Transmission transmission;
    private TripComputer tripComputer;
    private GPSNavigator gpsNavigator;

    @Override
    public void setType(Type type) {
        this.type = type;
    }

    @Override
    public void setSeats(int seats) {
        this.seats = seats;
    }

    @Override
    public void setEngine(Engine engine) {
        this.engine = engine;
    }

    @Override
    public void setTransmission(Transmission transmission) {
        this.transmission = transmission;
    }

    @Override
    public void setTripComputer(TripComputer tripComputer) {
        this.tripComputer = tripComputer;
    }

    @Override
    public void setGPSNavigator(GPSNavigator gpsNavigator) {
        this.gpsNavigator = gpsNavigator;
    }

    public Car getResult() {
        return new Car(type, seats, engine, transmission, tripComputer, gpsNavigator);
    }
}

```

```
/**
 * Unlike other creational patterns, Builder can construct unrelated products,
 * which don't have the common interface.
 *
 * In this case we build a user manual for a car, using the same steps as we
 * built a car. This allows to produce manuals for specific car models,
 * configured with different features.
 */
public class CarManualBuilder implements Builder{
    private Type type;
    private int seats;
    private Engine engine;
    private Transmission transmission;
    private TripComputer tripComputer;
    private GPSNavigator gpsNavigator;

    @Override
    public void setType(Type type) {
        this.type = type;
    }

    @Override
    public void setSeats(int seats) {
        this.seats = seats;
    }

    @Override
    public void setEngine(Engine engine) {
        this.engine = engine;
    }

    @Override
    public void setTransmission(Transmission transmission) {
        this.transmission = transmission;
    }

    @Override
    public void setTripComputer(TripComputer tripComputer) {
        this.tripComputer = tripComputer;
    }

    @Override
    public void setGPSNavigator(GPSNavigator gpsNavigator) {
        this.gpsNavigator = gpsNavigator;
    }

    public Manual getResult() {
        return new Manual(type, seats, engine, transmission, tripComputer, gpsNavigator);
    }
}

```

```
/**
 * Director defines the order of building steps. It works with a builder object
 * through common Builder interface. Therefore it may not know what product is
 * being built.
 */
public class Director {

    public void constructSportsCar(Builder builder) {
        builder.setType(Type.SPORTS_CAR);
        builder.setSeats(2);
        builder.setEngine(new Engine(3.0, 0));
        builder.setTransmission(Transmission.SEMI_AUTOMATIC);
        builder.setTripComputer(new TripComputer());
        builder.setGPSNavigator(new GPSNavigator());
    }

    public void constructCityCar(Builder builder) {
        builder.setType(Type.CITY_CAR);
        builder.setSeats(2);
        builder.setEngine(new Engine(1.2, 0));
        builder.setTransmission(Transmission.AUTOMATIC);
        builder.setTripComputer(new TripComputer());
        builder.setGPSNavigator(new GPSNavigator());
    }

    public void constructSUV(Builder builder) {
        builder.setType(Type.SUV);
        builder.setSeats(4);
        builder.setEngine(new Engine(2.5, 0));
        builder.setTransmission(Transmission.MANUAL);
        builder.setGPSNavigator(new GPSNavigator());
    }
}
```
```
/**
 * Demo class. Everything comes together here.
 */
public class Demo {

    public static void main(String[] args) {
        Director director = new Director();

        // Director gets the concrete builder object from the client
        // (application code). That's because application knows better which
        // builder to use to get a specific product.
        CarBuilder builder = new CarBuilder();
        director.constructSportsCar(builder);

        // The final product is often retrieved from a builder object, since
        // Director is not aware and not dependent on concrete builders and
        // products.
        Car car = builder.getResult();
        System.out.println("Car built:\n" + car.getType());


        CarManualBuilder manualBuilder = new CarManualBuilder();

        // Director may know several building recipes.
        director.constructSportsCar(manualBuilder);
        Manual carManual = manualBuilder.getResult();
        System.out.println("\nCar manual built:\n" + carManual.print());
    }

}
```
