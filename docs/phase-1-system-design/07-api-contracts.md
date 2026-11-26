# Nam API bat buoc

Tat ca endpoint REST thuoc Support API. Cac payload duoi day mo ta muc logic; chua tao endpoint hoat dong trong Phase 1/2.

## 1. Tao ticket

`POST /tickets`

- Request toi thieu: `submittedByUserId`, `content`, `priority`.
- Thanh cong: tra ve ticket vua tao voi ID va trang thai ban dau `New`.
- Tiep theo: ghi lich su tao ticket va dua su kien `ticket.created` vao luong RabbitMQ.
- Loi: request khong hop le hoac khong the tiep nhan cong viec phan cong phai duoc phan hoi ro rang.

## 2. Lay danh sach ticket

`GET /tickets`

- Tra ve danh sach ticket voi cac truong can thiet de nhan dien, xem trang thai, muc uu tien va dich den phan cong.
- De bai khong quy dinh filter, sort hay pagination; khong them query contract bat buoc.

## 3. Lay chi tiet ticket

`GET /tickets/{id}`

- Tra ve chi tiet mot ticket va cac thong tin nghiep vu toi thieu.
- ID khong ton tai: tra ve not found.

## 4. Cap nhat trang thai ticket

`PATCH /tickets/{id}/status`

- Request: `status`.
- Gia tri chap nhan: `New`, `Assigned`, `InProgress`, `Resolved`.
- Thanh cong: cap nhat ticket, ghi TicketHistory va phat `ticket.changed`.
- ID khong ton tai: not found; gia tri status ngoai tap: loi validation.
- De bai khong quy dinh transition matrix; khong tu them quy tac chuyen trang thai.

## 5. Lay ticket theo nguoi dung

`GET /users/{userId}/tickets`

- Tra ve cac ticket co `SubmittedByUserId` bang `userId`.
- Khong ton tai ket qua: tra ve danh sach rong; de bai khong yeu cau tao User moi khi truy van.

## Truong du lieu co ban

Du lieu ticket can dap ung cac truong toi thieu trong de bai: nguoi gui, noi dung, muc uu tien, nguoi hoac nhom xu ly va trang thai. TicketHistory cung luu lich su thay doi theo FR-09.
