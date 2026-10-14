# Roadmap · Litmatch Error History

id: roadmap
site: history
updated: 2026-10-14; ledger covers repo ducmanh001/litmatch up to d3cb28c

"Roadmap" của trang này: **A. lộ trình đọc**, **B. việc còn mở xếp theo loại** (sổ lỗi công khai đầy đủ, kể cả mục bảo mật và production đang mở), **C. bài học để không lặp lại**, **D. lộ trình dự án** (ở Atlas).
Tệp máy đọc: [llms.txt](llms.txt) · [sitemap.xml](sitemap.xml) · [search-index.json](search-index.json) · [json/issues.json](json/issues.json).

## A. Lộ trình đọc

| Câu hỏi | Mở |
|---|---|
| Một vấn đề cụ thể (P0xx) | issues/P0xx.md (problem, root cause, resolution, evidence) |
| Các vấn đề của một khu vực | issues/<area>.md, danh sách khu vực ở mục B3 |
| Còn gì đang mở | mục B1 và B2 của trang này |
| Bài học và cách đã xử lý | summary.md (playbook), mục C |
| Số liệu CI | summary.md (GitHub Actions) |
| Muốn tìm theo từ khoá | search.html, search-index.json |
| Khu vực này nằm ở module nào, API nào | https://ducmanh001.github.io/litmatch-atlas-demo/pack/modules/index.md |

## B. Việc còn mở

Loại A = lỗi / sự cố thực tế; B = thiết kế, quy trình, quan sát từ đọc code; C = báo động giả.

### B1. Đang mở hoặc đang xử lý (16)

| id | trạng thái | loại | khu vực | ngày | vấn đề |
|---|---|---|---|---|---|
| [P085](issues/P085.md) | open | A | frontend-ux | 2026-10-09 | Guest reload mất device token → Matching 401 |
| [P078](issues/P078.md) | open | A | dependencies | 2026-09-09 | PR Dependabot đỏ vì chính sách minimumReleaseAge của pnpm |
| [P077](issues/P077.md) | open | A | windows-toolchain | 2026-09-03 | Test hard-kill của run-stage lỗi trên Windows (exit 124) |
| [P075](issues/P075.md) | open | A | auth-security | 2026-09-03 | OTP trả mã ngay trong response khi production bật OTP |
| [P074](issues/P074.md) | in-progress | A | deploy-config | 2026-08-21 | Core API production crash lúc boot (media storage dev / thiếu biến R2) |
| [P065](issues/P065.md) | open | A | deploy-config | 2026-08-19 | Production chạy bản cũ: route profile 404, thông báo Facebook cũ |
| [P063](issues/P063.md) | open | A | ci-cd | 2026-08-14 | Test frontend (admin/web) timeout lặp lại |
| [P012](issues/P012.md) | open | A | auth-security | 2026-07-16 | CodeQL: loop-bound-injection (high) ở common/hash/fnv1a.ts còn mở |
| [P104](issues/P104.md) | open | B | other | 2026-10-09 | soul-match end phát lại soul.ended khi replay |
| [P103](issues/P103.md) | open | B | other | 2026-10-09 | Phân trang cursor video-queue admin (pending_review tăng dần nhưng cursor dùng less-than; suy luận) |
| [P102](issues/P102.md) | open | B | other | 2026-10-09 | Comment k8s lỗi thời |
| [P101](issues/P101.md) | open | B | other | 2026-10-09 | Lời mời hết hạn kiểu lazy-expire không được persist |
| [P100](issues/P100.md) | open | B | other | 2026-10-09 | getHiddenUserIds không có cửa sổ thời gian (cần quyết định sản phẩm) |
| [P099](issues/P099.md) | open | B | other | 2026-10-09 | Ranked sort loại hàng có rankScore IS NULL |
| [P094](issues/P094.md) | open | B | matching | 2026-10-09 | Giới hạn đã biết: advisory lock Palm/Movie Match, outbox chưa có consumer/retention |
| [P055](issues/P055.md) | open | B | ci-cd | 2026-08-14 | Chưa bắt buộc required checks: PR vẫn merge được khi CI đỏ |

### B2. Đã giảm nhẹ, chưa dứt điểm (8)

| id | trạng thái | loại | khu vực | ngày | vấn đề |
|---|---|---|---|---|---|
| [P092](issues/P092.md) | mitigated | A | windows-toolchain | 2026-10-09 | Windows thiếu zip/unzip nên docs:check không chạy |
| [P015](issues/P015.md) | mitigated | A | realtime-gateway | 2026-07-18 | Socket reconnect không khôi phục state bền (LRN-005) |
| [P011](issues/P011.md) | mitigated | A | database-concurrency | 2026-07-13 | Transaction Postgres bị aborted sau unique violation (LRN-002) |
| [P072](issues/P072.md) | mitigated | B | windows-toolchain | 2026-08-20 | Windows: Nx build lỗi 1314 + runner timeout (exit 124) |
| [P061](issues/P061.md) | mitigated | B | observability | 2026-08-14 | Lỗi TS ở tsconfig.spec không làm build fail |
| [P051](issues/P051.md) | mitigated | B | ai-agent-process | 2026-08-14 | ci:preflight treo làm mất thay đổi chưa commit |
| [P050](issues/P050.md) | mitigated | B | ai-agent-process | 2026-08-14 | Không push được vì môi trường (thiếu gh, Docker/WSL2, hook) |
| [P016](issues/P016.md) | mitigated | B | ai-agent-process | 2026-07-18 | PASS cục bộ bị hiểu thành PASS toàn repo (LRN-006) |

### B3. Theo khu vực (không tính báo động giả)

| khu vực | tổng | đang mở/đang xử lý |
|---|---|---|
| [ci-cd](issues/ci-cd.md) | 22 | 2 |
| [ai-agent-process](issues/ai-agent-process.md) | 13 | 0 |
| [auth-security](issues/auth-security.md) | 10 | 2 |
| [frontend-ux](issues/frontend-ux.md) | 9 | 1 |
| [windows-toolchain](issues/windows-toolchain.md) | 8 | 1 |
| [deploy-config](issues/deploy-config.md) | 7 | 2 |
| [other](issues/other.md) | 7 | 6 |
| [matching](issues/matching.md) | 6 | 1 |
| [database-concurrency](issues/database-concurrency.md) | 5 | 0 |
| [economy-payment](issues/economy-payment.md) | 3 | 0 |
| [observability](issues/observability.md) | 3 | 0 |
| [short-video](issues/short-video.md) | 3 | 0 |
| [realtime-gateway](issues/realtime-gateway.md) | 2 | 0 |
| [dependencies](issues/dependencies.md) | 2 | 1 |
| [docs-tooling](issues/docs-tooling.md) | 2 | 0 |

## C. Bài học để không lặp lại

- **Tái hiện trên hạ tầng thật rồi mới sửa, kèm test**: Lỗi race và trùng event được dựng lại rồi mới sửa. Relay realtime gửi trùng theo số pod có test hai pod chạy mã thật của adapter Redis và một case Redis thật, đã xác nhận đỏ khi bỏ fix. View count cộng đôi được tái hiện bằng lỗi "current transaction is aborted" trên Postgres thật. JWT trùng trong cùng giây có test riêng. 30 trên 102 vấn đề có test hoặc guard đi kèm.
- **Biến lỗi CI thành cổng chặn**: Sau mỗi lần CI đỏ, cái sai được đưa vào guard: ci:preflight chạy container Node 22 sạch trước khi push, watchdog theo từng stage thay cho wrapper 45 giây, guard migration bất biến, test quét cấu hình theo máy, ManagedInterval cho job định kỳ. 16 vấn đề xử lý bằng chỉnh CI hoặc cổng chất lượng.
- **Windows: chuẩn hoá thay vì né**: Chuỗi lỗi ngày 14/08 được xử lý bằng shim cho .cmd, resolver Jest riêng, chuẩn hoá path POSIX trong test và bỏ qua stage Linux-only trên host Windows (vẫn chạy trong container sạch), không tắt gate.
- **Cấu hình và deploy**: Lỗi môi trường xử lý ở cấu hình: biến production, avatar CDN giả đổi thành SVG local, bundleId Apple bắt buộc khi verifier là store. Riêng lệch phiên bản deploy (route profile 404) mới dừng ở khuyến nghị redeploy, chưa thấy bằng chứng đã làm. 13 vấn đề dùng env-config, 2 dùng redeploy.
- **Ghi bài học để lỗi không quay lại**: Bài học vào lessons-registry (11 mục, mỗi mục có guard và bằng chứng), quyết định lớn vào ADR, và lỗi quy trình của agent thành quy tắc: tối đa 2 sub-agent, trích xuất tất định trước, ghi kết quả từng phần. 10 vấn đề có tài liệu thiết kế/ADR/bài học, 19 có quy tắc quy trình.
- **Chưa xử lý**: 6 quan sát audit chưa xác nhận, 1 giới hạn đã biết cần quyết định sản phẩm (advisory lock, outbox), chưa bắt buộc required checks, OTP trả mã trong response, lệch phiên bản deploy production, guest reload mất device token, hai nhóm test timeout trên Windows và Core API production crash lúc boot. 16 vấn đề, chưa thấy commit sửa.

## D. Lộ trình dự án

Giai đoạn, quy mô S0-S8, ưu tiên P0-P2 và quyết định đã hoãn: [roadmap của Atlas](https://ducmanh001.github.io/litmatch-atlas-demo/roadmap.md).

Các trang cùng bộ: [Atlas](https://ducmanh001.github.io/litmatch-atlas-demo/) · [Service Map](https://ducmanh001.github.io/litmatch-service-map/) · [Error History](https://ducmanh001.github.io/litmatch-error-history/). Roadmap dự án và việc còn mở nằm ở [roadmap của Atlas](https://ducmanh001.github.io/litmatch-atlas-demo/roadmap.md).
