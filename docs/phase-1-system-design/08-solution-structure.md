# Cau truc Solution va thu muc

## Solution du kien

Solution `CustomerSupport.sln` co dung bon project .NET 10:

```text
CustomerSupport.sln
Directory.Build.props
global.json
CustomerSupport.Contracts/
CustomerSupport.SupportApi/
CustomerSupport.AssignmentWorker/
CustomerSupport.NotificationService/
docs/
```

Chi bon project tren la project trong Solution. Thu muc `docs/` chua tai lieu thiet ke va khong phai project .NET.

## Project va loai project

| Project | Loai | Vai tro |
| --- | --- | --- |
| `CustomerSupport.Contracts` | Class Library | DTO va hop dong chia se. |
| `CustomerSupport.SupportApi` | ASP.NET Core Web (Minimal API) | REST API host. |
| `CustomerSupport.AssignmentWorker` | .NET Worker Service | Background consumer cho phan cong. |
| `CustomerSupport.NotificationService` | ASP.NET Core Web host | Host SignalR va background consumer khi cac phase tuong ung duoc thuc hien. |

Notification Service dung web host vi SignalR can mot HTTP host; phase tao solution chi tao skeleton, chua them Hub hay consumer. Support API dung Web project rong de tranh endpoint mau khong thuoc yeu cau.

## Project references

```text
CustomerSupport.SupportApi ----------> CustomerSupport.Contracts
CustomerSupport.AssignmentWorker ----> CustomerSupport.Contracts
CustomerSupport.NotificationService -> CustomerSupport.Contracts
```

Contracts khong tham chieu service khac. Khong them project frontend, database, test, shared infrastructure hoac service thu nam.

## Thu muc logic du kien trong project

```text
CustomerSupport.Contracts/
  Dtos/
  Events/

CustomerSupport.SupportApi/
  Endpoints/
  Services/
  Persistence/
  Configuration/

CustomerSupport.AssignmentWorker/
  Consumers/
  Assignment/
  Persistence/
  Configuration/

CustomerSupport.NotificationService/
  Hubs/
  Consumers/
  Configuration/
```

Day la dinh huong thu muc cho cac phase hien thuc; trong Phase 2 chi tao skeleton/folder, khong tao code nghiep vu hay ket noi. Khong tao Persistence/EF Core implementation trong Phase 2.

## Cau hinh .NET

- Tat ca project nham `net10.0`.
- `Directory.Build.props` dung chung target framework va cac thiet lap build can thiet.
- `global.json` chon SDK .NET 10 co san, cho phep patch/feature band tuong thich.
- Cau hinh chay (database, RabbitMQ, URL/port) se duoc doc tu configuration/environment o cac phase tich hop; khong commit secrets.
- Mỗi service se co Dockerfile rieng va docker-compose se duoc bo sung trong phase Docker; khong tao cac file do trong Phase 2.

## Gioi han Phase 2

Phase 2 chi tao solution/project, folder, project references va cau hinh build .NET. Khong trien khai API nghiep vu, RabbitMQ, SignalR, database/EF Core, client hay du lieu mau.
