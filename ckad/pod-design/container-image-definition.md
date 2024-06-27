# Container Image Definition

- Use alpine iages to make the Docker image size smaller
- Start from a base OS or another image
- Intall all dependencie
- Copy source code
- Specify Entrypoint
- Image i built as a layered architecture
- Dockerfile should always start with `FROM`
- 
  ```bash
  docker build -t <name> /path/to/Dockerfile
  ```
- Here `8282` is host port and `8080` is container port
  ```bash
  docker run -p 8282:8080 <name>
  ```
- 
  ```bash
  docker run <image_name> cat /etc/*release*
  ```