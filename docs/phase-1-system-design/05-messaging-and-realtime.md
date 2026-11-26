# Luong RabbitMQ va SignalR

## RabbitMQ

### Topology logic

- Topic exchange: `support.events`.
- Queue cho Worker: `assignment.ticket-created`, bind routing key `ticket.created`.
- Queue cho thong bao: `notification.ticket-changed`, bind routing key `ticket.changed`.
- Queue durable; message duoc ack sau khi consumer ghi thanh cong thay doi can thiet vao database.

Ten tren la quy uoc thiet ke, chua tao broker hay queue trong Phase 1/2.

### Luong tao va phan cong

1. Support API tao ticket `New` va luu ticket/lich su.
2. Support API publish `ticket.created` kem ticket ID va du lieu can thiet cho Worker.
3. Assignment Worker doc ticket, tinh dich den phan cong theo quy tac don gian va cap nhat database.
4. Sau khi commit thay doi, Worker ack thong diep `ticket.created`.
5. Worker publish `ticket.changed` chua ticket ID, nguoi gui, dich den phan cong va trang thai moi.
6. Notification Service tieu thu su kien va gui SignalR den client lien quan.

### Luong cap nhat trang thai

1. Support API cap nhat trang thai va ghi lich su vao database.
2. Sau khi commit, API publish `ticket.changed`.
3. Notification Service tieu thu su kien va gui cap nhat realtime.

### Xu ly loi co ban

- Consumer chi ack sau khi thay doi database commit thanh cong.
- Khi consumer ngat ket noi, thong diep chua ack duoc RabbitMQ phat lai sau khi consumer ket noi lai.
- Loi khi phat message phai duoc ghi log va phan hoi ro rang; khong tra ve thanh cong gia tao khi khong dam bao da dua viec vao broker.
- De bai khong yeu cau retry/dead-letter queue, idempotent consumer hay transactional outbox; cac co che nay khong nam trong thiet ke nen.
- Tinh nhat quan giua database va broker khi broker tam dung can duoc xac nhan trong phase tich hop; khong dong bo hai he thong bang mot giao dich database thong thuong.

## Hop dong su kien muc logic

Thong diep can co du thong tin de xu ly, khong truyen toan bo entity database:

| Su kien | Noi phat | Du lieu can thiet |
| --- | --- | --- |
| `ticket.created` | Support API | `ticketId`, `submittedByUserId`, `content`, `priority`, `status`, thoi diem tao. |
| `ticket.changed` | Support API hoac Assignment Worker | `ticketId`, `submittedByUserId`, trang thai hien tai, nguoi/nhom duoc gan (neu co), thoi diem thay doi. |

Contract C# chinh thuc se duoc tao trong project Contracts o cac phase tiep theo; bang tren khong phai implementation hay migration.

## SignalR

1. Client lay danh sach/chi tiet ban dau qua REST.
2. Client mo ket noi SignalR toi Notification Service.
3. Notification Service nhan `ticket.changed`, xac dinh nguoi gui va dich den lien quan tu thong diep.
4. Service gui mot su kien realtime chua ticket ID, trang thai va thong tin phan cong cap nhat den cac client lien quan.
5. Client co the doc lai chi tiet ticket qua REST neu can du lieu hien tai day du.

De bai khong quy dinh ten Hub, ten event SignalR hay co che danh tinh. Ten hop dong SignalR se duoc chot khi hien thuc; khong mo phong authentication/authorization bang client cung cap user ID. Phan quyen va xac thuc khong thuoc yeu cau toi thieu trong hai tai lieu.
