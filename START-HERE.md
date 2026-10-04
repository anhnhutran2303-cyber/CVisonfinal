# CVision — tạo CV, thư ứng tuyển và tối ưu hồ sơ

Gói này có toàn bộ mã nguồn đã sửa và thêm tính năng. Chưa push lên GitHub hoặc triển khai lên website công khai do bước đăng nhập GitHub chưa hoàn tất.

## Tính năng mới nhất

1. **CV Builder:** nhập thông tin bằng biểu mẫu, chọn mẫu Modern hoặc Classic, chọn tiêu đề mục tiếng Việt/Anh, xem bản nháp và tải Word/TXT. Nút **Use this CV in Analyzer** đưa CV mới sang phân tích.
2. **Cover Letter:** lấy CV từ Analyzer hoặc CV Builder, nhập JD, công ty và vị trí; chọn 1–3 nội dung thật từ CV để tạo thư theo mẫu, sửa thư và tải Word/TXT. Dùng được không cần API key. Ngôn ngữ áp dụng cho phần khung thư, không tự dịch trích đoạn CV.
3. **Giữ bản nháp trong phiên:** đổi trang rồi quay lại vẫn có CV đã tạo và thư đã sửa. Khi đổi công ty/JD, cần tạo lại thư trước khi tải để tránh dùng bản cũ. Tải file trước khi đóng ứng dụng.

## Tính năng từ bản trước vẫn có

- Keyword Match: đối chiếu từ khóa CV–JD, nhóm kỹ năng, bộ lọc, ngữ cảnh và CSV.
- Searchability: checklist thông tin liên hệ, tiêu đề mục, văn bản và số liệu trong bullet.
- Optimize & Re-scan: chỉnh sửa CV/JD ngay trong báo cáo, quét lại và tải TXT.
- Before / after: so sánh trước/sau khi JD, vai trò và cấu hình phân tích giữ nguyên.
- Sửa nhận diện tiếng Việt, loại phúc lợi khỏi yêu cầu JD và ghi rõ điểm fallback là kết quả cơ bản.

## Cách đưa lên repo mới nhanh nhất

1. Giải nén ZIP và mở thư mục **CVision-updated**.
2. Mở https://github.com/anhnhutran2303-cyber/CVisonfinal ở tab **Code**.
3. Với repo trống, chọn **uploading an existing file**; với repo có file, chọn **Add file → Upload files**.
4. Tải các file và thư mục BÊN TRONG `CVision-updated` lên, rồi **Commit changes**. `app.py`, `requirements.txt`, `backend/` và `frontend/` phải ở thư mục gốc repo. Giữ cả `.streamlit/config.toml` để có giao diện đúng.
5. Trên Streamlit Community Cloud, tạo app từ repo `anhnhutran2303-cyber/CVisonfinal`, nhánh `main`, file chạy `app.py`.

Không tải riêng file ZIP vào repo để chạy app. Dùng mã nguồn đã giải nén. Hướng dẫn kỹ thuật và cấu hình nằm trong README.md của mã nguồn.

## Nội dung gói

- `CVision-updated/`: toàn bộ mã nguồn đã kiểm thử, không chứa database, CV người dùng hoặc key bí mật.
- `CVision-update.patch`: toàn bộ thay đổi từ commit gốc `f3a75e1960d327b48dcf9f31a658c16940848bb1`.
- `docs/application-documents.md`: CV Builder và Cover Letter.
- `docs/resume-optimization.md`: các tính năng tối ưu và so sánh.
- `docs/bugfix-2026-10-04.md`: chi tiết sửa lỗi tiếng Việt và fallback.

Nếu cập nhật repo cũ bằng patch, chỉ áp dụng khi đang ở commit gốc và không có thay đổi cục bộ:

```sh
git switch -c codex/resume-optimization
git apply --check /path/to/CVision-update.patch
git apply /path/to/CVision-update.patch
python -m pip install -r requirements-dev.txt
python -m pytest -q
```

## Cấu hình và kiểm thử

CV Builder, xuất Word, Cover Letter và các kiểm tra cơ bản không cần API key. Muốn phân tích ngữ nghĩa bằng Gemini thì chủ app đặt `GEMINI_API_KEY` trong Streamlit Secrets; không đưa key vào mã nguồn hoặc chat.

302 tests và 99 subtests đã qua với Gemini giả lập và database cô lập; sau chỉnh bố cục Word, 20 kiểm thử xuất tài liệu và giao diện liên quan được chạy lại thành công. Python compile và diff check đều qua. Bốn file Word mẫu (hai mẫu CV, thư tiếng Việt/Anh) đã được render và kiểm tra chữ, dấu và bố cục. Patch đã được kiểm tra trên bản gốc. Chưa kiểm thử AI với key thật hoặc website sau triển khai.

Các bản nháp mới chỉ nằm trong phiên làm việc. Workspace SQLite cũ vẫn dùng chung giữa người dùng của cùng app; chưa bổ sung tài khoản hoặc phân quyền. Không thay đổi schema hoặc xóa lịch sử cũ.
