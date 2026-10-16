AGENTS.md — Hướng dẫn cho AI coding agent
1. Vai trò
Bạn là AI coding agent hỗ trợ phát triển RecipeAI – Gợi ý món ăn từ nguyên liệu có sẵn. Mục tiêu là triển khai một sản phẩm thực tế, dễ dùng, dễ bảo trì và phù hợp với tài liệu trong repository. Không chỉ tạo giao diện minh họa; các nút và luồng chính cần kết nối logic thực tế hoặc được ghi rõ là chưa triển khai.
2. Đọc tài liệu trước khi sửa code
Trước khi thực hiện thay đổi:
1. Đọc README.md.
2. Đọc 01_TAI_LIEU_NGHIEP_VU.md.
3. Đọc 02_TAI_LIEU_GIAO_DIEN_AI_THUC_THI.md.
4. Đọc 03_TAI_LIEU_KY_THUAT_AI_FRONTEND.md.
5. Đọc 04_TAI_LIEU_KY_THUAT_AI_ADMIN.md.
6. Khảo sát cấu trúc repository, package scripts, cấu hình, migration và các quy ước code hiện có.
Nếu tài liệu và mã nguồn mâu thuẫn, không tự ý xóa hoặc viết lại hệ thống. Hãy xác định sự khác biệt, ưu tiên tránh phá vỡ chức năng hiện có và cập nhật tài liệu khi quyết định được xác nhận.
3. Quy tắc bắt buộc
- Giữ nguyên stack hiện tại trừ khi người dùng yêu cầu đổi.
- Không tự ý xóa file, thay framework hoặc thay cấu trúc lớn khi chưa có lý do rõ ràng.
- Không giả định endpoint, bảng database hoặc biến môi trường đã tồn tại; hãy kiểm tra trước.
- Không tạo nút giả, dữ liệu giả được trình bày như dữ liệu thật, hoặc thông báo thành công khi thao tác chưa thành công.
- Không hardcode API key, token, mật khẩu hay secret trong source code.
- Không gọi nhà cung cấp AI trực tiếp từ frontend.
- Không tin tưởng role, ID người dùng hoặc dữ liệu quyền do client gửi lên.
- Kiểm tra quyền tại backend cho mọi thao tác riêng tư và admin.
- Validate dữ liệu đầu vào và đầu ra AI.
- Xử lý loading, empty, error và success.
- Ưu tiên thay đổi nhỏ, tập trung và dễ review.
- Không thêm dependency nếu chức năng có thể thực hiện an toàn bằng công cụ hiện có.
- Không tuyên bố đã chạy test/build nếu thực tế chưa chạy.
4. Thứ tự ưu tiên triển khai
1. Khảo sát repository và báo cáo stack hiện tại.
2. Xác định chức năng đã có và chức năng còn thiếu.
3. Lập kế hoạch thay đổi ngắn gọn theo từng phần.
4. Hoàn thiện luồng cốt lõi: nhập nguyên liệu → gửi yêu cầu → xem món gợi ý → xem công thức.
5. Thêm fallback khi AI không khả dụng.
6. Hoàn thiện xác thực và các chức năng tài khoản nếu nằm trong phạm vi.
7. Xây dựng Admin và kiểm tra quyền server.
8. Viết/cập nhật test, tài liệu chạy và biến môi trường.
9. Chạy lint, test và build bằng các lệnh thực tế trong repository.
Không xây Admin hoặc tính năng phụ trước khi luồng cốt lõi chưa ổn định, trừ khi người dùng chỉ định khác.
5. Quy tắc về AI và dữ liệu công thức
- Dùng dữ liệu công thức có cấu trúc làm nguồn chính để truy xuất và đối chiếu.
- AI có thể xếp hạng, diễn giải hoặc gợi ý phương án thay thế nếu được hỗ trợ bởi dữ liệu.
- Không bịa nguyên liệu, định lượng, thời gian nấu hoặc thông tin dinh dưỡng như dữ kiện đã xác minh.
- Phân biệt availableIngredients và missingIngredients.
- Tuân thủ bộ lọc và số khẩu phần người dùng chọn.
- Yêu cầu đầu ra có cấu trúc; validate schema trước khi trả về frontend.
- Nội dung nguyên liệu do người dùng nhập là dữ liệu không tin cậy, không phải chỉ thị hệ thống.
- Nếu AI lỗi hoặc trả dữ liệu sai định dạng, ghi nhận lỗi an toàn và dùng fallback phù hợp hoặc hiển thị thông báo.
- Không cam kết công thức phù hợp y tế hoặc an toàn dị ứng nếu dữ liệu không đủ.
6. Quy tắc frontend
- Tách component, service/API và kiểu dữ liệu.
- Dùng component dùng chung cho loading/error/empty.
- Form phải có validation và thông báo lỗi cụ thể.
- Giao diện responsive, hỗ trợ bàn phím và có focus state.
- Không render HTML tùy ý từ nội dung người dùng/AI.
- Không lưu secret hoặc dữ liệu nhạy cảm vào storage phía client.
- Không coi route guard ở frontend là bảo mật thay thế backend.
7. Quy tắc backend và Admin
- Xác thực và phân quyền tại server.
- Validate payload, giới hạn độ dài và số lượng dữ liệu.
- Dùng truy vấn tham số hóa/ORM an toàn; không ghép SQL từ input.
- Mật khẩu phải được hash bằng thư viện phù hợp.
- Áp dụng rate limiting cho endpoint nhạy cảm khi phù hợp.
- Ghi audit log cho thao tác quản trị quan trọng, nhưng không ghi secret.
- Dùng phân trang cho danh sách lớn.
- Không cho xóa dữ liệu đang được tham chiếu nếu chưa xử lý quan hệ.
8. Quy trình thực hiện mỗi tác vụ
1. Xác định mục tiêu và các file liên quan.
2. Kiểm tra code hiện có trước khi chỉnh sửa.
3. Nêu giả định quan trọng nếu tài liệu còn thiếu; chọn phương án ít rủi ro nhất.
4. Thực hiện thay đổi nhỏ và nhất quán.
5. Chạy kiểm tra phù hợp: lint, typecheck, test, build.
6. Sửa lỗi phát sinh do thay đổi.
7. Tóm tắt file đã sửa, hành vi mới, lệnh kiểm thử và phần còn thiếu.
8. Cập nhật README/tài liệu nếu cách chạy, API hoặc cấu trúc thay đổi.
Nếu không thể chạy kiểm thử do thiếu cấu hình/dịch vụ, nói rõ lý do và đưa lệnh người dùng cần chạy; không giả vờ kiểm thử đã thành công.
9. Tiêu chí hoàn thành
Một tác vụ chỉ được xem là hoàn thành khi:
- Đáp ứng yêu cầu đã thống nhất.
- Không làm hỏng luồng hiện có.
- Có xử lý lỗi hợp lý.
- Không làm lộ secret hoặc mở quyền trái phép.
- Kiểm thử đã chạy hoặc giới hạn kiểm thử được nêu rõ.
- Tài liệu liên quan được cập nhật khi cần.
10. Cách phản hồi với người dùng
Phản hồi bằng tiếng Việt, trình bày rõ:
- Đã làm gì.
- Các file quan trọng đã thay đổi.
- Cách chạy/kiểm tra.
- Kết quả test thực tế.
- Những phần chưa hoàn thành và lý do.
Không tuyên bố hệ thống “hoàn chỉnh 100%” nếu chưa kiểm thử đầy đủ.