# Labels and Selectios

## Lables

- Labels are properties attached to each item.

## Selectors

- Selectors help us filter using these labels.

```
kubectl get pods --selector app=App1
```
- Get the count using `--no-headers | wc -l`