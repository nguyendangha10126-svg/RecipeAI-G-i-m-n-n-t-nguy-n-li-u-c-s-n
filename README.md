RecipeAI — Gợi ý món ăn từ nguyên liệu có sẵn
RecipeAI là ứng dụng giúp người dùng tìm món ăn phù hợp với các nguyên liệu hiện có. Hệ thống cung cấp danh sách món gợi ý, công thức, thời gian nấu, độ khó và nguyên liệu còn thiếu. AI hỗ trợ gợi ý/xếp hạng dựa trên dữ liệu công thức; kết quả luôn cần được kiểm tra và trình bày minh bạch.
Mục tiêu
- Giảm thời gian suy nghĩ hôm nay nấu món gì.
- Tận dụng nguyên liệu sẵn có và hạn chế lãng phí thực phẩm.
- Hỗ trợ người mới nấu ăn bằng hướng dẫn từng bước.
- Cung cấp khu vực Admin để quản lý dữ liệu và vận hành hệ thống.
Tài liệu dự án
Tệp	Nội dung
01_TAI_LIEU_NGHIEP_VU.md	Mục tiêu, đối tượng, chức năng, quy tắc và tiêu chí nghiệm thu
02_TAI_LIEU_GIAO_DIEN_AI_THUC_THI.md	Màn hình, luồng AI, schema minh họa và trạng thái UI
03_TAI_LIEU_KY_THUAT_AI_FRONTEND.md	Kiến trúc frontend, component, API client, bảo mật và kiểm thử
04_TAI_LIEU_KY_THUAT_AI_ADMIN.md	Phân hệ quản trị, API tham khảo, dữ liệu và bảo mật
AGENTS.md	Hướng dẫn cho AI coding agent khi đọc, sửa và triển khai dự án


Chức năng dự kiến
Người dùng
- Nhập/chọn nguyên liệu có sẵn.
- Lọc theo loại món, chế độ ăn, thời gian và độ khó.
- Xem danh sách gợi ý và công thức chi tiết.
- Xem nguyên liệu còn thiếu.
- Lưu món yêu thích, xem lịch sử và quản lý hồ sơ nếu đăng nhập.
Admin
- Dashboard tổng quan.
- Quản lý món ăn, nguyên liệu và danh mục.
- Quản lý người dùng và phản hồi/báo cáo.
- Quản lý cấu hình vận hành AI theo quyền được cấp.
- Theo dõi nhật ký thao tác quản trị.
Công nghệ
Tài liệu này không tự áp đặt framework hoặc cơ sở dữ liệu. Trước khi triển khai, hãy kiểm tra mã nguồn hiện có và giữ nguyên stack đang dùng nếu chưa có yêu cầu đổi công nghệ. Ghi lại stack đã chọn tại đây khi dự án được khởi tạo, ví dụ:
- Frontend: <framework và phiên bản>
- Backend: <framework và phiên bản>
- Database: <hệ quản trị và phiên bản>
- AI provider/model: <nhà cung cấp hoặc chế độ local/fallback>
- Công cụ chạy và kiểm thử: <lệnh thực tế>
Thiết lập và chạy
Các lệnh chạy phụ thuộc stack thực tế, vì vậy không nên sao chép lệnh giả định trước khi có mã nguồn. Khi triển khai, bổ sung:
1. Phiên bản runtime cần thiết.
2. Cách cài dependencies.
3. Cách tạo database và chạy migration/seed.
4. Cách cấu hình .env.
5. Lệnh chạy frontend/backend.
6. Lệnh lint, test và build.
Tạo .env.example chỉ với tên biến và giá trị mẫu. Không commit .env, khóa AI, mật khẩu database hoặc token thật.
Nguyên tắc an toàn
- Khóa API AI chỉ được sử dụng phía backend.
- Backend phải xác thực và phân quyền mọi endpoint riêng tư/admin.
- Không lưu mật khẩu dạng văn bản thuần.
- Kiểm tra dữ liệu đầu vào và cấu trúc đầu ra của AI.
- Không trình bày gợi ý AI như tư vấn y tế hoặc bảo đảm an toàn dị ứng.
- Không bịa kết quả khi dịch vụ AI lỗi; sử dụng dữ liệu công thức có sẵn nếu phù hợp hoặc thông báo lỗi rõ ràng.
Lộ trình đề xuất
1. Chốt stack và cấu trúc repository.
2. Xây dựng dữ liệu món ăn/nguyên liệu mẫu.
3. Hoàn thiện luồng nhập nguyên liệu và gợi ý dựa trên dữ liệu.
4. Bổ sung AI qua backend và validate đầu ra.
5. Hoàn thiện xác thực, yêu thích và lịch sử.
6. Xây dựng khu vực Admin.
7. Kiểm thử, sửa lỗi, responsive và viết hướng dẫn triển khai.
Trạng thái
Tệp này là bộ tài liệu đặc tả ban đầu. Các endpoint, kiểu dữ liệu và cấu trúc thư mục trong tài liệu kỹ thuật là đề xuất cho đến khi được đối chiếu với mã nguồn thực tế.