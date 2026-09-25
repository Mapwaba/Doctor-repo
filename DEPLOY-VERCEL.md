# Deploying the Doctor app to Vercel

The API must already be running on Render. See `DEPLOY-RENDER.md` in [Medical-api-repo](https://github.com/Mapwaba/Medical-api-repo).

1. In Vercel, go to **Add New → Project** and import `Mapwaba/Doctor-repo`.
2. Set these options:
   - **Project name:** `landadoc-doctor`. This gives `https://landadoc-doctor.vercel.app`, which is the URL the API's CORS settings expect.
   - **Root Directory:** `src/Frontend/Doctor`
   - **Framework Preset:** Other. Leave the build and output settings empty, because [src/Frontend/Doctor/vercel.json](src/Frontend/Doctor/vercel.json) provides them.
   - Keep **Include files outside the root directory** turned on (it's the default). The build needs `src/Frontend/LandaDoc.Frontend.Shared`, `src/LandaDoc.Shared` and `deploy/`.
3. Click **Deploy**. The build script [deploy/vercel/build.sh](deploy/vercel/build.sh) does three things:
   - installs the .NET 9 SDK, which takes about a minute;
   - publishes the app;
   - replaces `appsettings.Production.json` with [deploy/vercel/appsettings.Production.json](deploy/vercel/appsettings.Production.json), which holds the Render API URLs.

## If URLs differ

- **Render gave a service a different URL** (for example with a suffix): update that URL in `deploy/vercel/appsettings.Production.json` and push.
- **This app got a different Vercel URL:** in Render, update the matching `Cors__AllowedOrigins__*` value in the `landadoc-shared` env group.

Every push to `main` redeploys automatically.
