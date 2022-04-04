# Manifestos - Iniciativa Kubernetes 

Desenvolvimento de exemplos práticos utilizando imagem docker orquestrada por um cluster kubernetes através do k3d e kubectl.

## Pré requisitos

- Linux
- Terminal
- VSCode
- Docker
- Git
- ASDF
- kubectl
- [kubectx](https://github.com/ahmetb/kubectx)
- k3d

## Instalação de pré requisitos e inicialização do Docker

Primeiro certifique-se de ter os [pré requisitos](https://github.com/RLGHISLENI/rotten-potatoes) instalados e configurados em sua máquina.

## Como criar os pods no Kubernetes

Voce pode criar somente os pods no cluster kubernetes

```zsh
# Cria pods
kubectl apply -f pod.yaml

# Exibe os pods
kubectl get pods

# Exibe descrição completa do pod
kubectl describe pod/meupod

# Executa o pod
kubectl port-forward pod/meupod 8080:80

# Exclui o pod
kubectl delete pod meupod
# ou
kubectl delete -f pod.yaml
```

> **Importante:** Caso um pod sejá excluído ele morrerá e não voltará a ser executado a menos que seja criado manualmente. 
>
> Por este motivo não devemos criar pods sem a criação de um replicaset para gerencia-los e mantê-los sempre em execução.

## Como criar replicaset no Kubernetes

Voce pode criar somente uma replicaset no cluster kubernetes

```zsh
# Cria replicasets
kubectl apply -f replicaset.yaml

# Exibe as replicasets
kubectl get replicaset

# Exclui as replicasets contidas no manifesto
kubectl delete -f replicaset.yaml
```

## Como rodar o projeto no Kubernetes criando Deployment

Utilizando k3d crie um cluster kubernetes conforme o código abaixo:

```zsh
# Cria o cluster com load balancer e faz o bind com a porta 30000
k3d cluster create meucluster --agents 1 --servers 1 -p "8080:30000@loadbalancer"
```
> **ATENÇÃO**: Para funcionar o bind entre a porta 8080 -> 30000 você deverá criar um `service` e definir o **`type`** como **`NodePort`** no arquivo `deployment.yaml`.

Usando o `kubectl` aplique o manifesto de deployment

```zsh
kubectl apply -f deployment.yaml
```

## Comandos úteis

Veja alguns comandos úteis no uso de containers e kubernetes

```zsh
# Exibe informações do cluster kubernetes
kubectl cluster-info

# Exibe os nodes
kubectl get nodes

# Exibe os serviços
kubectl get service

# Exibe todos os objetos criados
kubectl get all

# Mostra a lista de recursos e suas versões
kubectl api-resources

# Altera a quantidade de replicaset por linha de comando
kubectl scale replicaset meureplicaset --replicas 10

# Altera a imagem definida no deployment através da linha de comando
kubectl set image deployment meudeployment web=kubedevio/web-page:green

# Exibe os pods de sistema
kubectl get pods --namespace kube-system
```

> Para acessar sua aplicação que estrará no ar utilizando todo o poder dos containers docker e sendo orquestrada pelo kubernetes, abra o navegador de sua preferência na url _**http://localhost:8080/**_ e o projeto será apresentado.