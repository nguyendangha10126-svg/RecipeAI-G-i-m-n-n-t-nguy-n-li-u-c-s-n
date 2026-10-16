RecipeAI — Tài liệu kỹ thuật khu vực Admin
1. Mục đích và ranh giới quyền hạn
Khu vực Admin dùng để quản lý dữ liệu và vận hành RecipeAI. Mọi quyền quản trị phải được kiểm tra ở backend; frontend chỉ hỗ trợ điều hướng và hiển thị phù hợp. Không được dựa vào một biến role ở trình duyệt để cấp quyền.
2. Vai trò
- User: sử dụng chức năng công khai và dữ liệu cá nhân của mình.
- Admin: quản lý dữ liệu nghiệp vụ và xử lý báo cáo theo quyền được cấp.
- System/service: xử lý yêu cầu gợi ý và tác vụ nền nếu có.
Nếu hệ thống có nhiều cấp quản trị, hãy định nghĩa quyền chi tiết theo từng hành động thay vì mặc định mọi admin có toàn quyền.
3. Các phân hệ
3.1. Dashboard
- Tổng số món ăn, nguyên liệu, người dùng.
- Số lượt yêu cầu gợi ý theo khoảng thời gian.
- Tỷ lệ yêu cầu thành công/thất bại nếu backend có đo lường.
- Các báo cáo mới cần xử lý.
- Chỉ hiển thị số liệu tổng hợp cần thiết; tránh lộ dữ liệu cá nhân.
3.2. Quản lý món ăn
- Danh sách, tìm kiếm, lọc, phân trang.
- Thêm/sửa thông tin món.
- Quản lý nguyên liệu, định lượng, khẩu phần, thời gian, độ khó và các bước.
- Quản lý ảnh/URL ảnh nếu tính năng được hỗ trợ.
- Trạng thái bản nháp/đã xuất bản/ẩn nếu có workflow.
- Kiểm tra dữ liệu trước khi lưu; xác nhận trước khi xóa.
3.3. Quản lý nguyên liệu
- Tạo, sửa, xem và xóa/ngừng sử dụng nguyên liệu.
- Chuẩn hóa tên và đơn vị.
- Ngăn dữ liệu trùng lặp theo quy tắc backend.
- Khi nguyên liệu đang được công thức sử dụng, ưu tiên ngừng hoạt động hoặc yêu cầu xử lý liên kết thay vì xóa gây lỗi dữ liệu.
3.4. Danh mục và thẻ
- Quản lý loại món, chế độ ăn, độ khó hoặc nhãn phân loại.
- Kiểm tra slug/mã định danh không trùng.
- Không cho xóa danh mục đang được sử dụng nếu chưa có phương án thay thế.
3.5. Người dùng
- Tìm kiếm theo thông tin được phép.
- Xem trạng thái tài khoản và ngày tạo.
- Khóa/mở khóa tài khoản theo chính sách.
- Không hiển thị mật khẩu, token hoặc thông tin xác thực.
- Ghi audit log với hành động tác động đến tài khoản.
3.6. Phản hồi và báo cáo
- Xem danh sách báo cáo.
- Phân loại trạng thái: mới, đang xử lý, đã giải quyết, từ chối.
- Ghi chú xử lý phù hợp.
- Hạn chế quyền xem dữ liệu riêng tư theo nhu cầu nghiệp vụ.
3.7. Cấu hình AI
- Bật/tắt nhà cung cấp AI hoặc chế độ dự phòng nếu kiến trúc hỗ trợ.
- Cấu hình giới hạn sử dụng và tham số không nhạy cảm.
- Không hiển thị giá trị đầy đủ của API key trên giao diện.
- Secret được quản lý bằng secret manager hoặc biến môi trường phía server.
- Thay đổi cấu hình quan trọng cần phân quyền và ghi nhật ký.
4. Quy ước API tham khảo
Các đường dẫn sau là gợi ý, cần điều chỉnh theo backend thực tế:
Method	Endpoint tham khảo	Mục đích
GET	/api/admin/dashboard	Số liệu tổng quan
GET	/api/admin/recipes	Danh sách món
POST	/api/admin/recipes	Tạo món
GET	/api/admin/recipes/:id	Chi tiết món
PATCH	/api/admin/recipes/:id	Cập nhật món
DELETE	/api/admin/recipes/:id	Xóa/ngừng món theo chính sách
GET	/api/admin/ingredients	Danh sách nguyên liệu
POST	/api/admin/ingredients	Tạo nguyên liệu
PATCH	/api/admin/ingredients/:id	Cập nhật nguyên liệu
GET	/api/admin/users	Danh sách người dùng
PATCH	/api/admin/users/:id/status	Cập nhật trạng thái
GET	/api/admin/reports	Danh sách báo cáo
PATCH	/api/admin/reports/:id	Cập nhật xử lý báo cáo


Backend phải xác minh danh tính, vai trò/quyền, schema đầu vào và quyền sở hữu dữ liệu ở mọi endpoint. Không coi bảng trên là API đã tồn tại nếu chưa được triển khai.
5. Mô hình dữ liệu khái niệm
Các thực thể có thể gồm:
- User: tài khoản, email/định danh, role, status, createdAt.
- Recipe: tên, mô tả, thời gian, độ khó, khẩu phần, trạng thái.
- Ingredient: tên chuẩn hóa, đơn vị mặc định, trạng thái.
- RecipeIngredient: liên kết món-nguyên liệu, định lượng và đơn vị.
- Category hoặc Tag: phân loại món.
- Favorite: liên kết người dùng và món ăn.
- SuggestionHistory: yêu cầu gợi ý và metadata cần thiết; hạn chế lưu dữ liệu nhạy cảm.
- FeedbackReport: nội dung phản hồi, trạng thái xử lý và người phụ trách.
- AuditLog: người thực hiện, hành động, đối tượng, thời điểm và kết quả.
Tên bảng/cột cuối cùng phụ thuộc hệ quản trị cơ sở dữ liệu và quy ước của dự án. Mật khẩu phải được hash bằng thuật toán phù hợp; không lưu dạng rõ.
6. Validation và xử lý lỗi
- Bắt buộc các trường quan trọng như tên món và bước nấu.
- Giới hạn độ dài chuỗi và số lượng phần tử.
- Thời gian, khẩu phần và định lượng phải nằm trong phạm vi hợp lý.
- Kiểm tra tham chiếu nguyên liệu/danh mục tồn tại.
- Trả mã lỗi HTTP phù hợp: 400 dữ liệu sai, 401 chưa xác thực, 403 không đủ quyền, 404 không tồn tại, 409 xung đột, 429 vượt giới hạn, 500 lỗi hệ thống.
- Không trả stack trace hoặc thông tin bí mật cho client.
7. Bảo mật và audit
- Dùng RBAC hoặc quyền chi tiết phía server.
- Mọi thao tác thay đổi dữ liệu quan trọng phải được xác thực.
- Có CSRF protection nếu dùng cookie và kiến trúc yêu cầu.
- Áp dụng rate limiting cho đăng nhập và endpoint nhạy cảm.
- Ghi log các hành động tạo/sửa/xóa, khóa tài khoản và thay đổi cấu hình.
- Không ghi mật khẩu, token, API key hoặc toàn bộ dữ liệu nhạy cảm vào log.
- Dùng phân trang và giới hạn kết quả; tránh trả toàn bộ dữ liệu lớn.
- Sao lưu dữ liệu và có quy trình phục hồi phù hợp.
8. Tiêu chí nghiệm thu Admin
- Người không có quyền nhận 401/403 khi gọi API admin.
- Admin có thể quản lý món ăn/nguyên liệu theo phạm vi được phép.
- Dữ liệu được validation ở server.
- Các thao tác nguy hiểm có xác nhận trên UI và kiểm soát ở backend.
- Lỗi được hiển thị dễ hiểu, không rò rỉ chi tiết nội bộ.
- Nhật ký có thể truy vết hành động quan trọng.