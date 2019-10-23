### Strategy Pattern
The Strategy pattern is known as a behavioural pattern - it's used to manage algorithms, relationships and responsibilities between objects. The definition of Strategy provided in the original Gang of Four book on DesignPatterns states: 

### Khi nào dùng Strategy

Where Would I Use This Pattern?
The Strategy pattern is to be used where you want to choose the algorithm to use at runtime. A good use of the Strategy pattern would be saving files in different formats, running various sorting algorithms, or file compression.

The Strategy pattern provides a way to define a family of algorithms, encapsulate each one as an object, and make them interchangeable.  

### Let's use the example of a file compression tool - where we create either zip or rar files. First we'll need a strategy

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
