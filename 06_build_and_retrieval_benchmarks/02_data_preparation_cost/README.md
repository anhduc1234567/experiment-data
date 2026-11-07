# Chi phí chuẩn bị dữ liệu

graph_build_and_neo4j_ingestion.csv: lượt build + import dùng metadata đã có sẵn.
vector_ingestion.csv: chia chunk, embedding và nhập vector cho full report/nguồn bổ sung.
Hai manifest ghi cấu hình từng lượt. Đo từ Markdown, không gồm PDF/OCR hay trích
metadata bằng LLM. Khi cộng các thành phần khác lượt, ghi là tổng thành phần.
