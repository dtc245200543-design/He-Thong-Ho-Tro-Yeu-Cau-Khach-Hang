# Phan tich yeu cau

## Yeu cau chuc nang

| ID | Yeu cau bat buoc | Ket qua mong doi |
| --- | --- | --- |
| FR-01 | Tao yeu cau ho tro moi | Luu nguoi gui, noi dung, muc uu tien va trang thai ban dau `New`; yeu cau duoc dua vao luong phan cong. |
| FR-02 | Tra cuu danh sach yeu cau | Co the lay danh sach ticket. |
| FR-03 | Tra cuu chi tiet yeu cau | Co the lay mot ticket theo ID. |
| FR-04 | Tra cuu ticket theo nguoi dung | Co the lay danh sach ticket cua mot `userId`. |
| FR-05 | Phan loai hoac gan ticket | Worker nhan yeu cau moi va gan mot nhom hoac mot nhan vien theo quy tac don gian. |
| FR-06 | Cap nhat trang thai | Ho tro dung bon trang thai `New`, `Assigned`, `InProgress`, `Resolved`. |
| FR-07 | Phat su kien thay doi | Phat su kien khi trang thai hoac dich den phan cong thay doi. |
| FR-08 | Thong bao realtime | Gui thay doi den client lien quan qua SignalR. |
| FR-09 | Luu lich su | Ghi nhan cac thay doi cua ticket de co the tra cuu. |

Nam API bat buoc va luong xu ly duoc mo ta chi tiet tai [API contracts](07-api-contracts.md) va [Messaging and realtime](05-messaging-and-realtime.md).

## Yeu cau phi chuc nang

| ID | Yeu cau | Co so |
| --- | --- | --- |
| NFR-01 | Nen tang va ngon ngu la C# tren .NET 10. API su dung ASP.NET Core Minimal API. | Huong dan chung. |
| NFR-02 | Cac service duoc to chuc de chay va trien khai doc lap theo kien truc. | Huong dan chung va kien truc toi thieu De tai 07. |
| NFR-03 | Cac cau hinh phu thuoc moi truong (connection string, broker address, URL va port) nam ngoai ma nguon. | Huong dan chung. |
| NFR-04 | Co logging du de theo doi cac luong qua API, Worker va Notification Service. | Huong dan chung. |
| NFR-05 | He thong phuc hoi hop ly khi mot service tam dung: message con lai trong queue duoc xu ly khi consumer hoat dong lai; loi ket noi DB khong duoc xem la xu ly thanh cong. | Huong dan chung va RabbitMQ trong De tai 07. |
| NFR-06 | Du lieu ticket va lich su duoc luu ben vung; truy van danh sach, chi tiet va theo user doc tu cung mot nguon du lieu. | Chuc nang cua De tai 07. |
| NFR-07 | Thong bao realtime duoc gui bat dong bo sau thay doi da duoc ghi nhan, khong lam client phu thuoc vao viec polling de nhan thay doi. | Mo ta SignalR trong De tai 07. |
| NFR-08 | Bao cao, ma nguon day du, huong dan build/chay va lich su commit la san pham cuoi cung cua hoc phan; moi service .NET co Dockerfile va he thong co docker-compose. | Huong dan chung; chi la muc tieu cho cac phase tuong ung, khong lam trong Phase 1/2. |

De bai khong dua ra muc tieu latency, throughput, SLA, kich thuoc du lieu hay chinh sach truy cap; khong tu dat ra cac nguong so lieu.

## Ngoai pham vi

- Dang ky/dang nhap, xac thuc va phan quyen.
- Danh muc/ma uu tien va bang quy tac phan cong cu the chua duoc de bai quy dinh.
- Retry topology, dead-letter queue, idempotent consumer, correlation ID, health-check, structured logging va service thong ke/audit mo rong.
- Web client hoac console client, Dockerfile, docker-compose va trien khai.
- Database migration, EF Core va du lieu mau trong Phase 1/2.
