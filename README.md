# 🔷 Vehicle Configurator — .NET Core Microservice

> **ASP.NET Core Web API** microservice for the **Vehicle Configurator** — a B2B portal that lets rental-car companies bulk-purchase, configure, customise, and invoice vehicles.

Part of a **three-stack capstone project**. The same product is also implemented in:

| Stack | Repo |
|---|---|
| ☕ **Java Spring Boot 3** (primary backend) | [`Pranavgawas/VehicleConfigurator-java`](https://github.com/Pranavgawas/VehicleConfigurator-java) |
| 🟢 **React** (frontend, lives on GitHub Pages) | [`Pranavgawas/VehicleConfigurator-react`](https://github.com/Pranavgawas/VehicleConfigurator-react) |

🔗 **Live demo:** [pranavgawas.github.io/VehicleConfigurator-react](https://pranavgawas.github.io/VehicleConfigurator-react/)

---

## ✨ Responsibilities in the System

This service is the **`.NET` leg of the trio**. In the microservices split it typically handles:

- Subset of read/write endpoints alongside the Java service
- Service-to-service communication via REST
- Independent deployability (own database, own scaling)

---

## 🧱 Tech Stack

- **.NET** (ASP.NET Core Web API)
- **Entity Framework Core** + EF Migrations
- **SQL Server** (via `ApplicationDbContext`)
- **JWT Bearer** authentication (`Microsoft.AspNetCore.Authentication.JwtBearer`)
- **Repository pattern** with explicit interfaces (e.g. `IUserRepository`, `IManufacturerRepository`)

---

## 🗂️ Project Structure

```
VehicleConfigurator-dotnet/
├── Controller/
│   ├── UserController.cs
│   ├── ManufacturerController.cs
│   ├── SegmentController.cs
│   ├── VariantController.cs
│   ├── Alternate_ComponentController.cs
│   └── vehicle_detailController.cs
├── DAL/
│   └── SubCompPrice.cs
├── Data/
│   └── ApplicationDbContext.cs
├── Migrations/                  # EF Core migrations
├── Models/
│   ├── User.cs
│   ├── Manufacturer.cs
│   ├── Segment.cs
│   ├── Variant.cs
│   ├── Component.cs
│   ├── Alternate_Component.cs
│   └── Vehicle_detail.cs
├── Repositories/
│   ├── IUserRepository.cs / SQLUserRepository.cs
│   ├── IManufacturerRepository.cs / SQLManufacturerRepository.cs
│   ├── ISegmentRepository.cs / SQLSegmentRepository.cs
│   ├── IVariantRepository.cs / SQLVariantRepository.cs
│   ├── IAlternateComponent.cs / SqlAlternateComponentRepo.cs
│   └── IVehicleDetail.cs / SqlVehicleDetailRepository.cs
├── Properties/
├── Program.cs                   # DI, auth, EF, JWT wiring
├── appsettings.json / appsettings.Development.json
├── demo1.csproj
└── demo1.sln
```

---

## 🚀 Getting Started

### Prerequisites
- .NET SDK **6.0+**
- SQL Server (LocalDB or full instance)

### Setup

```bash
git clone https://github.com/Pranavgawas/VehicleConfigurator-dotnet.git
cd VehicleConfigurator-dotnet

# Restore + build
dotnet restore
dotnet build

# Update DB connection string in appsettings.Development.json, then:
dotnet ef database update

# Run
dotnet run
```

The API will listen on the URL printed by Kestrel (typically `https://localhost:5001`).

---

## 🔐 Auth

JWT Bearer tokens are issued by the user controller and validated by middleware configured in `Program.cs`. Requests to protected routes must include:

```
Authorization: Bearer <token>
```

---

## 🌐 Key Endpoints (sample)

| Method | Route | Purpose |
|---|---|---|
| `GET` | `/api/User/...` | User CRUD |
| `GET` | `/api/Manufacturer/...` | Manufacturers |
| `GET` | `/api/Segment/...` | Vehicle segments |
| `GET` | `/api/Variant/...` | Variants |
| `GET` | `/api/Alternate_Component/GetCompnameByExt/{modelId}` | Exterior components |
| `GET` | `/api/Alternate_Component/GetCompnameByInt/{modelId}` | Interior components |

> See [`Controller/`](./Controller) for the full surface.

---

## 🤝 Contributing

Issues + PRs welcome. Keep public-facing endpoint shapes aligned with [`VehicleConfigurator-java`](https://github.com/Pranavgawas/VehicleConfigurator-java) so the React frontend can talk to either backend.

---

## 📄 License

[MIT](./LICENSE) — © 2026 Pranav Gawas