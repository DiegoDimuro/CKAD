## Tema
Texto
- Bullet
```yaml
...
rules:
- apiGroups: ['policy']
  resources: ['podsecuritypolicies']
  verbs:     ['use']
  resourceNames:
  - example
...
```