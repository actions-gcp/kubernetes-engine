# Update Kubernetes Engine deployment image

This [GitHub Action][action] changes the Docker image associated with
a [Kubernetes Engine][gke] deployment. It can be used to deploy a new
image built and pushed in earlier steps of a workflow.

`kubernetes-engine/set-deployment-image` requires a [service account][sa]
with permissions to update deployments in Kubernetes Engine. A JSON key
for that service account should be stored as a GitHub secret and supplied
as the `key` input.

## Inputs

| Name          | Description                     |
| ------------- | ------------------------------- |
| *project*     | Google Cloud project ID         |
| *location*    | Google Cloud location           |
| *cluster*     | Kubernetes Engine cluster name  |
| *namespace*   | Kubernetes namespace            |
| *deployment*  | Kubernetes deployment name      |
| *container*   | Deployment container name       |
| *image*       | Docker image name               |
| *key*         | JSON [service account key][key] |

## Usage

```yaml
      - uses: actions-gcp/kubernetes-engine/set-deployment-image@master
        with:
          project:    <project-id>
          location:   us-west1-a
          cluster:    test-cluster
          namespace:  default
          deployment: test-deployment
          container:  test-container
          image:      gcr.io/<project-id>/test:${{ github.sha }}
          key:        ${{ secrets.SERVICE_ACCOUNT_KEY }}

```

[action]: https://github.com/features/actions
[gke]:    https://cloud.google.com/kubernetes-engine
[sa]:     https://cloud.google.com/compute/docs/access/service-accounts
[key]:    https://console.cloud.google.com/apis/credentials/serviceaccountkey
