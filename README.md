# Cherry Project
This project is building a mini ecomerce app to practicing Event souring and CQRS pattern
Trong mini project này cần có đầy đủ các thành phần và các bước.

Trong project này tôi sẽ cố gắng note lại chi tiết các bước để có thể hoàn thành một sản phẩm. Các note, vấn đề thắc mắc cũng sẽ được ghi lại để review sau này.

Project được chạy theo mô hình agile

1. Có mô tả về project, các tính năng.
2. Có phân tích thiết kế các bước quan trọng
3. Code project

# Note
- Lúc đầu khi lên một ý tưởng làm 1 sản phẩm xong thì việc tiếp theo là thu thập được các thông tin về requerement

- Thu thập thông tin ứng với từng nhóm người dùng, việc này hết sức quan trọng nó hỗ trợ làm rõ hơn các công việc sẽ làm làm gì. Có thể không liệt kê được toàn bộ requirement nhưng cần liệt kê đủ rộng để team phát triển, manager, khách hàng đều hiểu theo một hướng về sản phẩm sẽ làm => bắt buộc việc này cần làm trước tiên

- Việc phát triển sản phẩm trải qua rất nhiều công đoạn và công việc. Việc hiểu sai ý khách hàng là không tránh khỏi hoặc việc khách hàng thay đổi reqirement là khó tránh. Do đó toàn bộ team phát triển, BA, manager, customer cần làm việc closely vs nhau. Đặt biệt là những sản phẩm chưa rõ ràng thì nên chạy theo mô hình agile. Việc còn thay đổi là sản phẩm còn đang phát triển. AE dev, manager cần hiểu được điều đó. Điều quan trọng là khi có thay đổi lớn thì manager, khách hàng, ba, team phát triển cần ngồi trao đổi chia sẻ với nhau. Điều mà sau khoảng 3 năm làm việc tôi nhận ra rằng rất nhiều leader không hiểu được giá trị của việc thường xuyên chia sẻ vision, chia sẻ công việc với team. Họ chỉ nghĩ giao việc và team cần làm. Điều này có thể dẫn đến trường hợp nhiều lúc sản phẩm cần thay đổi => dev thì nghĩ ô manager cứ thay đổi liên xoành xoạch. Họ cũng sẽ rất mệt mỏi. Nếu manager tốt thì sẽ chia sẻ với team là "à trước kia ae mình nghĩ làm thế này ngon, nhưng giờ sản phẩm ra, khách hàng feed back chắc ae mình cần thay đổi". Việc tương tác này là hết sức quan trọng.

- Với một ý tưởng về sản phẩm, nó cần chỉ ra được giải quyết được những paint point gì, từ đó có business model hợp lý. Một sản phẩm mới như thời ecommece mới xuất hiện, nó tạo ra mô hình kinh doanh mới. Mô hình này thực sự rất hữu ích với người dùng. Bởi nó cho người ta ngồi ở nhà mà có thể mua được hàng. Tuy nhiên nếu nhìn lại quá trình phát triển của các trang thương mại điện tử lớn thì rõ ràng họ cũng phải đi từng chặng đường một. Có khi cả 5-7 năm đánh đổi. Từ lúc sản phẩm mới hình thành, thay đổi và phát triển không ngừng.

- Sau khi có reqirement hòm hòm, BA sẽ là người chủ trì, vẽ flow nghiệp vụ cho sản phẩm => bước tiếp theo tôi cần làm là vẽ được rõ ràng flow nghiệp vụ, data flow (note ngày 13/06/2020). Cơ bản khi hoàn thành flow nghiệp vụ ta sẽ ra được cái nhìn khá rõ ràng về hệ thống mình đang phát triển

- Tiếp sau flow nghiệp vụ, data flow sẽ là thiết kế tổng quan hệ thống, biểu đồ ER, các service (hay nói cách khác là vẽ ra được architechture phù hợp cho hệ thống), lưu trữ, tương tác
# Requirement
Người dùng hệ thống: người mua, người bán hàng, người quản lý chiến dịch marketing hệ thống.
V1 giả sử chưa support việc thanh toán qua ví điện tử, internet banking. Gỉa sử người giao hàng sẽ nhận tiền mặt về giao. Tuy nhiên thiết kế hệ thống cần hướng đến việc thanh toán qua ví điện tử, internet banking.

- Là người dùng trên hệ thống tôi có thêm mới, bỏ bớt các sản phẩm ra khỏi 1 đơn hàng khi mua
- Là người dùng trên hệ thống tôi có thể tiến hành checkout các sản phẩm đã chọn mua trong một đơn hàng
- Là người dùng tôi muốn biết được trạng thái của đơn hàng
- Là người mua hàng tôi có thể xem lại lịch sử các đơn hàng đã mua của mình
- Là người bán hàng tôi có thể thêm mới hoặc xóa một mặt hàng trên hệ thống
- Là người bán hàng tôi có thể sửa thông tin mặt hàng mà mình đang bán
- Là người bán hàng tôi có thể xem lại thông tin thống kê các loại mặt hàng đã được khách hàng mua theo một khoảng thời gian được chọn
- Là người bán hàng tôi có thể xem thông tin thu nhập từ việc bán các mặt hàng, mỗi mặt hàng sẽ có giá thay đổi, do đó hệ thống cần lưu trữ được thông tin này
- Là người bán hàng tôi có thể xem thống kê theo khách hàng đã mua các sản phẩm của tôi
- Là người bán hàng tôi muốn được thông báo khi có 1 khách hàng đặt mua hàng của tôi
- Là người marketing tôi muốn tạo một chiến dịch quảng cáo, chiến dịch này sẽ thực hiện giảm giá trên một số mặt hàng mà tôi được chọn với số lượng và thời gian nhát định, người bán hàng lúc này là Cherry Trading
- Là người marketing tôi muốn xem lại thông tin số lượng đã bán ứng với từng mặt hàng trong đợt sale
- Là người marketing tôi muốn xem khách hàng truy cập vào hệ thống khi có đợt sale
- Là người marketing tôi muốn tạo ra một đợt sale với toàn bộ mặt hàng có trên hệ thống
- Là người giao hàng tôi muốn biết đơn hàng được giao đến đâu
- Là người giao hàng tôi muốn biết các đơn hàng mình cần phải xử lý
- Là người giao hàng tôi muốn biết các nơi cần đến để lấy các mặt hàng theo từng đơn
- Là người giao hàng tôi muốn được cập nhập trạng thái đã giao thành công đơn hàng cho người mua
- Là người quản lý tài chính tôi muốn xem lại thống kê các mặt hàng đã bán trên thống thống để tôi dễ dàng kiểm tra doanh thu
# Project Analysis

# Project Design
