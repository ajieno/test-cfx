# Monorepo SRE Assignment

## Approach
1. Created sample applications in Go and Node.js
2. Implemented CI/CD using GitHub Actions
3. Containerized applications using Docker
4. Used Google Artifact Registry for image storage
5. Deployed to Google Kubernetes Engine
6. Configured public access using LoadBalancer services and nip.io dns

## CI/CD Workflow
1. Triggered on push to main branch
2. Builds Docker images for both services
3. Pushes images to Google Artifact Registry
4. Deploys to GKE cluster:
   - Updates manifests with current image tags
   - Applies Kubernetes configurations
   - Uses LoadBalancer services for public access

## Setup Instructions
### Prerequisites
1. Google Cloud Project
2. GKE cluster
3. Artifact Registry repository
4. Service account with permissions:
   - Artifact Registry Writer
   - Kubernetes Engine Developer

### Secrets Configuration
Set these GitHub secrets:
- `GCP_PROJECT_ID`: GCP project ID
- `GKE_CLUSTER_NAME`: GKE cluster name
- `GKE_CLUSTER_ZONE`: GKE cluster zone
- `ARTIFACT_REGISTRY_REGION`: Artifact Registry location
- `ARTIFACT_REGISTRY_DOMAIN`: Artifact Registry repo name
- `GCP_SA_KEY`: Service account JSON key

### Deployment
1. Push to main branch triggers deployment
2. Verify deployment:
   kubectl get pods
   kubectl get services
3. Update ingress service with (loadbalancer_external_ip).xip.io for Expose the Services Publicly

### Exposed App Publicly
http://35.224.46.25.nip.io/ -> Nodejs app
34.71.77.190.nip.io -> go app
