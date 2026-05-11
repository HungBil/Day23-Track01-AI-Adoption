# 01 - Quét thách thức cá nhân và ma trận bằng chứng

## 1. Tình huống adoption bị kẹt

Trong dự án đang làm, Dev có thể dùng các công cụ AI như Cursor, Claude Code, GitHub Copilot hoặc ChatGPT để tăng tốc viết code, refactor, viết test và phân tích lỗi. Tuy nhiên, việc Dev dùng AI tốt hơn không tự động đồng nghĩa với việc cả quy trình phát triển sản phẩm đã adopt AI đúng cách.

Điểm nghẽn chính nằm ở bước **PM giao việc cho Dev**. Khi Dev dùng AI coding assistant, issue/spec của PM không còn chỉ là mô tả công việc cho người đọc. Nó trở thành **đầu vào cho cả Dev và AI của Dev**. Nếu issue thiếu bối cảnh, thiếu acceptance criteria, thiếu non-goals hoặc thiếu ràng buộc kiến trúc, AI có thể code rất nhanh nhưng đi sai hướng.

### Ghi chú cá nhân ban đầu

> PM khi giao việc cho Dev trong team cần mô tả theo kiểu prompt để Dev và AI của Dev đọc được. Nếu chỉ dùng AI để generate issue mà không có judgment của PM, team có thể bị khóa công nghệ hoặc bị định hướng sai theo prompt issue ban đầu. Do tốc độ phát triển nhanh nên khó kiểm soát codebase về mặt kiến trúc. Vì vậy, cần kinh nghiệm điều phối của Product Management và Project Management, đồng thời cần chia thành các squad team để giữ ownership rõ hơn.

## 2. Challenge statement

> Làm sao để AI coding giúp team giao feature nhanh hơn, nhưng không làm tăng rework, architecture drift, lỗi test hoặc tình trạng code lệch product intent?

Đây là vấn đề adoption ở cấp **quy trình làm việc**, không chỉ là vấn đề công nghệ. Nếu chỉ mua tool hoặc khuyến khích Dev dùng AI nhiều hơn, nhóm có thể đạt usage nhưng chưa đạt adoption thật.

## 3. Dấu hiệu quan sát được

| Dấu hiệu | Quan sát | Vì sao quan trọng |
|---|---|---|
| Issue/spec chưa đủ chuẩn cho AI-assisted development | PM mô tả việc bằng ngôn ngữ tự nhiên, nhưng chưa có checklist bắt buộc về context, acceptance criteria, non-goals, constraint và test expectation | Dev và AI có thể hiểu sai intent |
| AI tạo code nhanh nhưng khó kiểm soát kiến trúc | Tốc độ implementation tăng, nhiều thay đổi được tạo nhanh hơn | Codebase dễ bị architecture drift, duplicate logic hoặc lệch module boundary |
| Review bị dồn về cuối PR | Rủi ro kiến trúc hoặc API contract thường chỉ lộ ra khi PR đã lớn | Chi phí sửa cao và làm chậm delivery |
| Squad ownership chưa rõ | Nhiều người có thể sửa cùng vùng code hoặc cùng logic nghiệp vụ | Khó quy trách nhiệm, khó review và khó duy trì consistency |
| Chỉ số đo dễ bị sai | Nếu chỉ đo số prompt, số PR hoặc số dòng code, dashboard có thể báo tốt trong khi chất lượng giảm | Dễ rơi vào vanity metric |

## 4. Adoption threshold hiện tại

| Ngưỡng | Trạng thái của dự án |
|---|---|
| Usage | Dev đã dùng AI coding tool để code, refactor, viết test hoặc brainstorm |
| Pilot | Một số task có thể hoàn thành nhanh hơn nhờ AI |
| Deployment | Tool và repo đã phục vụ phát triển thực tế |
| Adoption | Chưa đạt đầy đủ vì PM issue, Dev plan, PR review và architecture guardrail chưa thành quy trình chuẩn |
| Normalization | Chưa đạt vì AI-assisted delivery chưa trở thành cách làm mặc định có checklist, owner, chỉ số và decision rule |

**Kết luận:** Dự án đang ở giữa **Usage/Pilot** và **Adoption**. Muốn lên adoption thật, nhóm phải thay đổi quy trình PM-Dev-AI chứ không chỉ tăng số lần dùng AI.

## 5. Lens chẩn đoán

| Lens | Câu hỏi chẩn đoán | Áp dụng vào dự án |
|---|---|---|
| Workflow | Công việc thật có đổi không, hay chỉ thêm AI vào bên ngoài? | AI đang mạnh ở bước coding, nhưng upstream PM issue/spec và downstream architecture review chưa đổi đủ |
| ADKAR | Người dùng đang kẹt ở Awareness, Desire, Knowledge, Ability hay Reinforcement? | Kẹt chính ở Ability và Reinforcement: mọi người biết AI hữu ích nhưng chưa có chuẩn vận hành để dùng đúng trong workflow thật |
| Readiness | Dữ liệu, quyền truy cập, governance và owner đã sẵn sàng chưa? | Có thể lấy dữ liệu từ GitHub/issue/PR/test, nhưng issue template, review checklist và squad owner chưa chuẩn hóa |
| Metrics | Team đang đo usage hay đo value thật? | Dễ đo số prompt, số PR, số commit; cần đo thêm rework, architecture violation và defect escape |
| Trust / Quality | Người dùng có tin output không? Khi AI sai thì xử lý thế nào? | Cần điểm human review rõ: PM review intent, Tech Lead review kiến trúc, Dev review code/test |

## 6. Ma trận bằng chứng

| Bằng chứng / quan sát | Diễn giải adoption | Rủi ro | Dashboard cần đo gì |
|---|---|---|---|
| Issue/spec của PM là đầu vào cho Dev và AI coding assistant | PM handoff trở thành lớp prompt của delivery system | Prompt/spec mơ hồ làm AI code sai hướng | Issue clarity score, clarification loops |
| Tốc độ phát triển nhanh làm khó kiểm soát kiến trúc | AI tăng throughput nhưng governance chưa chắc theo kịp | Architecture drift, tech debt, duplicate logic | Architecture guardrail violation rate |
| Team cần chia squad | Ownership chưa đủ rõ khi nhiều feature chạy song song | Cross-squad conflict, review bottleneck | Squad ownership coverage, blocked handoff rate |
| Dev dùng AI coding để tăng tốc | Có tín hiệu productivity | Productivity có thể tăng cùng rework hoặc bug | Cycle time đi kèm PR rework và defect escape |
| PM không thể chỉ AI-generate issue rồi giao thẳng | Human judgment vẫn phải giữ ở product intent và prioritization | Over-delegation cho AI | Human review completion rate |

## 7. Product được chọn cho ROI Dashboard

| Mục | Nội dung |
|---|---|
| Product / workflow system | AI-Assisted Software Delivery Workflow cho KingModerator / SupportAI |
| Bối cảnh | Phát triển nền tảng hỗ trợ điều phối và kiểm duyệt cộng đồng học tập |
| Người dùng chính | PM/Product Owner, Project Manager, Tech Lead, Dev |
| AI liên quan | AI coding assistant, AI hỗ trợ rà soát issue, AI tóm tắt PR, AI hỗ trợ test |
| Adoption challenge | AI coding tăng tốc delivery nhưng có thể khuếch đại handoff mơ hồ và architecture drift |
| Kết quả mong muốn | Giao feature nhanh hơn, kiến trúc ổn định hơn, ít rework hơn, owner rõ hơn và chất lượng đo được |

## 8. Chỉ số cần tránh

| Chỉ số yếu | Vì sao chưa đủ |
|---|---|
| Số prompt mỗi Dev | Dễ bị chạy số, không chứng minh code tốt hơn |
| Số commit do AI hỗ trợ | Nhiều commit có thể chỉ là fragmentation |
| Số dòng code tạo ra | Nhiều code có thể làm tăng tech debt |
| Số PR được merge | Throughput không tự chứng minh quality |
| Số người dùng AI tool | Usage không chứng minh workflow adoption |

## 9. Chỉ số tốt hơn cho dashboard

| Layer | Chỉ số đề xuất | Vì sao cần đo |
|---|---|---|
| Activation | % story dùng AI-readable issue template | Cho biết workflow có bắt đầu đúng cách không |
| Engagement | % story đi đủ luồng PM brief → Dev plan → PR review | Cho biết hành vi mới có lặp lại trong sprint không |
| Productivity | Median cycle time từ issue ready đến PR merged | Đo tốc độ delivery |
| Quality | PR rework rate, test pass rate, architecture violation rate | Ngăn việc tốc độ che mất rủi ro chất lượng |
| Trust | % AI-assisted PR được merge mà không cần rollback kiến trúc trong 2 tuần | Đo khả năng tin cậy sau khi merge |
| Value | Cycle time giảm trong khi defect escape không tăng | Nối AI usage với giá trị dự án |

## 10. Bài học cá nhân

> AI adoption trong software delivery không phải là Dev có dùng AI tool hay không. Adoption thật xảy ra khi quy trình PM-Dev-AI tạo ra code nhanh hơn, đúng intent hơn, dễ maintain hơn và ít rủi ro hơn.

Vì vậy, ROI Dashboard không nên thưởng cho “dùng AI nhiều hơn”. Dashboard phải thưởng cho **handoff rõ hơn, planning tốt hơn, cycle time thấp hơn, rework ít hơn, kiến trúc ổn định hơn và khả năng scale an toàn hơn**.
