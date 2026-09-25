# LandaDoc Doctor

The Doctor web app for LandaDoc, where doctors manage their schedule, appointments and reviews. It's a standalone Blazor WebAssembly app.

## Layout

| Path | Contents |
|---|---|
| `src/Frontend/Doctor` | The app (`LandaDoc.Doctor.csproj`) |
| `src/Frontend/LandaDoc.Frontend.Shared` | API clients, auth, SignalR hub client and shared components. The same code is copied into the other frontend repos. |
| `src/LandaDoc.Shared` | DTOs, events and enums. **This is a copy.** The master copy is in [Medical-api-repo](https://github.com/Mapwaba/Medical-api-repo). |

## Related repos

| Repo | Contents |
|---|---|
| [Medical-api-repo](https://github.com/Mapwaba/Medical-api-repo) | Backend services |
| [Patient-repo](https://github.com/Mapwaba/Patient-repo) | Patient web app |
| [Doctor-repo](https://github.com/Mapwaba/Doctor-repo) | Doctor web app |
| [Admin-repo](https://github.com/Mapwaba/Admin-repo) | Admin web app |

## Keeping shared code in sync

- **`src/LandaDoc.Shared`:** when the API changes a DTO or enum, copy the API repo's `src/LandaDoc.Shared` over this one.
- **`src/Frontend/LandaDoc.Frontend.Shared`:** the Patient, Doctor and Admin repos each have a copy. If you fix something here that the other apps also use, copy it to their repos too.

## Running locally

Requires the .NET 9 SDK. Start the API first by running `run-all.ps1` in Medical-api-repo. Then:

```powershell
dotnet run --project src/Frontend/Doctor/LandaDoc.Doctor.csproj   # http://localhost:5003
```

Local API addresses are in `src/Frontend/Doctor/wwwroot/appsettings.json`.

## Deploying

- **Vercel:** [DEPLOY-VERCEL.md](DEPLOY-VERCEL.md).
- **Self-hosted (Docker + nginx):**
  `docker build -f docker/Dockerfile.wasm --build-arg PROJECT_PATH=src/Frontend/Doctor/LandaDoc.Doctor.csproj -t landadoc-doctor .`
  This build uses `wwwroot/appsettings.Production.json`, which points at `https://api.landadoc.fr`.
