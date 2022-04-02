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
- k3d

## Instalação de pré requisitos

Primeiro certifique-se de ter os [pré requisitos](https://github.com/RLGHISLENI/rotten-potatoes) instalados e configurados em sua máquina.

## Iniciar o Docker na estação

Verifique o status do docker para saber se ele já está rodando na máquina.

```zsh
sudo service docker status
```

Caso não esteja rodando, inicie o docker conforme abaixo:

```zsh
sudo service docker start
```

## Como rodar o projeto no Kubernetes criando Deployment

Utilizando k3d crie um cluster kubernetes conforme o código abaixo:

```zsh
k3d cluster create meucluster --agents 1 --servers 1
```

Usando o `kubectl` execute o manifesto de deployment

```zsh
kubectl apply -f deployment.yaml
```

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