## 1. Tổng quan về CNN
CNN là một trong những mô hình để nhận dạng và phân loại hình ảnh. Trong đó, xác định đối tượng và nhận dạng khuôn mặt là 1 trong số những lĩnh vực mà CNN được sử dụng rộng rãi.
CNN phân loại hình ảnh bằng cách lấy 1 hình ảnh đầu vào, xử lý và phân loại nó theo các hạng mục nhất định (Ví dụ: Chó, Mèo, Hổ, ...)
Về kỹ thuật, mô hình CNN để training và kiểm tra, mỗi hình ảnh đầu vào sẽ chuyển nó qua 1 loạt các lớp tích chập với các bộ lọc (Kernels), tổng hợp lại các lớp được kết nối đầy đủ (Full Connected) và áp dụng hàm Softmax để phân loại đối tượng có giá trị xác suất giữa 0 và 1. Hình dưới đây là toàn bộ luồng CNN để xử lý hình ảnh đầu vào và phân loại các đối tượng dựa trên giá trị
## 2. Các kiểu tầng trong CNN
### a) Tầng tích chập (CONV)
Tích chập là lớp đầu tiên để trích xuất các tính năng từ hình ảnh đầu vào. Tích chập duy trì mối quan hệ giữa các pixel bằng cách tìm hiểu các tính năng hình ảnh bằng cách sử dụng các ô vuông nhỏ của dữ liệu đầu vào. Nó là một phép toán có hai đầu vào như ma trận hình ảnh và 1 bộ lọc hoặc hạt nhân.
### b) Pooling (POOL)
Tầng pooling (POOL) là một phép downsampling, thường được sử dụng sau - tầng tích chập, giúp tăng tính bất biến không gian.
Các dạng pooling đặc biệt:
Max pooling: giá trị lớn nhất được lấy ra.
Average pooling: giá trị trung bình được lấy ra.
### c) Fully Connection (FC)
Tầng kết nối đầy đủ (FC) nhận đầu vào là các dữ liệu đã được làm phẳng, mà mỗi đầu vào đó được kết nối đến tất cả neuron.
Thường được tìm thấy ở cuối mạng và được dùng để tối ưu hóa mục tiêu của mạng ví dụ như độ chính xác của lớp.
## 3. Các siêu tham số của bộ lọc
### a) Các chiều của một bộ lọc
Một bộ lọc kích thước F×F áp dụng lên đầu vào chứa C kênh (channels) thì có kích thước tổng kể là F×F×C thực hiện phép tích chập trên đầu vào kích thước I×I×C và cho ra một feature map (hay còn gọi là activation map) có kích thước  O×O×1.
### b) Stride
Đối với phép tích chập hoặc phép pooling, độ trượt S ký hiệu số pixel mà cửa sổ sẽ di chuyển sau mỗi lần thực hiện phép tính. 
![stride](https://user-images.githubusercontent.com/105013825/176097460-fbeef1a8-a189-406f-bf29-7bf8d9310125.png)

### c) Zero-Padding
Zero-padding là tên gọi của quá trình thêm P số không vào các biên của đầu vào. Giá trị này có thể được lựa chọn thủ công hoặc một cách tự động bằng một trong ba những phương pháp mô tả bên dưới:
> ![padding](https://user-images.githubusercontent.com/105013825/176098157-3ea6c586-e03a-4ac6-90b2-e7637258ccb1.png)

##4. Điều chỉnh siêu tham số.
### a) Tính tương thích của tham số trong tầng tích chập
Bằng cách ký hiệu I là độ dài kích thước đầu vào, F là độ dài của bộ lọc, P là số lượng zero padding, S là độ trượt, ta có thể tính được độ dài O của feature map theo một chiều bằng công thức:
> ![Thamso](https://user-images.githubusercontent.com/105013825/176098180-3c62b467-a476-47b0-9b9f-0163fb736464.png)

### b) Hiểu về độ phức tạp của mô hình
Để đánh giá độ phức tạp của một mô hình, cách hữu hiệu là xác định số tham số mà mô hình đó sẽ có. Trong một tầng của mạng neural tích chập, nó sẽ được tính toán như sau:
> ![Phuctap](https://user-images.githubusercontent.com/105013825/176098199-5eea7b7c-d77c-4ff4-9d52-ba9b5c4817e5.png)

### c) Trường thụ cảm
Trường thụ cảm tại tầng k là vùng được ký hiệu Rk ×Rk của đầu vào mà những pixel của activation map thứ k có thể "nhìn thấy". Bằng cách gọi Fj là kích thước bộ lọc của tầng j và Si là giá trị độ trượt của tầng i và để thuận tiện, ta mặc định S0 = 1, trường thụ cảm của tầng k được tính toán bằng công thức:
> ![image](https://user-images.githubusercontent.com/105013825/176097956-644e0f74-6682-4431-b626-80ced8aa718b.png)
##5. Các hàm kích hoạt thường gặp.
### a) Rectified Linear Unit
Rectified Linear Unit: Tầng rectified linear unit (ReLU) là một hàm kích hoạt g được sử dụng trên tất cả các thành phần. Mục đích của nó là tăng tính phi tuyến tính cho mạng. Với đầu ra là: ƒ (x) = max (0, x).
> ![image](https://user-images.githubusercontent.com/105013825/176098028-de954098-4c48-48c5-a3ed-4d41e1e6d37e.png)
### b) Signmod
Sigmoid Function (Hàm Sigmoid) còn được gọi là đường cong Sigmoid. Đây là một hàm toán học có đặc trưng là đường cong hình chữ S. Nó thể hiện cho sự biến đổi các giá trị giữa phạm vi 0 và 1. Nó là một trong những hàm kích hoạt (activation function) phi tuyến tính được sử dụng rộng rãi nhất.
### c) Softmax
Bước softmax có thể được coi là một hàm logistic tổng quát lấy đầu vào là một vector chứa các giá trị x ∈ Rn và cho ra là một vector gồm các xác suất p ∈ Rn thông qua một hàm softmax ở cuối kiến trúc. Nó được định nghĩa như sau:
> ![image](https://user-images.githubusercontent.com/105013825/176098094-2ae71188-9344-4354-af96-71d13713f4f4.png)








