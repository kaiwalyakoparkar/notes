# Swithching & Routing

## Switching

- Used to connect machines over same network
- 
  ```bash
  ip link
  ```
- 
  ```bash
  ip addr add ..... dev eth0
  ```

## Routing

- Helps to connect machines our different networks
- 
  ```bash
  route
  ```
- 
  ```bash
  ip route add ..... via .....
  ```
- We add gateway in switch to locate the router

## Default Gateway

- Any request to any network outside of the existing network goes to the default set router
- Weather a host can forward packets between interfaces is governed by file:
```bash
cat /proc/sys/net/ipv4/ip_forward
```
- By default value is zero here
- Set this vaule in file from 0 to 1 and packets forward will be allowed
- Also update in /etc/sysctl.conf