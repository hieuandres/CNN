# CNN
# 1. Tổng quan về CNN
CNN là một trong những mô hình để nhận dạng và phân loại hình ảnh. Trong đó, xác định đối tượng và nhận dạng khuôn mặt là 1 trong số những lĩnh vực mà CNN được sử dụng rộng rãi.
CNN phân loại hình ảnh bằng cách lấy 1 hình ảnh đầu vào, xử lý và phân loại nó theo các hạng mục nhất định (Ví dụ: Chó, Mèo, Hổ, ...)
Về kỹ thuật, mô hình CNN để training và kiểm tra, mỗi hình ảnh đầu vào sẽ chuyển nó qua 1 loạt các lớp tích chập với các bộ lọc (Kernels), tổng hợp lại các lớp được kết nối đầy đủ (Full Connected) và áp dụng hàm Softmax để phân loại đối tượng có giá trị xác suất giữa 0 và 1. Hình dưới đây là toàn bộ luồng CNN để xử lý hình ảnh đầu vào và phân loại các đối tượng dựa trên giá trị
# 2. Các kiểu tầng trong CNN
Tầng tích chập (CONV)
Tích chập là lớp đầu tiên để trích xuất các tính năng từ hình ảnh đầu vào. Tích chập duy trì mối quan hệ giữa các pixel bằng cách tìm hiểu các tính năng hình ảnh bằng cách sử dụng các ô vuông nhỏ của dữ liệu đầu vào. Nó là một phép toán có hai đầu vào như ma trận hình ảnh và 1 bộ lọc hoặc hạt nhân.
Pooling (POOL)
Tầng pooling (POOL) là một phép downsampling, thường được sử dụng sau - tầng tích chập, giúp tăng tính bất biến không gian.
Các dạng pooling đặc biệt:
Max pooling: giá trị lớn nhất được lấy ra.
Average pooling: giá trị trung bình được lấy ra.
c) Fully Connection (FC)
	Tầng kết nối đầy đủ (FC) nhận đầu vào là các dữ liệu đã được làm phẳng, mà mỗi đầu vào đó được kết nối đến tất cả neuron.
Thường được tìm thấy ở cuối mạng và được dùng để tối ưu hóa mục tiêu của mạng ví dụ như độ chính xác của lớp.
# 3. Các siêu tham số của bộ lọc
Các chiều của một bộ lọc
Một bộ lọc kích thước F×F áp dụng lên đầu vào chứa C kênh (channels) thì có kích thước tổng kể là F×F×C thực hiện phép tích chập trên đầu vào kích thước I×I×C và cho ra một feature map (hay còn gọi là activation map) có kích thước  O×O×1.
Stride
Đối với phép tích chập hoặc phép pooling, độ trượt S ký hiệu số pixel mà cửa sổ sẽ di chuyển sau mỗi lần thực hiện phép tính. 
![stride](https://user-images.githubusercontent.com/105013825/176097460-fbeef1a8-a189-406f-bf29-7bf8d9310125.png)
