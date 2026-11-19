# Cloud Run mapping

The local deployment stage uses Docker Compose to pull the image published to
Docker Hub and run it on the Actions runner. A Cloud Run deployment would
replace that stage as follows; this repository does not deploy to Cloud Run.

| Pipeline step | Cloud Run equivalent |
| --- | --- |
| Push image to Docker Hub | Build and push the image to Artifact Registry |
| `docker compose pull` and `docker compose up -d` | Deploy the Artifact Registry image with `gcloud run deploy` |
| Docker Hub username and access token | Authenticate with a Google Cloud service account, preferably using Workload Identity Federation |

The Cloud Run service would need to expose the app's port (`8080`) and use
`GET /health` as its health check path.
