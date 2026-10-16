RecipeAI — Tài liệu nghiệp vụ
Tên dự án: RecipeAI – Gợi ý món ăn từ nguyên liệu có sẵn
Phiên bản: 1.0
Loại tài liệu: Business Requirements / nghiệp vụ sản phẩm
1. Tổng quan
RecipeAI là ứng dụng hỗ trợ người dùng tìm ý tưởng nấu ăn từ những nguyên liệu họ đang có. Người dùng nhập hoặc chọn nguyên liệu, hệ thống phân tích dữ liệu và đưa ra các món phù hợp, kèm công thức, thời gian nấu, độ khó và nguyên liệu còn thiếu nếu có.
Mục tiêu là giảm thời gian nghĩ món, hạn chế lãng phí thực phẩm và giúp người dùng nấu ăn dễ dàng hơn. AI có vai trò hỗ trợ gợi ý; kết quả cần rõ ràng, thực tế và không được trình bày nội dung chưa kiểm chứng như sự thật tuyệt đối.
2. Vấn đề và cơ hội
- Người dùng có nguyên liệu trong tủ lạnh nhưng chưa biết nấu món gì.
- Tìm công thức trên mạng thường yêu cầu nguyên liệu mà người dùng không có.
- Thực phẩm có thể bị bỏ phí vì không được sử dụng kịp thời.
- Người mới nấu ăn cần hướng dẫn từng bước, dễ hiểu.
3. Mục tiêu sản phẩm
1. Cho phép nhập nhiều nguyên liệu nhanh chóng.
2. Đề xuất các món phù hợp với nguyên liệu có sẵn.
3. Hiển thị công thức, khẩu phần, thời gian và độ khó.
4. Cho phép lọc theo nhu cầu như món chay, bữa ăn, thời gian nấu và chế độ ăn.
5. Cho phép lưu món yêu thích và xem lại lịch sử gợi ý nếu đã đăng nhập.
6. Cung cấp khu vực quản trị để quản lý món ăn, nguyên liệu, danh mục và nội dung hệ thống.
4. Đối tượng người dùng
- Khách chưa đăng nhập: thử nhập nguyên liệu, xem gợi ý và công thức công khai.
- Người dùng đã đăng nhập: lưu món yêu thích, xem lịch sử và quản lý hồ sơ cá nhân.
- Quản trị viên (Admin): quản lý dữ liệu, kiểm duyệt nội dung, theo dõi hoạt động và xử lý báo cáo.
- Hệ thống AI: xử lý yêu cầu và tạo gợi ý dựa trên dữ liệu nguyên liệu/công thức được cung cấp.
5. Phạm vi chức năng
5.1. Chức năng người dùng
- Trang chủ giới thiệu sản phẩm và nút bắt đầu gợi ý.
- Nhập nguyên liệu bằng ô tìm kiếm/chọn từ danh sách; thêm và xóa nguyên liệu.
- Chọn bộ lọc: món chính/món phụ/đồ uống, chay/mặn, thời gian nấu, độ khó.
- Xem danh sách món gợi ý và mức độ phù hợp với nguyên liệu.
- Xem chi tiết món: mô tả, ảnh (nếu có), nguyên liệu, định lượng, khẩu phần, thời gian, độ khó và các bước nấu.
- Hiển thị nguyên liệu còn thiếu, không tự động coi nguyên liệu chưa nhập là đang có.
- Lưu/bỏ lưu món yêu thích (yêu cầu đăng nhập).
- Xem lịch sử gợi ý và quản lý hồ sơ (yêu cầu đăng nhập).
- Gửi phản hồi hoặc báo cáo nội dung không phù hợp.
5.2. Chức năng Admin
- Đăng nhập và đăng xuất an toàn.
- Dashboard thống kê tổng quan.
- CRUD món ăn, nguyên liệu, danh mục và thẻ phân loại.
- Quản lý tài khoản người dùng và trạng thái tài khoản.
- Xem lịch sử yêu cầu AI ở mức cần thiết cho vận hành.
- Kiểm duyệt phản hồi/báo cáo.
- Quản lý cấu hình gợi ý, giới hạn sử dụng và thông báo.
- Ghi nhận nhật ký hoạt động quản trị.
6. Luồng nghiệp vụ chính
1. Người dùng mở trang gợi ý món.
2. Nhập/chọn các nguyên liệu hiện có.
3. Tùy chọn bộ lọc và số khẩu phần.
4. Gửi yêu cầu.
5. Hệ thống kiểm tra dữ liệu đầu vào, chuẩn hóa tên nguyên liệu và kiểm tra giới hạn sử dụng.
6. Bộ gợi ý tìm công thức phù hợp từ dữ liệu đã có; AI có thể hỗ trợ xếp hạng hoặc diễn giải.
7. Hệ thống trả danh sách món, điểm phù hợp/giải thích, thời gian nấu và nguyên liệu thiếu.
8. Người dùng mở chi tiết món, lưu món hoặc điều chỉnh nguyên liệu để tìm lại.
Nếu AI gặp lỗi hoặc không khả dụng, hệ thống nên trả về các công thức khớp từ cơ sở dữ liệu khi có thể và thông báo rõ ràng; không hiển thị kết quả giả như thể đã được AI xử lý thành công.
7. Quy tắc nghiệp vụ
- Phải có ít nhất một nguyên liệu trước khi gửi yêu cầu.
- Tên nguyên liệu được chuẩn hóa để hạn chế trùng lặp do viết hoa, khoảng trắng hoặc cách viết phổ biến.
- Kết quả ưu tiên công thức dùng được nhiều nguyên liệu đang có.
- Nguyên liệu thiếu phải được tách riêng khỏi nguyên liệu sẵn có.
- Bộ lọc của người dùng phải được áp dụng khi xếp hạng kết quả.
- Không cam kết món ăn an toàn với dị ứng chỉ dựa trên suy luận AI. Nếu người dùng khai báo dị ứng, cần hiển thị cảnh báo và lọc theo dữ liệu thành phần có sẵn.
- Thời gian và khẩu phần là ước lượng tham khảo.
- Dữ liệu do người dùng nhập phải được kiểm tra, giới hạn độ dài và xử lý an toàn.
- Không công khai dữ liệu cá nhân hoặc lịch sử riêng tư của người dùng cho tài khoản khác.
8. Yêu cầu phi chức năng
- Giao diện responsive trên điện thoại, máy tính bảng và máy tính.
- Trạng thái loading, rỗng, lỗi và thành công phải rõ ràng.
- Tác vụ phổ biến nên phản hồi nhanh; nếu AI cần thêm thời gian, hiển thị trạng thái chờ.
- Xác thực và phân quyền phía máy chủ, không chỉ ẩn nút trên giao diện.
- Bảo vệ thông tin đăng nhập, khóa API và dữ liệu cá nhân.
- Có kiểm tra dữ liệu đầu vào, xử lý lỗi và nhật ký vận hành.
- Nội dung dễ tiếp cận, tiếng Việt tự nhiên, nút bấm có nhãn rõ ràng.
9. Tiêu chí nghiệm thu
- Người dùng có thể thêm/xóa nguyên liệu và gửi yêu cầu hợp lệ.
- Kết quả gợi ý hiển thị món ăn cùng công thức và nguyên liệu thiếu.
- Bộ lọc ảnh hưởng đúng đến kết quả.
- Người dùng có thể lưu và bỏ lưu món sau khi đăng nhập.
- Người chưa đăng nhập không truy cập được chức năng yêu cầu tài khoản.
- Tài khoản thường không truy cập được trang/API Admin.
- Admin có thể thêm, sửa, xem và xóa dữ liệu theo quyền được cấp.
- Lỗi từ AI hoặc máy chủ được xử lý có thông báo, không làm treo giao diện.
- Không có khóa bí mật hoặc thông tin nhạy cảm được đưa vào mã frontend.
10. Ngoài phạm vi phiên bản đầu
- Đặt mua thực phẩm hoặc tích hợp thanh toán.
- Chẩn đoán dinh dưỡng/y tế.
- Nhận diện nguyên liệu từ ảnh nếu chưa có mô-đun xử lý ảnh.
- Tự động đảm bảo an toàn dị ứng hoặc độ chính xác tuyệt đối của công thức.
- Tích hợp thiết bị nhà bếp thông minh.
11. Chỉ số đánh giá
- Tỷ lệ yêu cầu gợi ý trả kết quả thành công.
- Tỷ lệ người dùng mở chi tiết món sau khi xem danh sách.
- Số món được lưu yêu thích.
- Thời gian phản hồi trung bình.
- Tỷ lệ lỗi và tỷ lệ phản hồi tiêu cực.