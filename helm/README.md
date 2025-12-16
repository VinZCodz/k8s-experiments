# What is Helm?
A bundler or a package manager for k8s objects.
<img width="1773" height="845" alt="image" src="https://github.com/user-attachments/assets/95408a74-00e3-41e3-95d8-8de0019e74ed" />

# Getting the local/remote charts.

- Help

```
helm version
helm create -h 
```
- Create

```
helm create [CHART_NAME]
helm create sample_chart
```

<img width="656" height="300" alt="image" src="https://github.com/user-attachments/assets/08b3f05d-ae36-43dd-b1b6-1d1c4036aadb" />****

- Adds a chart repository to your Helm configuration, allowing you to search and install charts from it. 
```
helm repo add [NAME] [URL] 
helm repo add bitnami https://charts.bitnami.com/bitnami
```

- Run periodically to update/get latest chart
```
helm repo update 
```

- Retrieves a chart package from a repository and downloads it to your local machine as a compressed archive. Use --untar to extract.

```
helm pull [REPO_NAME]/[CHART_NAME] --untar 
helm pull bitnami/mysql --untar
helm pull https://example.com/charts/chartname-1.2.3.tgz
```
# How Helm Works?
<img width="604" height="465" alt="image" src="https://github.com/user-attachments/assets/49772351-79d2-41d4-a99d-12219e4f38c7" />

# CRUD on helm release.

### Creating the release 

- Check for syntax error, lint before install
- Navigate to the directory containing your Helm chart (which must contain a Chart.yaml file) and run the command, specifying the path to the chart: 
```
helm lint <path-to-chart>
helm lint .
```
- Installs a new chart in the Kubernetes cluster and creates a new release.
```
helm install [RELEASE_NAME] [CHART_NAME] 
helm install my-nginx bitnami/nginx
```
<img width="849" height="329" alt="image" src="https://github.com/user-attachments/assets/5bc1fcde-60cc-4fee-8089-bf283ea61849" />

### Read the release in the cluster
- Get a specific release or Lists all installed releases in the specified namespace
- Use -A or --all-namespaces to list releases across all namespaces.
```
helm status [RELEASE_NAME]
helm ls
```

### Updating/Revision of the release.
- Upgrades an existing release to a new version of a chart or updates its configuration. Via, either by chart yaml file or --set cmd
```
helm upgrade [RELEASE_NAME] [CHART_NAME]
helm upgrade my-nginx bitnami/nginx --set image.tag=1.21.0
```

- Note: The --dry-run flag is useful for testing an upgrade without actually deploying the changes to the cluster.
```
helm upgrade my-nginx bitnami/nginx --set image.tag=1.21.0 --dry-run
```

- Get the revision history of a release.
```
helm history [RELEASE_NAME]
```

### Rollback the release to prev revision.
```
helm rollback [RELEASE_NAME] [REVISION_NUMBER]
helm rollback my-nginx 1
```

### Delete the release
- Uninstalls a release and removes all associated Kubernetes resources.

```
helm uninstall [RELEASE_NAME]
helm uninstall my-nginx
```

- Note: By default, this command removes the release record; use the --keep-history flag to retain the history for auditing or potential rollbacks. 
```
helm uninstall [RELEASE_NAME] --keep-history
```
# Final difference on deploying a single micro service? 

<img width="744" height="435" alt="image" src="https://github.com/user-attachments/assets/d281bc90-468c-4f0c-8e54-b7f084278ee8" />
