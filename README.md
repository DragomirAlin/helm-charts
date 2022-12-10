# helm-charts
Public Helm Charts Repository for my applications

## Charts
| Chart name 	| Description 	| 
|------------	|-------------	|
| helm-chart-test           	|   For testing repo purpose          	|   


## Add Repo
```bash
$ helm repo add drg https://charts.dragomiralin.ro/
$ helm repo list
NAME     URL                                            
drg      https://charts.dragomiralin.ro/ 
```

### Test Repo
```bash
$ helm install test-repo drg/helm-chart-test
```