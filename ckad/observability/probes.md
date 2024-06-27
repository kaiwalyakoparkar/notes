# Probes

- The pod might be in running state but application inside it might still be loading
- Here pod is not truly said to be "ready to use"
- So we use different probes to tie "ready" conditions of pod to the actual statu of application
- **Type:**
    1. HTTP
      ```yaml
      readineProbe:
        httpGet:
          path: /api/ready
          port: 8080
      ```
    2. TCP Socket
      ```yaml
      readineProbe:
        tcpSocket:
          port: 3306
      ```
    3. Exec Command
      ```yaml
      readinesProbe:
        exec:
          command:
            - cat
            - /app/is -r
      ```
- LivenesProbe: This probe help u to verify if the application running in container is healthy
- ReadinesProbe: This probe helps u to keep pod on hold until the application i ready to be used

## Logs

```bash
k logs -f <pod_name> <container_name>
```