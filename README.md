## Commands CheatSheet
#### Nano
```bash
Ctrl + G: Display Nano's help menu.
Ctrl + K: Cut the current line.
Ctrl + U: Paste the cut text.
Ctrl + C: Display current line and column number.
Ctrl + P: Move cursor to the previous line.
Ctrl + N: Move cursor to the next line.
Ctrl + A: Move cursor to the beginning of the current line.
Ctrl + E: Move cursor to the end of the current line.
Ctrl + \: Move cursor to a specific line number.
Ctrl + W: Search for text.
Alt + W: Repeat search in the opposite direction.
Ctrl + \: Replace text.
```
#### UNIX
```bash
whoami: Get current user
```

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
#### ServiceAccounts
User account is used by humans, service account is used by applications.
SA creates a secret with the token that you have to use from the applications in the header "Autorization: Bearer token"
- kubectl commands
```bash
k create serviceaccount name
k describe serviceaccount name #to get the related secret name with the token
k create token sa-name # From 1.24 the token is not auto-generated and now is time bound
```
#### Resource Request
- Memory: M/G/K/Gi/Mi/Ki
- CPU: 1/100m
```yaml
...
kind: Pod
...
spec:
  containers:
  - name:
    resources:
      requests:
        memory: "4Gi"
        cpu: 2
      limits:
        memory:
        cpu:
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