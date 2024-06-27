# Jobs

- "restartPolicy" on pod is reponible for continuou retart of the pod even after its executed successfully once
- Job i used to run set of pods to perform set of tasks to completion
- Job config file is similar to pod but with
  ```yaml
  completion: xx
  restartPolicy: Never
  kind: Job
  ```

## Cron Jobs:

- Similar to Job specification but take chedule as a tring
```
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23)
│ │ ┌───────────── day of the month (1 - 31)
│ │ │ ┌───────────── month (1 - 12)
│ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday)
│ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
│ │ │ │ │ 
│ │ │ │ │
* * * * *
```