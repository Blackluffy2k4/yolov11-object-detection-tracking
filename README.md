# Hướng dẫn thực hành sử dụng yolov trên raspberry pi 4
# 1.Chuẩn bị tài nguyên
Chuẩn bị mạch Raspberry pi 4 của bạn, cài OS mới nhất, trường hợp tôi sử dụng là 64 bit Debian Bookworm
Cập nhật bằng cách dùng lệnh

sudo apt update && sudo apt upgrade -y

tiếp theo hãy tạo 1 môi trường ảo, venv này có tác dụng làm cho các cài đặt bên trong venv không bị xung đột với hệ thống, những gì bạn đã tải về trong venv không thể sử dụng ở ngoài venv. Vì vậy tạo venv để hoạt động độc lập là điều cần thiết:
Tạo 1 thư mục, ví dụ yolo:
mkdir yolo
cd yolo

Tạo 1 môi trường ảo tại đây: 
python3 -m venv --system-site-packages venv

Chạy môi trường ảo: 
source venv/bin/activate
Khi chạy lệnh trên, sẽ có 1 chữ ở đầu command, ví dụ (venv) 

Tắt terminal và mở lại, chạy lại môi trường ảo trên, tiến hành cài yolo:
pip install ultralytics ncnn
Lệnh này sẽ tải yolo với thư viện NCNN phổ biến và hiệu quả nhất trên Pi, tham khảo thêm tại https://docs.ultralytics.com/vi/integrations/ncnn/
Quá trình tải diễn ra khoảng 20-30p, nếu có lỗi, hãy thực hiện lại lệnh cài

Sau khi tải thành công, tiến hành setup model, chọn model nano vì nhẹ và nhanh nhất cho Pi:
yolo detect predict model=yolo11n.pt
Tải xong bạn sẽ có 1 file .pt trong thư mục bạn đang đứng.
Nếu bạn có model custom riêng, hãy đưa nó vào trong thư mục của bạn, ví dụ candy.pt

Tiếp theo tiến hành format 
yolo export model=yolo11n.pt format=ncnn
Sau khi chạy xong ta sẽ có 1 folder mới tên yolo11n_ncnn_model

Sau đó bạn hãy chạy thử file python test của tôi, có tên main.py trên repo này
python main.py --model=yolo11n_ncnn_model --source=picamera0 --resolution=1280x720
Lệnh này sẽ lấy nguồn từ camera của bạn 

