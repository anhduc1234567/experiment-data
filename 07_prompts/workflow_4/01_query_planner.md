# WF4 — Query planner

Một lượt lập plan và query; sau đó code thực hiện hybrid + rerank, giữ top1 mỗi query, tuần tự từng query. Prompt planner giống WF5; khác biệt nằm ở retrieval.

Các chỗ `{{...}}` là dữ liệu được chèn tại runtime. Đây là bản xuất để đọc; sửa Markdown không đổi prompt chạy.

Mỗi lần gọi chỉ dùng **một** biến thể theo ngành. Hướng dẫn group liệt kê đầy đủ để đọc; runtime chỉ chèn group có trong inventory báo cáo.

## Doanh nghiệp thường

```text
Lập kế hoạch lấy context từ một BCTC Việt Nam bằng tìm kiếm toàn văn.
Câu hỏi: {{question}}
Báo cáo cố định: {"company_name": "{{company_name}}", "report_type": "{{report_type}}", "report_time": "{{report_time}}", "sector": "Công nghiệp"}
Phân biệt doanh thu, lợi nhuận, số dư tài sản/nợ/vốn và dòng tiền; tỷ số cần đủ tử/mẫu.
Trả planner bằng tiếng Việt và 1–6 queries theo schema.
Mỗi query là một cụm tìm kiếm tự đủ nghĩa, gồm tên chỉ tiêu/keyword và kỳ nếu cần.
Phân tách câu hỏi nhiều ý thành các query bổ sung nhau; có thể dùng tên viết tắt
hoặc từ đồng nghĩa tài chính phù hợp, không sinh các biến thể trùng nghĩa vô ích.
Tỷ số cần tìm đủ thành phần; phân biệt số dư cuối kỳ, dồn tích trong kỳ và tiền thực thu/chi.
Có thể tìm cả bảng chính và chi tiết thuyết minh; không cần chọn tên section/subsection.
Chỉ tìm trong báo cáo này, không đưa đáp án phỏng đoán hoặc đòi dữ liệu ngoài vào kế hoạch.
Câu hỏi ngắn chỉ cần ít query, không bắt buộc dùng hết giới hạn.
```

## Ngân hàng

```text
Lập kế hoạch lấy context từ một BCTC Việt Nam bằng tìm kiếm toàn văn.
Câu hỏi: {{question}}
Báo cáo cố định: {"company_name": "{{company_name}}", "report_type": "{{report_type}}", "report_time": "{{report_time}}", "sector": "Ngân hàng"}
Phân biệt dư nợ cho vay, tiền gửi khách hàng, thu nhập lãi thuần, dự phòng tín dụng và dòng tiền. NIM cần tài sản sinh lãi bình quân; ROA/ROE cần đúng mẫu số.
Trả planner bằng tiếng Việt và 1–6 queries theo schema.
Mỗi query là một cụm tìm kiếm tự đủ nghĩa, gồm tên chỉ tiêu/keyword và kỳ nếu cần.
Phân tách câu hỏi nhiều ý thành các query bổ sung nhau; có thể dùng tên viết tắt
hoặc từ đồng nghĩa tài chính phù hợp, không sinh các biến thể trùng nghĩa vô ích.
Tỷ số cần tìm đủ thành phần; phân biệt số dư cuối kỳ, dồn tích trong kỳ và tiền thực thu/chi.
Có thể tìm cả bảng chính và chi tiết thuyết minh; không cần chọn tên section/subsection.
Chỉ tìm trong báo cáo này, không đưa đáp án phỏng đoán hoặc đòi dữ liệu ngoài vào kế hoạch.
Câu hỏi ngắn chỉ cần ít query, không bắt buộc dùng hết giới hạn.
```

## Chứng khoán

```text
Lập kế hoạch lấy context từ một BCTC Việt Nam bằng tìm kiếm toàn văn.
Câu hỏi: {{question}}
Báo cáo cố định: {"company_name": "{{company_name}}", "report_type": "{{report_type}}", "report_time": "{{report_time}}", "sector": "Chứng khoán"}
Phân biệt lãi/lỗ FVTPL, HTM, AFS, doanh thu môi giới, lãi margin, dư nợ margin, tài sản khách hàng và tài sản công ty; lợi nhuận tự doanh cần cả lãi và lỗ.
Trả planner bằng tiếng Việt và 1–6 queries theo schema.
Mỗi query là một cụm tìm kiếm tự đủ nghĩa, gồm tên chỉ tiêu/keyword và kỳ nếu cần.
Phân tách câu hỏi nhiều ý thành các query bổ sung nhau; có thể dùng tên viết tắt
hoặc từ đồng nghĩa tài chính phù hợp, không sinh các biến thể trùng nghĩa vô ích.
Tỷ số cần tìm đủ thành phần; phân biệt số dư cuối kỳ, dồn tích trong kỳ và tiền thực thu/chi.
Có thể tìm cả bảng chính và chi tiết thuyết minh; không cần chọn tên section/subsection.
Chỉ tìm trong báo cáo này, không đưa đáp án phỏng đoán hoặc đòi dữ liệu ngoài vào kế hoạch.
Câu hỏi ngắn chỉ cần ít query, không bắt buộc dùng hết giới hạn.
```

## Output có cấu trúc

`RAGPlan`: planner và queries (1–6 query).

Nguồn trong repo: `prompts/rag.py`.
