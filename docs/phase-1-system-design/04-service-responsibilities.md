# Trach nhiem cua tung service

## CustomerSupport.SupportApi

- La ASP.NET Core Minimal API, nhan cac request REST.
- Thuc hien nam API trong tai lieu thiet ke.
- Kiem tra du lieu request va gia tri trang thai nam trong tap cho phep.
- Tao va doc ticket; cap nhat trang thai; ghi lich su tuong ung.
- Phat su kien ticket tao moi hoac thay doi qua RabbitMQ.
- Khong thuc hien phan cong ticket tai request thread va khong gui SignalR truc tiep.

## CustomerSupport.AssignmentWorker

- La .NET Worker Service doc lap.
- Tieu thu su kien ticket tao moi tu RabbitMQ.
- Ap dung mot quy tac don gian de gan mot nhom hoac nhan vien.
- Luu dich den phan cong, trang thai `Assigned` va ban ghi lich su vao PostgreSQL.
- Phat su kien thay doi sau khi ket qua duoc luu.
- Khong cung cap REST API cho client va khong host SignalR.

De bai khong dinh nghia bang quy tac cu the; quy tac cu the phai duoc chot khi trien khai, khong duoc suy dien thanh mot tinh nang tu dong phan loai phuc tap.

## CustomerSupport.NotificationService

- La service doc lap host SignalR va consumer RabbitMQ.
- Tieu thu su kien ticket thay doi do Support API hoac Assignment Worker phat.
- Gui cap nhat trang thai/phan cong den client lien quan qua SignalR.
- Khong la nguon su that cua ticket; khong tu thay doi du lieu ticket.
- Khong nhan thay API tra cuu; client lay du lieu ban dau qua Support API.

## CustomerSupport.Contracts

- Thu vien chia se DTO va hop dong thong diep giua cac project.
- Khong ket noi database, RabbitMQ hay SignalR.
- Khong chua quy tac nghiep vu; cac service van so huu xu ly cua minh.

## Ranh gioi phu thuoc

| Project | Tham chieu project |
| --- | --- |
| CustomerSupport.Contracts | Khong tham chieu project nao. |
| CustomerSupport.SupportApi | CustomerSupport.Contracts. |
| CustomerSupport.AssignmentWorker | CustomerSupport.Contracts. |
| CustomerSupport.NotificationService | CustomerSupport.Contracts. |

Khong co tham chieu truc tiep giua ba service; khong co service nao tham chieu project UI.
