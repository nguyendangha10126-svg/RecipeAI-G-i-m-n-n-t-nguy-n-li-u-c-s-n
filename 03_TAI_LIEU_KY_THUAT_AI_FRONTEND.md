RecipeAI — Tài liệu kỹ thuật Frontend
1. Mục tiêu
Tài liệu này hướng dẫn AI lập trình hoặc thành viên frontend xây dựng giao diện RecipeAI có cấu trúc rõ ràng, dễ kiểm thử và dễ bảo trì. Nếu dự án đã chọn framework cụ thể, cần giữ framework hiện có; không tự ý viết lại toàn bộ stack khi chưa được yêu cầu.
2. Nguyên tắc kiến trúc
- Tách giao diện, component, logic nghiệp vụ phía client và lớp gọi API.
- Không gọi trực tiếp nhà cung cấp AI từ frontend.
- Không chứa secret, API key hoặc quyền admin trong mã client.
- Không tin dữ liệu từ client; backend vẫn phải xác thực và kiểm tra.
- Ưu tiên component tái sử dụng và kiểu dữ liệu rõ ràng.
- Dùng trạng thái loading/error/empty/success nhất quán.
3. Cấu trúc thư mục tham khảo
src/
  app/ or pages/
  components/
    layout/
    recipe/
    ingredients/
    forms/
    feedback/
  features/
    auth/
    recipe-search/
    favorites/
    profile/
    admin/
  services/
    api-client
    auth-service
    recipe-service
    favorite-service
  hooks/
  types/
  utils/
  styles/
  assets/
Đây là cấu trúc tham khảo; điều chỉnh theo framework đang dùng. Không tạo song song nhiều cấu trúc routing khác nhau.
4. Component chính
- AppLayout: bố cục chung, header, footer.
- Header / Navigation: điều hướng.
- IngredientInput: tìm kiếm và thêm nguyên liệu.
- IngredientChipList: danh sách nguyên liệu đã chọn.
- RecipeFilters: bộ lọc món ăn.
- RecipeCard: thẻ món ăn.
- RecipeList: danh sách kết quả và trạng thái rỗng.
- RecipeDetail: thông tin và các bước nấu.
- FavoriteButton: lưu/bỏ lưu món.
- LoadingState, ErrorState, EmptyState: trạng thái dùng chung.
- ProtectedRoute hoặc cơ chế tương đương: trải nghiệm điều hướng; không thay thế phân quyền backend.
- AdminLayout, AdminTable, AdminForm: thành phần khu vực quản trị.
5. Kiểu dữ liệu gợi ý
export type Difficulty = "easy" | "medium" | "hard";

export interface RecipeSummary {
  recipeId: string;
  name: string;
  summary?: string;
  imageUrl?: string;
  availableIngredients: string[];
  missingIngredients: string[];
  cookingMinutes: number;
  difficulty: Difficulty;
  servings: number;
}

export interface RecipeDetail extends RecipeSummary {
  ingredients: Array<{
    name: string;
    quantity?: string;
    available: boolean;
  }>;
  steps: string[];
  notice?: string;
}

export interface RecipeSuggestionRequest {
  ingredients: string[];
  filters?: {
    mealType?: string;
    diet?: string;
    maxCookingMinutes?: number;
    difficulty?: Difficulty | "any";
    servings?: number;
  };
}

export interface RecipeSuggestionResponse {
  items: RecipeSummary[];
  source?: string;
  notice?: string;
}
Các kiểu trên là hợp đồng gợi ý; cần khớp với API backend thực tế trước khi tích hợp.
6. Quản lý state
- State cục bộ cho input, bộ lọc, mở/đóng modal.
- State dữ liệu máy chủ cho kết quả gợi ý, chi tiết món, hồ sơ và yêu thích.
- Khi gửi yêu cầu mới, loại bỏ hoặc đánh dấu kết quả cũ để tránh gây hiểu nhầm.
- Chống gửi request lặp do nhấn nút liên tục.
- Hủy request cũ nếu người dùng thay đổi tìm kiếm và công nghệ đang dùng hỗ trợ.
- Không lưu dữ liệu nhạy cảm vào localStorage. Chỉ lưu tùy chọn không nhạy cảm nếu cần.
7. Lớp API
Tạo một API client dùng chung:
- Đặt base URL qua biến môi trường public phù hợp với framework.
- Thiết lập timeout nếu thư viện hỗ trợ.
- Chuẩn hóa xử lý lỗi HTTP và lỗi mạng.
- Gửi token theo cơ chế xác thực được backend hỗ trợ; ưu tiên cookie HttpOnly, Secure, SameSite nếu kiến trúc cho phép.
- Không log token, mật khẩu hoặc dữ liệu cá nhân.
- Kiểm tra response trước khi sử dụng; không giả định server luôn trả dữ liệu hợp lệ.
Các nhóm service đề xuất:
- recipeService: gợi ý, danh sách, chi tiết.
- favoriteService: lấy, thêm, xóa yêu thích.
- authService: đăng nhập, đăng ký, đăng xuất, hồ sơ.
- adminService: thao tác quản trị, chỉ gọi khi người dùng có quyền.
8. Bảo mật frontend
- Không xem việc ẩn route/nút là cơ chế bảo mật.
- Làm sạch/escape nội dung người dùng khi hiển thị; tránh render HTML tùy ý.
- Không đưa thông tin bí mật vào file .env được bundle ra trình duyệt.
- Kiểm tra URL ảnh và không render URL không tin cậy tùy tiện.
- Không hiển thị stack trace, SQL error hoặc thông tin nội bộ cho người dùng.
- Thực hiện kiểm tra quyền ở backend với mọi endpoint riêng tư.
- Nếu dùng cookie xác thực, cân nhắc biện pháp chống CSRF theo kiến trúc backend.
9. UX và hiệu năng
- Chia component hợp lý, tránh component khổng lồ.
- Lazy-load các trang ít dùng nếu framework hỗ trợ.
- Tối ưu ảnh và chỉ tải ảnh cần thiết.
- Có skeleton hoặc spinner khi tải dữ liệu.
- Không để layout nhảy mạnh khi ảnh/dữ liệu xuất hiện.
- Dùng debounce cho tìm kiếm nguyên liệu nếu gọi API theo từng ký tự.
- Hỗ trợ responsive và bàn phím.
10. Kiểm thử
- Unit test: chuẩn hóa input, validation, component trọng yếu.
- Integration test: gửi yêu cầu gợi ý, xử lý response, lỗi API.
- UI test: thêm/xóa nguyên liệu, áp dụng bộ lọc, xem chi tiết, lưu yêu thích.
- Accessibility check: label, focus, keyboard navigation, contrast.
- Kiểm tra quyền điều hướng chỉ để UX; xác minh backend vẫn chặn API trái quyền.
11. Checklist bàn giao
- [ ] Không có lỗi lint/type/build.
- [ ] Có file .env.example chỉ chứa tên biến và giá trị mẫu không bí mật.
- [ ] Không commit .env có secret.
- [ ] Các màn hình có trạng thái loading/error/empty.
- [ ] Form có validation và thông báo dễ hiểu.
- [ ] Responsive trên mobile và desktop.
- [ ] API được gọi qua lớp service.
- [ ] Có hướng dẫn chạy dự án trong README.