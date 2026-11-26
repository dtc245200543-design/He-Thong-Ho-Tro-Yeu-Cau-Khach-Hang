# Tac nhan va nghiep vu

## Tac nhan

| Tac nhan | Vai tro trong he thong |
| --- | --- |
| Khach hang / nguoi gui | Tao ticket, xem danh sach/chi tiet ticket cua minh va nhan thay doi lien quan. |
| Nhan vien ho tro | Duoc Worker gan ticket; xem ticket duoc phan cong va cap nhat trang thai theo API. |
| Nhom xu ly | Dich den phan cong thay the cho mot nhan vien cu the. |
| Assignment Worker | Nhan ticket moi, ap dung quy tac phan loai/phan cong don gian va ghi ket qua. |
| Notification Service | Nhan su kien thay doi va gui cap nhat realtime qua SignalR cho client lien quan. |

Khach hang, nhan vien va nhom la cac vai tro nghiep vu. De bai khong quy dinh co che dang nhap, quan ly danh tinh hay phan quyen; do do tai lieu chi su dung ID de lien ket du lieu, khong thiet ke he thong tai khoan.

## Nghiep vu chinh

### Tiep nhan va phan cong ticket

1. Client gui thong tin ticket den `POST /tickets`.
2. Support API kiem tra du lieu dau vao, tao ticket trang thai `New` va ghi lich su tao moi.
3. Support API dua thong diep ticket moi vao RabbitMQ.
4. Assignment Worker nhan thong diep, lay thong tin can thiet, chon mot nhom hoac nhan vien theo quy tac don gian.
5. Worker ghi dich den phan cong, cap nhat trang thai thanh `Assigned` va ghi lich su thay doi trong database.
6. Worker phat su kien thay doi de Notification Service thong bao realtime.

### Tra cuu ticket

- Client lay danh sach qua `GET /tickets`.
- Client lay chi tiet qua `GET /tickets/{id}`.
- Client lay cac ticket theo nguoi gui qua `GET /users/{userId}/tickets`.

### Cap nhat trang thai

1. Client gui trang thai moi den `PATCH /tickets/{id}/status`.
2. Support API xac nhan ticket ton tai va trang thai thuoc tap bon gia tri duoc quy dinh.
3. Support API ghi trang thai moi va lich su thay doi.
4. Support API phat su kien; Notification Service gui cap nhat realtime.

De bai khong quy dinh cac chuyen tiep hop le giua bon trang thai, nen chua ap dat state machine ngoai viec gioi han gia tri trang thai.
