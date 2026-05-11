# 03 - Bảng đo lường ROI cho AI Adoption

## Tên bài

**AI-Assisted Software Delivery Workflow cho KingModerator / SupportAI**

## Tóm tắt quyết định

| Mục | Nội dung |
|---|---|
| Product / workflow system | AI-Assisted Software Delivery Workflow |
| Dự án áp dụng | KingModerator / SupportAI |
| Người dùng chính | PM/Product Owner, Project Manager, Tech Lead, Dev |
| Vấn đề adoption | Dev dùng AI coding nhanh hơn, nhưng PM-Dev handoff và architecture governance chưa được redesign tương ứng |
| Quyết định | Continue with conditions - tiếp tục có điều kiện |
| Điều kiện scale | Chỉ scale khi cycle time giảm mà PR rework, architecture violation, defect escape và rollback không tăng |

---

# Part A - Adoption Context

## A1. Thách thức chính

Trong dự án KingModerator / SupportAI, Dev có thể dùng AI coding assistant để tăng tốc viết code, tạo test, refactor và phân tích bug. Tuy nhiên, adoption thật không nằm ở việc Dev có dùng AI nhiều hay không. Adoption thật nằm ở việc toàn bộ quy trình delivery có thay đổi để tận dụng AI mà vẫn giữ được chất lượng hay không.

Điểm nghẽn chính là **PM-to-Dev handoff**. Khi Dev dùng AI coding tool, issue/spec của PM trở thành đầu vào cho cả Dev và AI. Nếu issue/spec thiếu context, acceptance criteria, non-goals, architecture constraint hoặc test expectation, AI có thể tạo code rất nhanh nhưng lệch product intent.

## A2. Phạm vi sản phẩm

| Trường | Nội dung |
|---|---|
| Tên hệ thống | AI-Assisted Software Delivery Workflow |
| Dự án | KingModerator / SupportAI |
| Phạm vi | Quy trình từ PM issue/spec đến Dev planning, AI-assisted coding và PR review |
| Không nằm trong phạm vi | Đo adoption của end-user ngoài sản phẩm, đo số prompt cá nhân của Dev, ranking người dùng AI |
| Kết quả cần tạo | Delivery nhanh hơn, issue rõ hơn, ít rework hơn, kiến trúc ổn định hơn, squad ownership rõ hơn |

## A3. Người dùng và vai trò

| Vai trò | Trách nhiệm trong workflow |
|---|---|
| PM/Product Owner | Xác định product intent, acceptance criteria, non-goals và business priority |
| Project Manager | Điều phối sprint, theo dõi blocker, đảm bảo story đi đúng workflow |
| Tech Lead | Kiểm soát kiến trúc, review plan, review PR có rủi ro cao |
| Dev | Dùng AI coding assistant có kiểm soát, viết code/test, tự review output trước khi PR |
| AI coding assistant | Hỗ trợ tách task, gợi ý code, viết test, tóm tắt PR và phát hiện rủi ro ban đầu |

## A4. Core workflows

| # | Quy trình | AI làm gì? | Người kiểm ở đâu? | Failure path |
|---:|---|---|---|---|
| 1 | PM issue/spec → AI-readable delivery brief | AI hỗ trợ rà soát issue: thiếu context, thiếu AC, thiếu constraint, thiếu test expectation | PM review final issue; Tech Lead review phần technical constraint nếu story có rủi ro kiến trúc | Nếu issue thiếu thông tin, chuyển trạng thái `Needs clarification`, chưa cho Dev bắt đầu code |
| 2 | Dev planning → AI-assisted implementation plan | AI giúp Dev tách task, đề xuất file/module cần sửa, test plan và risk area | Dev tự kiểm tra; Tech Lead duyệt plan với story medium/high complexity | Nếu plan chạm vùng kiến trúc nhạy cảm, bắt buộc Tech Lead approve trước khi code |
| 3 | AI-assisted coding → PR + architecture review | AI hỗ trợ code, test generation, PR summary và risk checklist | Dev review code/test; Tech Lead review kiến trúc; CI/local test kiểm tra | Nếu PR vi phạm architecture guardrail hoặc test fail, block merge và log root cause |

## A5. ADKAR barrier chính

| Stage | Chẩn đoán |
|---|---|
| Awareness | Team biết AI coding có thể giúp tăng tốc |
| Desire | Dev có động lực dùng AI, nhưng có thể lo bị giám sát nếu metric sai |
| Knowledge | Cần chuẩn hóa cách viết AI-readable issue và cách kiểm output AI |
| Ability | Rào cản chính: team chưa có workflow đủ cụ thể để dùng AI trong delivery thật |
| Reinforcement | Rào cản thứ hai: chưa có dashboard và ritual để duy trì hành vi đúng |

**Kết luận:** Rào cản chính là **Ability + Reinforcement**.

## A6. Tactics được chọn

| Tactic | Mục tiêu | Cách triển khai trong dự án |
|---|---|---|
| Explain the how | Giải thích cụ thể AI thay đổi workflow thế nào | Tạo template issue/spec có context, goal, AC, non-goals, constraint, test expectation |
| Track team-specific impact | Đo outcome theo team/squad, không ranking cá nhân | Đo cycle time, rework, architecture violation và defect escape theo squad |
| Turn enthusiasts into teachers | Biến người dùng AI tốt thành người hướng dẫn | Tech Lead/AI champion review issue mẫu, plan mẫu và PR mẫu mỗi tuần |
| Prioritize high-impact tasks | Không áp dụng quá rộng ngay từ đầu | Pilot với story medium/high complexity hoặc vùng code có rủi ro kiến trúc cao |

---

# Part B - Root Cause Diagnosis

## B1. Lens chẩn đoán

| Lens | Phát hiện |
|---|---|
| Workflow | AI đang được thêm vào bước coding, nhưng PM issue/spec và PR review chưa được redesign tương ứng |
| Metrics | Các chỉ số dễ đo như prompt count, số commit, số PR có thể tạo cảm giác adoption giả |
| Trust / Quality | AI output cần được kiểm bằng test, PR review, architecture guardrail và rollback tracking |
| Readiness / Absorption | Cần owner rõ cho issue quality, review quality, architecture quality và dashboard cadence |

## B2. Nguyên nhân gốc

| Nguyên nhân gốc | Bằng chứng | Tác động nếu không xử lý |
|---|---|---|
| PM issue/spec chưa đủ chuẩn cho AI-readable handoff | PM phải mô tả việc theo kiểu prompt để Dev và AI hiểu được, nhưng chưa có checklist bắt buộc | Dev và AI hiểu sai intent, tăng clarification loop và rework |
| Architecture governance không theo kịp tốc độ AI-assisted coding | AI giúp tạo code nhanh, nhưng review kiến trúc vẫn bị dồn về cuối PR | Architecture drift, duplicate logic, technical debt |
| Squad ownership chưa rõ | Nhiều người có thể chạm cùng domain hoặc module | Cross-squad conflict, khó quy trách nhiệm, review bottleneck |
| Metric dễ bị lệch | Dễ đo usage hơn đo quality/value | Team có thể tối ưu số prompt, số PR, số commit thay vì outcome thật |

## B3. Bài học từ case comparison

| Case | Bài học áp dụng |
|---|---|
| DWP / GDS | Muốn nói ROI phải có baseline, comparison hoặc ít nhất nhiều nguồn dữ liệu vận hành khớp nhau |
| JPMorgan dashboard | Không nên đo adoption bằng usage cá nhân hoặc ranking kỹ sư; dễ làm sai động lực và giảm trust |

## B4. Chẩn đoán tóm tắt

> Vấn đề không phải Dev chưa dùng AI. Vấn đề là quy trình PM-Dev-AI chưa có đủ handoff, guardrail, owner và metric để đảm bảo AI tạo ra delivery nhanh hơn nhưng vẫn đúng intent và ổn định về kiến trúc.

---

# Part C - Giải pháp và lộ trình 30/60/90 ngày

## C1. Giải pháp tổng thể

Thiết kế lại delivery workflow theo hướng **Centaur**: AI hỗ trợ các bước draft, phân tích, coding và test, nhưng các điểm cần judgment vẫn do con người quyết định.

| Phần cần đổi | Thay đổi đề xuất |
|---|---|
| PM issue/spec | Chuẩn hóa AI-readable issue template |
| Dev planning | Bắt buộc implementation plan cho story medium/high complexity |
| Coding | Dev dùng AI nhưng phải tự review output trước PR |
| PR review | Thêm architecture guardrail checklist |
| Squad ownership | Mỗi domain/module có squad hoặc owner rõ |
| Dashboard | Đo workflow outcome, không đo prompt count cá nhân |

## C2. Roadmap 30/60/90 ngày

| Giai đoạn | Việc cần làm | Owner | Dấu hiệu hoàn thành |
|---|---|---|---|
| 0-30 ngày | Chốt AI-readable issue template gồm context, goal, AC, non-goals, constraint, test expectation | PM/Product Owner | 100% story pilot dùng template |
| 0-30 ngày | Tạo architecture guardrail checklist cho PR | Tech Lead | Checklist được dùng trong PR medium/high impact |
| 0-30 ngày | Lấy baseline 2 sprint: cycle time, PR rework, defect escape, clarification loops | Project Manager | Baseline report có đủ số liệu |
| 31-60 ngày | Pilot workflow với 1-2 squad hoặc 1 nhóm feature có rủi ro rõ | Project Manager + Tech Lead | ≥60% story pilot đi đủ workflow |
| 31-60 ngày | Review dashboard hàng tuần trong sprint review/retro | Project Manager | Có action khi metric đỏ |
| 31-60 ngày | Tổ chức show-and-tell: issue tốt, plan tốt, PR tốt | Tech Lead / AI champion | Có ít nhất 2 buổi chia sẻ thực hành |
| 61-90 ngày | So sánh story theo workflow mới với baseline cũ | PM + Project Manager | Báo cáo ROI 90 ngày hoàn thành |
| 61-90 ngày | Cập nhật operating model: squad owner, review owner, escalation path | PM + Tech Lead | Workflow trở thành default trong sprint planning |
| 61-90 ngày | Quyết định continue / pivot / pause / kill theo ngưỡng | PM/Product Owner | Có decision memo cuối pilot |

---

# Part D - Product ROI Dashboard v2

## D1. Product-level metrics

| Layer | Chỉ số | Baseline | Target 90 ngày | Nguồn dữ liệu | Owner | Rủi ro phản biện | Fix v2 |
|---|---|---:|---:|---|---|---|---|
| Activation | % story mới dùng AI-readable issue template | 0% trước template | ≥85% | Audit issue template | PM/Product Owner | PM có thể điền hình thức | Thêm issue clarity rubric và rating từ Dev |
| Engagement | % story trong sprint đi đủ PM brief → Dev plan → PR review | TBD từ tuần 1 | ≥70% | Issue board + PR checklist | Project Manager | Quy trình có thể thành bureaucracy | Chỉ bắt buộc full flow cho story medium/high complexity |
| Productivity | Median cycle time từ issue ready → PR merged | Baseline 2 sprint gần nhất | Giảm 20% | GitHub PR timestamps | Project Manager | Nhanh hơn có thể che chất lượng kém | Ghép với rework, test và defect metric |
| Quality | % PR qua review không cần major rework | Baseline 2 sprint gần nhất | ≥80% | PR comments + labels | Tech Lead | Major rework có thể chủ quan | Định nghĩa major rework là sửa lại kiến trúc/API/logic chính |
| Trust | % AI-assisted PR merge không rollback kiến trúc trong 2 tuần | Baseline từ pilot | ≥90% | GitHub PR + rollback log | Tech Lead | Rollback có thể không được log | Bắt buộc dùng rollback label và review hàng tuần |
| Value | Cycle time giảm nhưng defect escape không tăng | Baseline 2 sprint gần nhất | Cycle time -20%, defect escape ≤ baseline | GitHub + bug log | PM + Tech Lead | Attribution cho AI có thể yếu | So sánh story đi đúng workflow với story chưa đi workflow |

## D2. Workflow-level metrics

| Quy trình | Layer | Chỉ số | Baseline | Target 90 ngày | Nguồn dữ liệu | Owner | Rủi ro phản biện | Fix v2 |
|---|---|---|---:|---:|---|---|---|---|
| PM issue/spec | Quality | Issue clarity score: context, goal, AC, non-goals, constraint, test | Chưa có rubric | Trung bình ≥4/5 | Rating nhanh của Dev + PM checklist | PM | Dev có thể ngại chấm thấp | Dùng rating ẩn danh ngắn + audit mẫu |
| PM issue/spec | Productivity | Số clarification loop trước khi Dev bắt đầu | TBD | ≤1 loop/story | Comment trong issue / trạng thái issue | Project Manager | Story phức tạp cần hỏi nhiều hơn | Segment theo độ phức tạp |
| Dev planning | Quality | % implementation plan được duyệt không cần viết lại lớn | Chưa bắt buộc | ≥75% | Planning note / PR description | Tech Lead | Dev có thể bỏ qua plan | Chỉ bắt buộc với thay đổi API/DB/architecture-sensitive |
| Dev planning | Trust | % plan có liệt kê risk area rõ | Chưa bắt buộc | ≥80% | PR template | Tech Lead | Checklist theater | Tech Lead audit mẫu hàng tuần |
| AI-assisted coding | Productivity | Thời gian từ plan approved → PR ready | TBD | Giảm 25% | GitHub timestamps | Dev | Speed có thể làm giảm test | Ghép với CI/local test pass rate |
| AI-assisted coding | Quality | First-pass CI/test success rate | Baseline hiện tại | ≥90% | CI log / local test record | Dev + Tech Lead | Chưa có CI đầy đủ | Bắt đầu bằng documented local test, sau đó bổ sung CI |
| PR review | Quality | Architecture guardrail violation rate | TBD | ≤10% | PR review labels | Tech Lead | Định nghĩa chưa rõ | Dùng checklist guardrail cố định |
| PR review | Trust | % AI-assisted PR không cần major architecture rework | TBD | ≥85% | PR comments | Tech Lead | Review burden tăng | Chỉ áp dụng với PR medium/high impact |
| Squad governance | Engagement | % story có squad/code owner trước khi implement | Một phần | ≥90% | Sprint board + ownership map | Project Manager | Owner chỉ trên danh nghĩa | Owner phải approve plan cho domain của mình |
| Squad governance | Value | Cross-squad conflict / duplicate work rate | TBD | ≤5% story/sprint | Retro notes + PR conflict | Project Manager | Khó đo | Chỉ track conflict gây blocker hoặc rework |

---

# Part E - Dashboard Mock

```text
┌────────────────────────────────────────────────────────────────────┐
│ KingModerator / SupportAI - AI Delivery Dashboard v2                │
├──────────────────────────────┬─────────────────────────────────────┤
│ Product Health               │ 72% story đi đủ workflow             │
│ Decision                     │ Continue with conditions             │
├──────────────────────────────┼─────────────────────────────────────┤
│ PM Issue Quality             │ 4.1 / 5 clarity score                 │
│ Clarification Loops          │ 0.9 loop / issue                      │
├──────────────────────────────┼─────────────────────────────────────┤
│ Dev Planning Quality         │ 76% plan không cần viết lại lớn       │
│ Risk Areas Listed            │ 82% story nhạy cảm có risk area       │
├──────────────────────────────┼─────────────────────────────────────┤
│ Delivery Productivity        │ Cycle time giảm 18%                   │
│ Guardrail                    │ Chỉ continue nếu quality ổn định      │
├──────────────────────────────┼─────────────────────────────────────┤
│ Architecture Control         │ 8% PR vi phạm guardrail kiến trúc      │
│ PR Rework                    │ 14% PR cần major rework                │
├──────────────────────────────┼─────────────────────────────────────┤
│ Trust / Value                │ 89% PR không rollback sau 2 tuần       │
│ Scale Gate                   │ Scale khi ≥90% trong 3 sprint liên tục │
└──────────────────────────────┴─────────────────────────────────────┘
```

---

# Part F - Phản biện và sửa từ v1 sang v2

## F1. Bảng phản biện

| Vai phản biện | Câu hỏi phản biện | Rủi ro trong v1 | Sửa trong v2 |
|---|---|---|---|
| CFO | Active AI usage không phải ROI. Giá trị nằm ở đâu? | v1 có thể đếm prompt và số PR | Đổi sang cycle time reduction đi kèm defect escape và rework |
| User / Dev | Metric này có ép Dev dùng AI hoặc phạt người dùng ít không? | Individual leaderboard có thể làm giảm trust | Đo outcome cấp workflow/squad, không đo prompt count cá nhân |
| Risk / Legal | Nếu AI code sai kiến trúc hoặc tạo lỗ hổng thì sao? | v1 tách chưa rõ speed và quality | Thêm architecture violation, rollback, CI/test pass rate |
| Workflow Owner | Ai lấy dữ liệu và ai xử lý khi metric đỏ? | Owner trong v1 còn mơ hồ | Gán owner cụ thể: PM, Project Manager, Tech Lead, Dev |
| Tech Lead | Issue template có thể thành checkbox theater không? | Template compliance có thể hình thức | Thêm Dev clarity rating và sample audit |
| PM | Quy trình mới có làm delivery chậm hơn không? | Workflow có thể quá nặng | Chỉ áp dụng full flow cho story medium/high complexity |

## F2. Sửa cụ thể từ v1 sang v2

| Vấn đề ở v1 | Vì sao yếu | Sửa ở v2 |
|---|---|---|
| Dùng `number of AI prompts/dev/week` | Dễ bị chạy số, tạo áp lực cá nhân | Thay bằng `% AI-assisted PR không cần major architecture rework` |
| Dùng `number of PRs merged` | Throughput không chứng minh quality | Ghép cycle time với PR rework, test pass và defect escape |
| Owner ghi chung là “team” | Không ai chịu trách nhiệm thật | Gán owner theo metric: PM, Project Manager, Tech Lead, Dev |
| Scale toàn bộ team ngay | Rủi ro process nặng và dữ liệu nhiễu | Pilot 1-2 squad hoặc story medium/high complexity trước |
| Chỉ có template issue | Có thể điền cho đủ form | Thêm clarity score từ Dev và audit mẫu hàng tuần |

---

# Part G - Decision Memo

## 1. Quyết định

**Continue with conditions.**

Tiếp tục triển khai AI-assisted delivery workflow cho KingModerator / SupportAI, nhưng chưa scale toàn bộ ngay. Nên pilot trong 1-2 squad hoặc trong nhóm story medium/high complexity trước.

## 2. Metric mạnh nhất để bảo vệ quyết định

Metric mạnh nhất là:

> **% AI-assisted PR được merge mà không cần major architecture rework hoặc rollback trong 2 tuần.**

Chỉ số này tốt hơn prompt count vì nó nối AI usage với outcome thật: code có qua review không, có giữ kiến trúc không, có sống ổn sau khi merge không.

## 3. Metric hoặc giả định đã sửa sau phản biện

Metric cần sửa là **số prompt hoặc số lần Dev dùng AI**. Đây là vanity metric và có thể làm sai hành vi. Sau phản biện, metric được thay bằng nhóm chỉ số outcome:

| Nhóm | Chỉ số thay thế |
|---|---|
| Productivity | Cycle time từ issue ready đến PR merged |
| Quality | PR rework rate, test pass rate, architecture violation rate |
| Trust | PR không rollback sau 2 tuần |
| Value | Cycle time giảm nhưng defect escape không tăng |

## 4. Trước khi scale cần làm gì?

| Việc cần làm | Owner | Lý do |
|---|---|---|
| Chốt AI-readable issue template | PM/Product Owner | Đảm bảo PM handoff đủ rõ cho Dev và AI |
| Chốt architecture guardrail checklist | Tech Lead | Ngăn AI-assisted coding làm lệch kiến trúc |
| Lấy baseline 2 sprint | Project Manager | Có dữ liệu để so sánh ROI |
| Chia squad/code ownership rõ | PM + Tech Lead | Giảm cross-squad conflict và review bottleneck |
| Review dashboard hàng tuần | Project Manager | Biến số liệu thành hành động, không chỉ trang trí |

## 5. Decision rule

| Kết quả sau pilot | Quyết định |
|---|---|
| Cycle time giảm ≥20%, PR rework không tăng, defect escape không tăng, architecture violation ≤10% | Continue và mở rộng sang squad tiếp theo |
| Activation cao nhưng clarity score thấp hoặc clarification loop cao | Pivot sang training PM issue/spec và template coaching |
| Cycle time giảm nhưng defect escape hoặc architecture violation tăng | Pause scale, sửa guardrail và review process |
| PR rollback hoặc architecture violation vượt ngưỡng trong 2 sprint liên tiếp | Kill hoặc thu hẹp phạm vi dùng AI trong phần coding nhạy cảm |

## 6. Kết luận

AI có thể làm tăng tốc development, nhưng nếu workflow không đổi thì AI cũng có thể tăng tốc sai lệch. Với KingModerator / SupportAI, adoption thật không phải là Dev dùng AI nhiều hơn. Adoption thật là khi PM, Dev, Tech Lead và AI cùng nằm trong một workflow có handoff rõ, review rõ, owner rõ, failure path rõ và metric đo được value thật.
