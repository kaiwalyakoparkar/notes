# DNS

- We can name an ip address and ping it directly
- We can set that name here: `/etc/hosts`
- We can see the name of the host using:
  ```bash
  hostname
  ```
- Translating hostname to iip address is called as **Name Resolution**
- DNS has host & name resolution files for all machines
- It is stored at `/etc/resolv.conf`
- The order of choosing which record to choose between hosts & DNS is saved in: `/etc/nsswitch.conf`
- You can add search entry in `/etc/resolv.conf` so it can smartly detect what you mean: 
  ```bash
  ping web
  ```
which is, search mycompany.com

## Record Types:

1. A: Records ip to hostname
2. AAAA: Records ipv6 to hostname
3. CNAME: Records name to a name

## nslookup

- Used to query hostname from DNS server
- Only DNS server & no local host files

## dig

- Returns DNS record in more detail

## Network Namespace:

- Create network namespace using
- 
  ```bash
  ip netns add <name>
  ```
- Viewing namespaces
  ```bash
  ip netns
  ```
- 
  ```bash
  ip netns exec <name> ip link
  ```
