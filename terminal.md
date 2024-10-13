# ~/.bashrc

```
alias k=kubectl

kget()  {
  kubectl get $@
}
  
kdes()  {
  kubectl describe $@
}

kns() {
  kubectl config set-context $(kubectl config current-context) --namespace=$1
}

source <(kubectl completion bash)
complete -F __start_kubectl k

export dry="--dry-run=client -o yaml"

export force="--grace-period 0 --force"
```

# ~/.vimrc

```
set tabstop=2
set expandtab
set clipboard=unnamedplus
```