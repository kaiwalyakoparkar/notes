# Deployment Strategy

Services are used to route the traffic among the present deployments

## 1. Blue Green:

- New version deployment is created alongside old versions
- All the traffic is shifted at once.

## 2. Canary:

- Only route small % of traffic to new version pod.