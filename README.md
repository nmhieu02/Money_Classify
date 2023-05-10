# Money_Classify

Thực hiện nghiên cứu việc xác định giá trị mặt tiền Việt Nam dựa trên ảnh chụp một cách tự động hóa bằng công nghệ phần mềm và khoa học máy tính. Sử dụng thư viện OpenCV, thư viện Sklearn, thư viện Keras, Visual Studio Code,...
## Tổng quan

![tongquan](https://github.com/nmhieu02/Money_Classify/assets/133008099/b297ce55-f0c0-47fb-a392-63a8fb4fe439)

## Bố cục chung

**• setup.txt**: chứa các thư viện cần phải cài đặt.
**• make_data.py**: dùng để đọc liên tục từ camera và save lại vào các thư mục tương ứng ảnh các tờ tiền. Sau khi chạy thành công các class, chúng em sẽ có thư mục data với các thư mục con
**• train.py**: Xử lý dữ liệu ảnh, thiết kế mạng CNN Classify dùng để train, sử dụng augmentation cho dữ liệu và train model CNN Classify
**• test.py**: để kiểm thử model.

## Các bước thực nghiệm
### Tạo data
Sử dụng _**make_data.py**_ để xây dựng bộ data. Trong thư mục data có chứa các thư mục con với tên là nhãn tờ tiền cho từng mệnh giá tiền tương ứng.

![datap](https://github.com/nmhieu02/Money_Classify/assets/133008099/a86f3aab-c0ca-4289-b956-b88a9826e53e)

Data được tạo thông qua webcam. Thực chất là đọc liên tục từ camera và lưu lại vào các thư mục tương ứng ảnh các tờ tiền. Ví dụ trong bài này chúng em làm sample với 7 nhãn là 0, 10000, 20000 và 50000,... Sau khi chạy thành công các class, chúng em sẽ có thư mục data với các thư mục con như hình sau:

![data_500k](https://github.com/nmhieu02/Money_Classify/assets/133008099/d3bf77de-b08f-4bd9-97d0-5e0ce07611c7)

### Xử lý dữ liệu ảnh
Sau khi tạo xong data, bây giờ chúng ta sẽ tiến hành xử lý dữ liệu đó và ghi vào file dữ liệu _pix.data_. Trong quá trình chúng ta train model, thử nghiệm model thì sẽ phải chạy chương trình nhiều lần để debug, sửa lỗi. . . Như vậy mỗi lần chạy sẽ phải đi lần lượt hết các file và thư mục, việc đó khá lâu và làm ảnh hưởng đến thời gian tiến trình nên chúng ta sẽ đọc 1 lần mà thôi.

###  Thiết kế mạng CNN Classify và train model
Thiết kế và train được thực hiện trong file _**train.py**_. Trong quá trình training, chương trình đưa ra liên tục kết quả của từng epoch, bao gồm biến loss, accuracy, val_loss, val_accuracy.
Huấn luyện với các mẫu sau khi đã qua tăng cường dữ liệu:

![train](https://github.com/nmhieu02/Money_Classify/assets/133008099/cc8e5640-dedd-45f3-988a-6474793868d7)

Sau cùng, khi đã chạy hết epoch, chương trình sẽ trả về 2 biều đổ, thể hiện sự thay đổi của biến loss và biến value qua các epoch:

![plot1](https://github.com/nmhieu02/Money_Classify/assets/133008099/7e16bd8c-a428-4d0e-8ab5-c470df2f4ebc)

### Kiểm tra kết quả
Cuối cùng để kiểm thử model chúng ta chạy file test.py file này sẽ đọc ảnh từ camera sau đó thực hiện resize ảnh, normalize ảnh, chuyển thành tensor và đưa vào model để predict và cuối cùng là lấy kết quả đầu ra và hiển thị trên màn hình.
![ketqua](https://github.com/nmhieu02/Money_Classify/assets/133008099/70f48d44-ec3d-4b99-97a3-c1b05ccbdc41)
Chú ý: Ở đây chỉ xét các ảnh được nhận dạng có xác suất > 0.8 để nhận được kết quả tốt nhất.
