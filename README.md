# Bài 8: Lọc giải pháp khắc phục lỗi cổng mạng trên StackOverflow

## Phần 1: Phân tích sai lầm và thẩm định giải pháp

1\. Ba dấu hiệu nhận diện Câu trả lời A là giải pháp đáng tin cậy hơn Câu trả lời B

- Tích xanh (✓): Câu trả lời A được người đặt câu hỏi xác nhận là giải pháp phù hợp.
- Upvotes: Câu A có 1.240 lượt bình chọn, trong khi câu B có -2 lượt. Điều này cho thấy cộng đồng đánh giá câu A tốt hơn.
- Thời gian và bình luận: Câu A được đăng năm 2024 và có bình luận xác nhận chạy tốt trên Windows 11. Câu B đã đăng từ năm 2012 và có cảnh báo gây lỗi mạng.

2\. Vì sao thời gian đăng bài (Recency) quan trọng?

- Công nghệ và hệ điều hành thường xuyên được cập nhật nên cách sửa lỗi cũ có thể không còn phù hợp.
- Windows 11 có những thay đổi về quản lý mạng so với các phiên bản Windows trước.
- Áp dụng lệnh cũ như `net stop winnat` có thể làm gián đoạn kết nối mạng, ảnh hưởng đến Hyper-V và card mạng LAN.

Vì vậy, cần ưu tiên những hướng dẫn mới, phù hợp với phiên bản hệ điều hành đang sử dụng.

## Phần 2: Ứng dụng GitHub Issues và quy trình khắc phục sự cố

3\. Quy trình 30 giây đọc lướt trên StackOverflow

1. Nhìn vào tiêu đề để xác định bài viết có đúng lỗi `EADDRINUSE` hay không.
2. Kiểm tra Tags như `node.js`, `windows`, `port` để xác định đúng công nghệ.
3. Cuộn xuống phần Answers, tìm câu trả lời có tích xanh hoặc Upvotes cao.
4. Bỏ qua phần giải thích dài, tập trung đọc các lệnh trong Code Block.
5. Kiểm tra bình luận bên dưới để xem giải pháp có hoạt động trên Windows 11 không.

Lệnh sửa lỗi trong Câu trả lời A:

Bước 1: Kiểm tra tiến trình đang chiếm cổng 8080.

```
netstat -ano | findstr :8080
```

Bước 2: Xác định PID (mã tiến trình) đang sử dụng cổng 8080.

Bước 3: Nếu xác định đúng tiến trình không cần thiết, mới thực hiện lệnh giải phóng cổng:

```
taskkill /PID <PID> /F
```

Lưu ý: Không nên tắt tiến trình hệ thống hoặc tiến trình quan trọng khi chưa xác định rõ. Lệnh trên sẽ buộc dừng tiến trình được chỉ định.

4\. Nên tìm GitHub Issues ở trạng thái nào?

Theo em, nên ưu tiên tìm kiếm Issues ở trạng thái OPEN khi thư viện `ocpp-gateway` vừa phát sinh lỗi mới.

- OPEN: Lỗi vẫn đang được thảo luận, có thể tìm được cách khắc phục tạm thời.
- CLOSED: Lỗi đã được đóng, có thể tham khảo cách sửa lỗi chính thức.

Workaround là gì?

Workaround là giải pháp tạm thời giúp phần mềm tiếp tục hoạt động khi lỗi chưa được sửa triệt để.

Cách nhận diện Workaround uy tín:

- Được nhiều người xác nhận đã thử thành công.
- Có bình luận hoặc Reactions tích cực.
- Có hướng dẫn cụ thể, dễ hiểu và phù hợp với phiên bản phần mềm đang sử dụng.
- Không yêu cầu chạy lệnh nguy hiểm hoặc thay đổi hệ thống khi chưa rõ tác dụng.

## Kết luận

Theo em, khi tìm cách sửa lỗi cần ưu tiên giải pháp có tích xanh, nhiều Upvotes, thời gian cập nhật gần đây và được kiểm chứng trên môi trường tương tự. Không nên làm theo các lệnh cũ hoặc chưa hiểu rõ tác dụng vì có thể khiến máy tính gặp thêm lỗi nghiêm trọng.
