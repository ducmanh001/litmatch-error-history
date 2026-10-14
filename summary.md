# Error history summary

id: summary
span: 10/07/2026 → 09/10/2026 (3 tháng); tạo 14/10/2026 08:11 (+07); repo ducmanh001/litmatch @ d3cb28c
rows: 108 (102 vấn đề thật, 6 báo động giả); raw records extracted: 130

Loại A = lỗi / sự cố thực tế; B = thiết kế, quy trình, quan sát từ đọc code; C = báo động giả.

## Counts

- by status: fixed 78, open 15, mitigated 8, false-alarm 6, in-progress 1
- by tier: A 66, B 36, C 6
- by area: ci-cd 24, ai-agent-process 13, auth-security 12, frontend-ux 9, windows-toolchain 8, deploy-config 7, other 7, matching 6, database-concurrency 5, observability 4, economy-payment 3, realtime-gateway 3, short-video 3, dependencies 2, docs-tooling 2

## GitHub Actions

360 runs, 132 red (human 286/81, dependabot 74/51, bot 141/94; main 127/26). Peak 32 runs on 13/07; last human red 14/08. Per month: 2026-07 74/219, 2026-08 7/64, 2026-10 0/3.

Failing steps: Frontend: contract, test, build, bundle audit (16); gitleaks quét lịch sử Git tìm secret (15); ESLint (nx run-many lint) (12); Preflight test + build (tương đương local) (9); Preflight chất lượng (format/lint) (7); Trivy: lỗ hổng/misconfig trong repo (6); Audit dependency mức high/critical (4); Trivy: quét runtime image (4).

Lấy bằng gh từ 501 run (11/07 đến 09/10). Số đỏ lấy từ API (job và step), không đoán từ log. Hai job tổng hợp "CI required" và "Security required" bị loại khỏi danh sách bước vì chúng chỉ đỏ khi một bước khác đỏ.

## Sources

- **181 → 141 commit**: Mọi nhánh → thay đổi duy nhất sau khi bỏ 11 merge, 3 stash, 11 bot dependabot và bản trùng do rebase. 45 commit kiểu sửa lỗi (31 fix:, 1 revert, 13 harden/stabilize nhập nhằng).
- **76 PR**: 57 do người viết (13 tiêu đề fix), 12 đang mở, 0 issue. Thân commit và PR phần lớn rỗng hoặc là template nên cách sửa phải lấy từ diff và phiên làm việc.
- **25 thread Codex**: 14/08 → 09/10, khoảng 472 triệu token, 110 lượt hoàn tất và 8 lượt bị ngắt. Bộ nhớ tự động của Codex rỗng (memories_1.sqlite: 0 dòng).
- **5 phiên Claude**: 04/10 → 09/10 (65 MB) và 3 note memory về dự án (service-map, nhánh multi-pod, chi phí). Lịch sử Claude trước 04/10 không nằm trên máy này.
- **11 bài học**: LRN-2026-001 đến 011 trong lessons-registry, cộng 20 file review/plan trong docs/plans và memory khởi động project-memory.md.
- **360 run CI**: GitHub Actions (CI, Security, Hosted release): 132 đỏ, trong đó 81/286 từ nhánh của bạn và 51/74 từ PR Dependabot. 2 cảnh báo CodeQL, 0 cảnh báo Dependabot.

## Playbook (how problems were solved)

- **Tái hiện trên hạ tầng thật rồi mới sửa, kèm test** (tái hiện): Lỗi race và trùng event được dựng lại rồi mới sửa. Relay realtime gửi trùng theo số pod có test hai pod chạy mã thật của adapter Redis và một case Redis thật, đã xác nhận đỏ khi bỏ fix. View count cộng đôi được tái hiện bằng lỗi "current transaction is aborted" trên Postgres thật. JWT trùng trong cùng giây có test riêng. 30 trên 102 vấn đề có test hoặc guard đi kèm.
- **Biến lỗi CI thành cổng chặn** (guard): Sau mỗi lần CI đỏ, cái sai được đưa vào guard: ci:preflight chạy container Node 22 sạch trước khi push, watchdog theo từng stage thay cho wrapper 45 giây, guard migration bất biến, test quét cấu hình theo máy, ManagedInterval cho job định kỳ. 16 vấn đề xử lý bằng chỉnh CI hoặc cổng chất lượng.
- **Windows: chuẩn hoá thay vì né** (windows): Chuỗi lỗi ngày 14/08 được xử lý bằng shim cho .cmd, resolver Jest riêng, chuẩn hoá path POSIX trong test và bỏ qua stage Linux-only trên host Windows (vẫn chạy trong container sạch), không tắt gate.
- **Cấu hình và deploy** (cấu hình): Lỗi môi trường xử lý ở cấu hình: biến production, avatar CDN giả đổi thành SVG local, bundleId Apple bắt buộc khi verifier là store. Riêng lệch phiên bản deploy (route profile 404) mới dừng ở khuyến nghị redeploy, chưa thấy bằng chứng đã làm. 13 vấn đề dùng env-config, 2 dùng redeploy.
- **Ghi bài học để lỗi không quay lại** (ghi lại): Bài học vào lessons-registry (11 mục, mỗi mục có guard và bằng chứng), quyết định lớn vào ADR, và lỗi quy trình của agent thành quy tắc: tối đa 2 sub-agent, trích xuất tất định trước, ghi kết quả từng phần. 10 vấn đề có tài liệu thiết kế/ADR/bài học, 19 có quy tắc quy trình.
- **Chưa xử lý** (còn lại): 6 quan sát audit chưa xác nhận, 1 giới hạn đã biết cần quyết định sản phẩm (advisory lock, outbox), chưa bắt buộc required checks, OTP trả mã trong response, lệch phiên bản deploy production, guest reload mất device token, hai nhóm test timeout trên Windows và Core API production crash lúc boot. 16 vấn đề, chưa thấy commit sửa.

## Method

- Nguồn: 181 commit, 76 PR, 501 run GitHub Actions và cảnh báo CodeQL, lessons-registry và docs/plans, 25 thread Codex (đọc từ thread_items trong SQLite), 5 phiên Claude cùng memory. Số liệu git và CI dựng bằng script, không qua mô hình.
- Bảy agent (tối đa hai chạy cùng lúc, đúng AGENTS.md) đọc các gói bằng chứng dựng sẵn và trích 130 bản ghi vấn đề thô. Chi phí: khoảng 528 nghìn token, 3 phút 40 giây.
- Gộp trùng giữa nguồn thành 108 dòng: 102 vấn đề và 6 báo động giả. Bảy bản ghi thô bị loại hoặc tách: 2 bản ghi tổng quát trùng với bản ghi chi tiết, 1 đề xuất tối ưu, 2 mục cá nhân hoá terminal, 1 review FAIL không có chi tiết, 1 gói 6 quan sát được tách thành 6 dòng. Bổ sung thủ công 4 dòng từ lịch sử CI/CodeQL và 3 gotcha từ memory.
- Kiểm chứng tự động: 274/275 tham chiếu tồn tại (một commit cũ nêu trong lessons-registry đã không còn trong lịch sử) và 168/170 trích dẫn khớp nguyên văn với nguồn. Tám commit cốt lõi được đối chiếu tay với diff.
- Không tính: tính năng mới, hỏi đáp, lệnh thăm dò thất bại, 19 golden-bug fixtures (bài mẫu cho review, không phải sự cố), và rủi ro scale lý thuyết trong capacity plan.
- Phân loại: "lỗi / sự cố thực tế" là thứ đã làm hỏng build, CI, deploy hoặc hành vi; "thiết kế · quy trình · quan sát" gồm lỗi thiết kế, sai sót quy trình và công cụ AI, và quan sát từ đọc code chưa tái hiện.

## Limits

- Phiên Claude/Codex trước 13/08 không còn nguồn nào (máy cũ đã cài lại, backup không chứa dự án này), nên tháng 7 chỉ dựa vào git, PR, docs và lịch sử CI. Lịch sử GitHub Actions bù một phần: nhánh của chủ repo có 74/219 run đỏ trong tháng đó.
- Tháng 7 chỉ có git và tài liệu làm nguồn, tháng 8 có log Codex chi tiết, nên so sánh giữa các tháng bị lệch về phía tháng 8.
- Số đếm phụ thuộc cách gộp. Gộp theo nguyên nhân gốc (cả chuỗi lỗi Windows thành một) sẽ ít hơn, tách theo lỗi con sẽ nhiều hơn.
- Đây là phân tích tĩnh, không chạy lại test hay tái hiện lỗi. Sáu quan sát audit chưa xác nhận ở runtime. Agent trích xuất có thể diễn giải sai nguyên nhân; bằng chứng được đối chiếu tự động nhưng từng nhận định không được kiểm toán lại toàn bộ.
- Sổ được cập nhật đến commit d3cb28c (10/10/2026) của nhánh fix/multi-pod-readiness; tại thời điểm dựng trang không có commit nào mới hơn.

Dữ liệu: repo ducmanh001/litmatch @ d3cb28c, SQLite của Codex, transcript Claude. Sổ đầy đủ, không ẩn mục nào (kể cả các mục bảo mật và production đang mở), công khai trên GitHub Pages.
