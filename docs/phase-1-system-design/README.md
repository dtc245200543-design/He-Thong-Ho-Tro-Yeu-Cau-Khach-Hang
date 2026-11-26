# Phase 1 - System Design

## Muc tieu va pham vi

Tai lieu nay thiet ke he thong ho tro yeu cau khach hang theo De tai 07 va Huong dan chung. Day la tai lieu thiet ke, khong tao database, API hoat dong, message consumer, SignalR hub, client hay deployment.

Phan tich bao gom cac chuc nang bat buoc, cac thanh phan toi thieu `Support API`, `Assignment Worker`, `Notification Service`, RabbitMQ, SignalR va co so du lieu. Cac tinh nang mo rong khong nam trong pham vi thiet ke nen.

## Tai lieu nguon da doi chieu

- `HUONG-DAN-CHUNG.md.pdf`: C#, .NET 10, ASP.NET Core Minimal API, REST va cong nghe phan tan theo de tai, service doc lap, cau hinh moi truong, logging, kha nang phuc hoi, san pham can nop va cac mo rong khong bat buoc.
- `07-he-thong-ho-tro-yeu-cau-khach-hang.md.pdf`: mo ta he thong, kien truc toi thieu, 8 chuc nang chinh, 5 API bat buoc va cac truong du lieu toi thieu.

## Muc luc

1. [Phan tich yeu cau](01-requirements.md)
2. [Tac nhan va nghiep vu](02-actors-and-workflows.md)
3. [Kien truc tong the](03-architecture.md)
4. [Trach nhiem service](04-service-responsibilities.md)
5. [Luồng RabbitMQ va SignalR](05-messaging-and-realtime.md)
6. [Thiet ke du lieu va ERD](06-data-model.md)
7. [Nam API bat buoc](07-api-contracts.md)
8. [Cau truc Solution va thu muc](08-solution-structure.md)
9. [Ke hoach kiem thu](09-test-plan.md)

## Quy uoc va gioi han

- Trang thai dung dung tap gia tri `New`, `Assigned`, `InProgress`, `Resolved` trong de bai.
- Ticket co the chua duoc gan; khi da gan thi dich den la mot nhan vien hoac mot nhom, khong dong thoi ca hai.
- De bai khong quy dinh danh muc uu tien, quy tac phan cong cu the, co che xac thuc, SLA hay phan quyen. Tai lieu khong tu dat ra cac chinh sach nghiep vu nay.
- PostgreSQL duoc chon lam co so du lieu quan he de luu ticket va lich su; day la quyet dinh ky thuat cho ban thiet ke, chua tao database hay schema.
- Kiem thu duoc lap ke hoach de thuc hien o giai doan sau; Phase 1/2 khong tao test hay chay database.
- Khong them tinh nang tuy chon nhu authentication/authorization, retry queue/dead-letter queue, idempotent consumer, audit/statistics service hay client.
