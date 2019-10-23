### Strategy Pattern
Chúng ta dùng Strategy Pattern để quản lý thuật toán , các mối quan hệ giữa các object trong ứng dụng

### Khi nào dùng Strategy
Chúng ta sử dung Strategy khi chúng ta muốn chọn một thuật toán cho một đối tượng cụ thể lúc runtime (chương trình đang chạy). Ví dụ như thuật toán thanh toán cho khi mua hàng online trên mạng. Chúng ta có thể thanh toán bằng thẻ visa hay master. Thì khi chương trình mình dang chạy nếu người dùng chọn visa thì mình sẽ dùng thuật toán tính tiền của visa để thanh toán. Như vậy ta wrap các thuật toán , các business thành một đối tượng và sử dụng nó


### UML

![general-strategy-pattern](https://user-images.githubusercontent.com/37821007/67373760-5b81f600-f5aa-11e9-9f75-4c0efed9450d.png)

### Vi dụ sau dây ta làm cho thuật toán nén file. Người dùng có thể nén bằng zip hoặc bằng rar 

```
//Strategy Interface
public interface CompressionStrategy {
  public void compressFiles(ArrayList<File> files);
}
```

```
public class ZipCompressionStrategy implements CompressionStrategy {
  public void compressFiles(ArrayList<File> files) {
    //using ZIP approach
  }
}
```

```
public class RarCompressionStrategy implements CompressionStrategy {
  public void compressFiles(ArrayList<File> files) {
    //using RAR approach
  }
}
```

```
public class CompressionContext {
  private CompressionStrategy strategy;
  //this can be set at runtime by the application preferences
  public void setCompressionStrategy(CompressionStrategy strategy) {
    this.strategy = strategy;
  }
  
  //use the strategy
  public void createArchive(ArrayList<File> files) {
    strategy.compressFiles(files);
  }
}
```
```
public class Client {
  public static void main(String[] args) {
    CompressionContext ctx = new CompressionContext();
    //we could assume context is already set by preferences
    ctx.setCompressionStrategy(new ZipCompressionStrategy());
    //get a list of files...
    ctx.createArchive(fileList);
  }
}
```
