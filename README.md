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

## Package and Publish to this repository by Github Actions
```yaml
name: Package and Publish Helm Chart
on:
  push:
    paths:
      - helm-chart/**
  pull_request:
    branches: [ main ]
jobs:
  helm-chart:
    runs-on: ubuntu-20.04
    steps:
      - name: Chart Checkout
        uses: actions/checkout@v2
      - name: Helm Installation
        uses: azure/setup-helm@v1.1
        with:
          version: v3.7.0
      - name: Helm Repository Checkout
        uses: actions/checkout@v2
        with:
          repository: DragomirAlin/helm-charts
          token: ${{ secrets.BOT_GH_TOKEN }}
          fetch-depth: 0
          persist-credentials: true
          ref: main
          path: helm-charts
      - name: Helm Package
        run: helm package yourchart --version "0.0.1+<version>" -d helm-charts
      - name: Helm Push
        env:
          GITHUB_TOKEN: ${{ secrets.BOT_GH_TOKEN }}
        run: |
          git config --global user.email "bot@<yourbotemail>"
          git config --global user.name "Helm Bot"
          CHART_PACKAGE_NAME="yourchart-0.0.1+<version>.tgz"
          cd helm-charts
          git add "$CHART_PACKAGE_NAME"
          git commit -m "$CHART_PACKAGE_NAME"
          git push origin main
```