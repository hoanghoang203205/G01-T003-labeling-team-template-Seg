# Problem backlog

Những chỗ gặp trong lúc gán nhãn mà **guideline chưa trả lời được**, cộng các pain point về công cụ.

Ghi ngay khi gặp, kể cả lúc chưa biết xử lý thế nào. Một edge case không được ghi lại thì
mỗi người sẽ tự xử lý theo một kiểu — và đó là nguồn lớn nhất của nhãn không nhất quán.

> Các mục bên dưới là **ví dụ**, tên và link CVAT đều giả. Mẫu trống để copy nằm cuối file.

## Danh sách

| Mã | Tóm tắt | Loại | Mục guideline | Trạng thái | Kết quả |
|---|---|---|---|---|---|
| [P-001](#p-001) | Người ngồi sau xe máy: box riêng hay gộp với người lái | Guideline mơ hồ | §3.2 | ✅ Đã chốt | [QĐ-001](so-quyet-dinh.md#qđ-001) |
| [P-002](#p-002) | Xe bị che khuất hơn một nửa | Guideline chưa nói tới | §3.4 | ↗️ Hỏi BTC | — |
| [P-003](#p-003) | Phải vẽ lại box y hệt qua nhiều frame liên tiếp | Pain point công cụ | — | 🗣️ Đang bàn | — |

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

**Người ngồi sau xe máy: box riêng hay gộp chung với người lái**

- **Loại:** Guideline mơ hồ
- **Mục guideline:** §3.2 — "mỗi người một bounding box"
- **Người phát hiện:** @thanh-vien-b · 16/09/2026
- **Link CVAT:**
  - https://cvat.example.com/tasks/12/jobs/101?frame=37 — hai người, gần như chồng khít
  - https://cvat.example.com/tasks/12/jobs/101?frame=112 — người ngồi sau chỉ lộ đầu
- **Mô tả:** §3.2 nói mỗi người một box, nhưng hình minh hoạ trong guideline lại vẽ một box
  cho cả xe máy lẫn người trên xe.
- **Các cách hiểu:**
  1. Theo câu chữ: người ngồi sau có box `nguoi` riêng.
  2. Theo hình minh hoạ: không vẽ box `nguoi` cho ai đang ngồi trên xe.
- **Xử lý tạm trong lúc chờ:** vẽ box riêng và gắn tag `can_xem_lai` để dễ lọc ra sửa.
- **Kết quả:** ✅ [QĐ-001](so-quyet-dinh.md#qđ-001)

## P-002

**Xe bị che khuất hơn một nửa**

- **Loại:** Guideline chưa nói tới
- **Mục guideline:** §3.4 — chỉ nói về vật thể bị cắt ở mép ảnh, không nói về bị che
- **Người phát hiện:** @thanh-vien-c · 17/09/2026
- **Link CVAT:**
  - https://cvat.example.com/tasks/12/jobs/103?frame=8 — ô tô sau xe buýt, lộ khoảng 30%
  - https://cvat.example.com/tasks/12/jobs/103?frame=64 — xe máy sau cột điện, lộ khoảng 50%
- **Mô tả:** Không rõ có gán nhãn vật thể bị che không, và nếu có thì box ôm phần nhìn thấy
  hay ôm cả phần ước lượng bị che.
- **Các cách hiểu:**
  1. Bỏ qua khi lộ dưới 50%.
  2. Luôn gán, box chỉ ôm phần nhìn thấy.
  3. Luôn gán, box ôm cả phần ước lượng.
- **Xử lý tạm trong lúc chờ:** dừng job 103, chuyển sang job khác ít ca che khuất.
- **Kết quả:** ↗️ Đã hỏi BTC ngày 18/09/2026, chờ trả lời.

## P-003

**Phải vẽ lại box y hệt qua nhiều frame liên tiếp**

- **Loại:** Pain point công cụ
- **Mục guideline:** —
- **Người phát hiện:** @thanh-vien-d · 18/09/2026
- **Link CVAT:** https://cvat.example.com/tasks/12/jobs/105?frame=200 — frame 200–260, xe đỗ không di chuyển
- **Mô tả:** Ảnh chụp liên tiếp từ camera cố định. Xe đỗ bên đường xuất hiện y nguyên ở hàng chục
  frame, annotator phải vẽ lại ở từng frame. Ước tính chiếm ~40% thời gian job 105.
- **Hướng đang cân nhắc:**
  1. Dùng chế độ *Track* sẵn có của CVAT — cần thử xem có hợp với dữ liệu dạng ảnh rời không.
  2. Viết script đọc file export của CVAT, nhân box sang các frame kế tiếp, rồi import lại.
- **Kết quả:** 🗣️ Đang bàn. Nếu chọn hướng 2 thì đổi trạng thái sang 🛠️ và làm trong
  [`source-tool/`](source-tool/).

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


**Minh**
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