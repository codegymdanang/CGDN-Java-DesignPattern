# Factory Method Design Pattern 
### Factory Method dùng làm gì ?
+ Factory Method cho phép chúng ta tạo ra một đối tượng mà chúng ta không cần quan tâm nó được tạo ra như thế nào
### Khi nào nên sử dụng Factory method
+ Khi ta muốn tạo ra đối tượng lúc chương trình đang chay (run time) mà ta chưa biết nó sẽ trả về đối tượng gì
+ Khi các đối tượng được tạo ra có chung đặc điểm của lớp cha
+ Che dấu đối tượng được tạo ra . Client chỉ dùng nhưng không quan tâm các đối tượng con sẽ tạo ra như thế nào

### Factory Method UML

![FactoryMethod](https://user-images.githubusercontent.com/37821007/63338794-bc543e80-c36d-11e9-9bfb-6d27bc46112a.gif)

+ Trong ví dụ sau  chúng ta sẽ sử dụng Factory Method createButton để ra các dialog(Hộp thoại) trên hộp thoại đó sẽ có các button(nút bấm) khác nhau dự vào cái máy đang chạy ứng dụng này.
+ Nếu máy Windows chạy chương trình này thì nó sẽ tạo ra hộp thoại và có nút theo định dạng của máy Windows. 
+ Nếu máy chạy chương trình này là Mac hay Ubuntu thì chúng ta sẽ tạo ra dialog có nút bấm  tương ứng theo định dạng nút Mac hay Ubuntu
+ Ví dụ máy của mình đang là máy Mac thì khi chạy chương trình nó sẽ sinh ra Dialog (hội thoại) có button (nút bấm) theo định dạng Mac. Ví dụ máy khác đang sử dụng là Windows thì khi chạy chương trình nó sẽ sinh ra Dialog (hội thoại) có button (nút bấm) theo định dạng Windows 

### Factory Method tạo ra Dialog (hộp thoại) với các button (nút bấm) khác nhau
![factorymethod-dialog](https://user-images.githubusercontent.com/37821007/63355928-26320f80-c391-11e9-906c-577b8f9c86ef.png)

+ Theo thiết kế ở trên thì HTML Button và Windows Button chính là 2 Concreat Class. Là 2 class sản phẩm được tạo ra từ abstract method createButton của HTML Dialog và Windows Dialog

+ Abstract Dialog chính là Creator chứa method abstract và 1 phương thức để gọi Abstract

+ HTML Dialog và Windows Dialog chính là 2 Concreat Creator . 2 class này sẽ kế thừa phương thức abstract class của lớp Abstract Dialog. 2 Class HTML Dialog và Windows Dialog kế thừa phương thức abstract createButton. Nhưng mỗi lớp sẽ cài đặt phương thức tạo ra button khác nhau. Kết quả của phương thức abstract sẽ sinh ra 1 đối tượng tương ứng. Ví dụ HTML Dialog thì sẽ tạo ra đối tượng HTML Button , còn Windows Dialog sẽ tạo ra Windows Button .

+ Demo Application sẽ sử dụng Dialog để tuỳ vào hệ điều hành mà cho ra các sản phẩm dialog tương ứng (Win, Mac, Ubuntu)


