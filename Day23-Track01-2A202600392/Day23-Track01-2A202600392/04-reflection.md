# 04 - Reflection cá nhân

Một chỉ số tôi sẽ sửa sau bài học Day 23 là **số lần dùng AI hoặc số prompt của từng Dev**. Trước đây, chỉ số này nhìn có vẻ hợp lý vì nó cho thấy team có đang dùng AI hay không. Tuy nhiên, sau khi làm ROI Dashboard, tôi thấy đây là một vanity metric rất dễ gây sai lệch. Một Dev dùng AI nhiều chưa chắc tạo ra code tốt hơn. Nếu chỉ số này bị biến thành mục tiêu, mọi người có thể prompt nhiều hơn để “có số”, trong khi chất lượng code, kiến trúc và test không cải thiện.

Tôi sẽ thay chỉ số đó bằng **% AI-assisted PR được merge mà không cần major architecture rework hoặc rollback trong 2 tuần**. Chỉ số này tốt hơn vì nó nối AI usage với kết quả thật: code có đúng intent không, có maintainable không, có vượt review không và có ổn định sau khi merge không. Với dự án KingModerator / SupportAI, điều quan trọng không phải là Dev dùng AI nhiều, mà là quy trình PM-Dev-AI giúp team ship nhanh hơn mà không làm codebase khó kiểm soát hơn.
