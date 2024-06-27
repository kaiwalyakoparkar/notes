# Helm

- A template is created for the manifest files with placeholders in `{{}}`
- The values are stored in seperate yaml file
- Together templates and values form helm charts
- Charts can be found at `artifactshub.io`
- Can also search using command 
  ```bash
  helm search hub <name>
  ```
- Install chart
  ```bash
  helm install <release> <chart_name>
  ```

## Some Helm Commands

```bash
helm list
```
```bash
helm uninstall my-release
```
```bash
helm pull --untar <name>
```
```bash
helm install release ./path
```
```bash
helm repo list
```
```bash
helm install <release_name> <chart_name>
```