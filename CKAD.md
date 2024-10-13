## Kubernetes
#### Command and Args

![commands](img/command.webp)

`command`: Setting the Primary Command
- Think of command as the heart of the action, defining the main command to be run within a container.
- Specify it as an array of strings, with each element representing a part of the command.
```yaml
command: ["echo", "Hello from the container!"]
```
`args`: Providing Additional Arguments
- Need to pass extra information to the command? That’s where args come in.
```yaml
args: ["This message is brought to you by args."]
```
#### Security Contexts
Can be configured at the POD level or the CONTAINER level.
- For the POD
```yaml
...
kind: Pod
...
spec:
    securityContext:
        runAsUser: 1000
```
- For the CONTAINER. Capabilities are only supported at the container level.
```yaml
...
kind: Pod
...
spec:
    containers:
        securityContext:
            runAsUser: 1000
            capabilities: 
                add: ["MAC_ADMIN"]
```

## Docker
#### Users
- When running the container
```bash
docker run --user=1000 ubuntu sleep 3600
docker run --cap-add MAC_ADMIN
docker run --cap-remove KILL
```
- Or from the Dockerfile
```dockerfile
FROM ubuntu
USER 1000
```