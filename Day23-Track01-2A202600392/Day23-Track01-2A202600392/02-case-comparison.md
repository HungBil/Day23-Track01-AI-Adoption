# 02 - So sánh tình huống thành công và tình huống cảnh báo

## 1. Cặp tình huống được chọn

| Loại | Tình huống |
|---|---|
| Thành công / tín hiệu tốt | DWP / GDS Copilot measurement |
| Thất bại / cảnh báo | JPMorgan AI usage dashboard |

## 2. Lý do chọn hai tình huống này

Bài lab tập trung vào adoption trong quy trình phát triển phần mềm: PM viết issue/spec, Dev dùng AI coding tool, Tech Lead kiểm soát kiến trúc và nhóm đo chất lượng delivery.

Vì vậy, hai tình huống phù hợp nhất là:

1. **DWP / GDS**: cho thấy phương pháp đo rất quan trọng. Self-report về thời gian tiết kiệm yếu hơn baseline, comparison group và đánh giá nhiều nguồn dữ liệu.
2. **JPMorgan AI usage dashboard**: cho thấy dashboard đo usage của kỹ sư có thể phản tác dụng nếu tạo cảm giác bị xếp hạng hoặc khuyến khích hoạt động thay vì outcome.

## 3. Bảng so sánh chính

| Tiêu chí | DWP / GDS - tín hiệu tốt | JPMorgan AI usage dashboard - cảnh báo |
|---|---|---|
| Domain | Public sector productivity | Engineering productivity / AI coding tools |
| Quy trình có AI | Nhân sự dùng Copilot-style tools trong công việc năng suất | Kỹ sư dùng Copilot, Claude hoặc công cụ AI coding trong development |
| Người dùng chính | Civil servants / government employees | Software engineers, engineering managers |
| Chỉ số chính | Time saved và productivity signals, có cố gắng đo bằng phương pháp chặt hơn | Usage buckets, heavy/light usage, ranking hoặc so sánh giữa team/cá nhân |
| Layer metric | Productivity + measurement methodology | Activation / Engagement nhưng dễ thành vanity metric |
| Metric chứng minh được gì? | Có thể chứng minh AI có tín hiệu tiết kiệm thời gian nếu đo có baseline và comparison | Có thể chứng minh ai đang dùng AI nhiều hay ít |
| Metric chưa chứng minh được gì? | Time saved không tự động trở thành cost saving, quality improvement hoặc service outcome | Usage cao không chứng minh code tốt hơn, delivery nhanh hơn hay ít lỗi hơn |
| Missing metric | Quality, error rate, rework rate, trust, downstream outcome | PR rework, architecture violation, defect escape, cycle time, developer sentiment |
| Rủi ro nếu copy máy móc | Overclaim ROI từ self-report | Tạo áp lực xếp hạng, làm giảm Desire trong ADKAR, khuyến khích chạy số usage |
| Bài học chính | ROI cần phương pháp đo đáng tin | Không đo adoption bằng bảng xếp hạng số lần dùng AI |

## 4. Phân tích tình huống DWP / GDS

| Trường | Phân tích |
|---|---|
| Workflow | Nhân sự dùng công cụ AI kiểu Copilot để hỗ trợ công việc tri thức |
| Chỉ số | Time saved, productivity signal, so sánh với baseline hoặc nhóm đối chứng |
| Chứng minh được | Nếu phương pháp đo đủ tốt, có thể nói AI giúp giảm thời gian làm việc ở một số tác vụ |
| Chưa chứng minh được | Chưa chắc thời gian tiết kiệm chuyển thành chi phí tiết kiệm, chất lượng tốt hơn hoặc citizen outcome tốt hơn |
| Chỉ số còn thiếu | Output quality, rework, error rate, trust, business/citizen outcome |

### Bài học cho dashboard của tôi

Không nên chỉ hỏi Dev: “AI có giúp tiết kiệm thời gian không?”. Cần đo bằng dữ liệu vận hành:

| Nhóm dữ liệu | Ví dụ chỉ số |
|---|---|
| Issue data | Clarification loops, issue clarity score |
| PR data | Cycle time, PR rework rate, review comments |
| Quality data | Test pass rate, defect escape, rollback |
| Architecture data | Architecture guardrail violation rate |

Bài học là: **ROI cần measurement discipline, không chỉ cần cảm nhận tích cực.**

## 5. Phân tích tình huống JPMorgan AI usage dashboard

| Trường | Phân tích |
|---|---|
| Workflow | Kỹ sư dùng AI coding tools trong development workflow |
| Chỉ số | Usage level, heavy/light usage, proactive/passive usage, team comparison |
| Chứng minh được | Cho biết adoption activity và mức độ sử dụng tool |
| Chưa chứng minh được | Không chứng minh productivity thật, code quality, architecture quality hoặc developer experience |
| Chỉ số còn thiếu | Cycle time, PR rework, defect escape, architecture violation, code review quality, developer trust |

### Bài học cho dashboard của tôi

Không nên tạo dashboard kiểu “Dev nào dùng AI nhiều nhất”. Cách đó dễ làm mọi người dùng AI để có số, hoặc sợ bị đánh giá nếu dùng ít. Với dự án KingModerator / SupportAI, dashboard nên đo ở cấp **quy trình và squad**, không đo theo ranking cá nhân.

## 6. Bài học áp dụng cho KingModerator / SupportAI

| Nguyên tắc | Cách áp dụng |
|---|---|
| Không dừng ở usage | Không dùng số prompt, số dòng code hoặc số lần mở AI tool làm metric chính |
| Ghép productivity với quality | Cycle time giảm chỉ được xem là tốt nếu PR rework, defect escape và architecture violation không tăng |
| Đo ở cấp workflow/squad | Theo dõi story có đi đủ PM brief → Dev plan → PR review không |
| Tránh tạo áp lực sai | Không ranking Dev theo usage cá nhân |
| Có decision rule | Continue, Pivot, Pause hoặc Kill dựa trên ngưỡng rõ ràng |

## 7. Kết luận cho dashboard

> DWP / GDS dạy rằng ROI phải được đo bằng phương pháp đáng tin. JPMorgan cảnh báo rằng dashboard đo usage cá nhân có thể làm sai hành vi người dùng.

Vì vậy, dashboard của tôi sẽ không hỏi “Dev dùng AI bao nhiêu?”. Dashboard sẽ hỏi:

1. Issue của PM có đủ rõ để Dev và AI hiểu đúng không?
2. Dev plan có được Tech Lead duyệt mà không phải viết lại nhiều không?
3. AI-assisted PR có giảm cycle time không?
4. PR có giữ được chất lượng test và kiến trúc không?
5. Team có thể scale quy trình này mà không tăng rework hoặc defect không?
