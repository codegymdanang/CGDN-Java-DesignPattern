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
