---
language:
- vi
task_categories:
- question-answering
pretty_name: FR-Graph Evaluation — 421 Questions
---
# FR-Graph — Kết quả đánh giá trên 421 câu

**Dataset duy nhất: [02_question_sets/questions_421.jsonl](02_question_sets/questions_421.jsonl).**
Kết quả chính WF2–5 và RAGAS dùng cùng bộ 421 ID này.

| Thư mục | Nội dung |
|---|---|
| `01_source_reports/` | PDF, Markdown báo cáo và danh mục tên file. |
| `02_question_sets/` | Chỉ một dataset 421 câu và README. |
| `03_graph_and_indexes/` | JSON graph và catalog. |
| `04_workflow_results/benchmark_raw_results/` | Kết quả WF2–5 đã lọc theo 421 ID, kèm context, trace, chunk, thời gian, token và input RAGAS. |
| `04_workflow_results/workflow1_hard15_exploratory/` | Lượt thử WF1 trên tập con Hard, tách khỏi bảng so sánh chính. |
| `05_ragas_evaluation/` | Bốn lượt chấm chính, điểm cuối và audit. Mỗi workflow có 421 × 5 điểm thành công. |
| `06_build_and_retrieval_benchmarks/` | Ba nhóm: kiểm tra graph; chi phí chuẩn bị dữ liệu; độ trễ retrieval. Đọc README bên trong. |
| `07_prompts/` | Prompt theo từng lượt gọi LLM, chia bốn thư mục WF2–5; dữ liệu động dùng biến {{tên_dữ_liệu}}. |

Nối dữ liệu theo case_id + workflow. question_number giữ số gốc để truy vết, có
thể không liên tục. MANIFEST.csv ghi SHA-256 và nguồn của từng file. Các bảng đã
lọc được đánh dấu filtered_421_from trong manifest; bằng chứng từng câu giữ nguyên.
Đây là bản xuất theo bộ 421 câu từ kết quả lưu sẵn, không phải lượt chạy mới.
Dữ liệu nguồn/lượt chạy gốc vẫn giữ trong repo làm việc; không dùng bản phát hành
đã lọc để resume. Các path lịch sử bên trong log là provenance. Gói chỉ chứa dữ liệu, kết quả và tài liệu; source code được giữ ngoài gói.

Không có .env chứa khóa API, trọng số model hoặc dữ liệu DB runtime. Thư mục là
bản sao độc lập, không tự đồng bộ với lượt đang chạy. Giấy phép/thông tin nguồn của
các thành phần giữ theo tài liệu gốc; chưa gán một giấy phép chung mới cho toàn bộ.

```bash
zip -r fr_graph_evaluation.zip research_artifacts
```
