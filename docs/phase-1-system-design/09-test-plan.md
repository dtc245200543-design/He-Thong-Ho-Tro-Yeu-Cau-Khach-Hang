# Ke hoach kiem thu

Ke hoach nay xac dinh nhung gi can kiem thu khi cac phase hien thuc den. Phase 1 va Phase 2 khong tao test suite va khong can database/broker de kiem thu.

## Kiem thu theo lop

| Lop | Pham vi | Tieu chi dat |
| --- | --- | --- |
| Unit - API validation | Tao ticket va cap nhat status voi request hop le/khong hop le. | Du lieu hop le duoc chap nhan; status chi nhan dung bon gia tri. |
| Unit - assignment | Quy tac gan nhom/nhan vien don gian. | Dau vao theo quy tac da chot tao dung mot dich den phan cong; ticket moi khong bi gan ca user va group. |
| Unit - history | Tao ticket, thay doi trang thai va phan cong. | Moi thay doi bat buoc tao ban ghi history voi gia tri truoc/sau phu hop. |
| API integration | Nam endpoint bat buoc. | Tao, lay danh sach, lay chi tiet, cap nhat status va lay theo user dung contract; ID sai tra not found. |
| Persistence integration | PostgreSQL va quan he du lieu. | Ticket, assignment va history duoc luu/doc dung; rang buoc FK va dich den duoc giu. |
| RabbitMQ integration | Tao ticket, phan cong va su kien thay doi. | `ticket.created` den Worker; Worker luu assignment/history truoc khi ack; `ticket.changed` den Notification Service. |
| SignalR integration | Thay doi trang thai/assignment. | Client ket noi nhan cap nhat tu ticket lien quan; noi dung su kien khop du lieu da commit. |
| Resilience | Tam dung Worker hoac Notification Service. | Message con trong queue duoc xu ly sau khi consumer ket noi lai; consumer khong ack neu DB update that bai. |
| Solution build | Build Release cho toan bo Solution tren SDK .NET 10. | Restore va build hoan tat khong loi; Solution co dung bon project net10.0. |

## Ma tran nghiep vu bat buoc

| Kich ban | Ket qua can xac minh |
| --- | --- |
| Tao ticket hop le | Ticket `New`, du lieu nguoi gui/noi dung/priority duoc luu, co history va duoc phat vao queue. |
| Assignment Worker xu ly | Ticket duoc gan mot user hoac group, chuyen `Assigned`, co history va phat event. |
| GET list/detail/by-user | Ket qua khop du lieu da luu; ticket khong ton tai duoc xu ly theo contract. |
| PATCH status hop le | Status cap nhat, history ghi nhan, Notification Service phat cap nhat realtime. |
| PATCH status ngoai tap | Request bi tu choi, du lieu ticket khong bi thay doi. |
| Consumer restart | Message chua ack duoc xu ly lai sau khi consumer khoi dong lai. |

## Dieu kien va gioi han

- Kiem thu integration can PostgreSQL, RabbitMQ va SignalR host; se duoc thuc hien khi cac thanh phan duoc hien thuc.
- Khong gan nguong performance vi de bai khong quy dinh.
- Phase 2 chi chay `dotnet restore` va `dotnet build --configuration Release`; ket qua chi xac nhan project skeleton, khong thay the cac kiem thu nghiep vu tren.
