# Problem backlog

Những chỗ gặp trong lúc gán nhãn mà **guideline chưa trả lời được**, cộng các pain point về công cụ.

Ghi ngay khi gặp, kể cả lúc chưa biết xử lý thế nào. Một edge case không được ghi lại thì
mỗi người sẽ tự xử lý theo một kiểu — và đó là nguồn lớn nhất của nhãn không nhất quán.

> Các mục bên dưới là **ví dụ**, tên và link CVAT đều giả. Mẫu trống để copy nằm cuối file.

## Danh sách

| Mã | Tóm tắt | Loại | Mục guideline | Trạng thái | Kết quả |
|---|---|---|---|---|---|
| [P-001](#p-001) |Dây điện xuất hiện trên vùng bầu trời | Guideline mơ hồ | §2, §3, §6 — Rule 03 | 🔴 Mở | ↗️ Hỏi BTC |
| [P-002](#p-002) | Xe ở quá xa, không thể xác định rõ class | Guideline chưa nói tới |§3 — OBJECT NHỎ/XA; §4 — car vs truck vs bus; §6; §9 | 🔴 Mở| ↗️ Hỏi BTC |

**Loại**

| Loại | Nghĩa là |
|---|---|
| Guideline chưa nói tới | Tình huống không có trong guideline |
| Guideline mơ hồ | Đọc guideline ra được hai cách hiểu trở lên |
| Guideline mâu thuẫn | Hai mục trong guideline nói ngược nhau |
| Pain point công cụ | Guideline rõ, nhưng làm trên CVAT chậm hoặc dễ sai |

**Trạng thái:** 🔴 Mở · 🗣️ Đang bàn · ↗️ Hỏi BTC · ✅ Đã chốt (trỏ sang QĐ) · 🛠️ Làm tool (trỏ sang `source-tool/`) · ⚪ Bỏ (ghi lý do)

---
## P-001

**Dây điện xuất hiện trên vùng bầu trời**

- **Loại:** Guideline mơ hồ
- **Mục guideline:** §2, §3, §6 — Rule 03
- **Người phát hiện:** [@TMTower18](https://github.com/TMTower18) · 16/09/2026
- **Link CVAT:** (https://cvat.note.transformerlabs.ai/tasks/176/jobs/1554?frame=12)
- **Mô tả:** Trong một số frame, dây điện chạy qua khu vực bầu trời. Dây điện không
  thuộc danh sách 19 class được quy định trong §2, nhưng guideline chưa nói rõ
  cách xử lý phần pixel của dây điện khi nó nằm trên vùng sky.
- **Các cách hiểu:**
  1. Không tạo class riêng cho dây điện; phần nền xung quanh dây điện vẫn được
     gán theo semantic class tương ứng, ví dụ sky.
  2. Đưa vùng dây điện vào review vì không có class phù hợp trong 19 class.
- **Xử lý tạm trong lúc chờ:** Không tạo class mới và không tự gán dây điện vào
  một class khác. Đưa case vào review nếu không xác định được cách xử lý theo
  semantic hiện tại.
- **Kết quả:** 🔴 Mở

## P-002

**Xe ở quá xa, không thể xác định rõ class**

- **Loại:** Guideline chưa nói tới
- **Mục guideline:** §3 — OBJECT NHỎ/XA; §4 — car vs truck vs bus; §6; §9
- **Người phát hiện:** [@TMTower18](https://github.com/TMTower18) · 17/09/2026
- **Link CVAT:** (https://cvat.note.transformerlabs.ai/tasks/176/jobs/1554?frame=15)
- **Mô tả:** Một số xe xuất hiện ở khoảng cách rất xa, kích thước rất nhỏ hoặc
  hình ảnh bị mờ khiến không thể xác định chắc chắn class của phương tiện.
- **Các cách hiểu:**
  1. Nếu vẫn nhận dạng được class thì annotate.
  2. Nếu quá nhỏ/mờ để xác định chắc chắn thì đưa review thay vì đoán.
- **Xử lý tạm trong lúc chờ:** Zoom để kiểm tra. Nếu vẫn không thể xác định
  chắc chắn class, tạo Issue/đưa reviewer theo quy trình escalation.
- **Kết quả:** 🔴 Mở

---

## Mẫu để copy

```markdown
## P-NNN

**Tóm tắt một dòng**

- **Loại:** Guideline chưa nói tới | Guideline mơ hồ | Guideline mâu thuẫn | Pain point công cụ
- **Mục guideline:** §
- **Người phát hiện:** @ · dd/mm/yyyy
- **Link CVAT:** (bỏ trống nếu không có)
  - https://…/tasks/<id>/jobs/<id>?frame=<n> — frame này có gì
- **Mô tả:**
- **Các cách hiểu:** (với pain point công cụ thì ghi **Hướng đang cân nhắc:**)
  1.
  2.
- **Xử lý tạm trong lúc chờ:**
- **Kết quả:** 🔴 Mở
```

Nhớ thêm một dòng vào bảng **Danh sách** ở đầu file.
