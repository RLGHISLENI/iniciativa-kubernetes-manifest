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

Para este desafio utilizaremos o **k3d** para criação de nosso cluster kubernetes e o **kubectl** para criação de pods, replicasets, services e deployments.

Primiero vamos instalar o **asdf** para podermos controlar todas as versões de pacotes instalados em nossa distribuição linux, permitindo a coexistência de mais de uma versão da mesma ferramenta em nosso sistema operacional.

### **Instalando o asdf**

Abra o terminal na pasta raiz do seu usuário e clone o repositório do asdf

```zsh
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.9.0
```

Abra e edite o arquivo `.bashrc` como permissão de administrador utilizando o editor `nano`

```zsh
sudo nano ~/.bashrc
```

Adicione a instrução abaixo na última linha do arquivo, salve e feche

```zsh
. $HOME/.asdf/asdf.sh
```

Execute o comando abaixo para validar a instalação do asdf

```zsh
asdf info
```

Caso não funcione, reinicie seu terminal e tente novamente.

### **Instalando o k3d e kubectl**

Após a instalação do asdf, abra o terminal e execute a lista de comandos abaixo:

**k3d:**
```zsh
asdf plugin-add k3d && asdf install k3d latest && asdf global k3d latest
```

**kubectl:**
```zsh
asdf plugin-add kubectl && asdf install kubectl latest && asdf global kubectl latest
```

Estes comandos combinados irão realizar a **adição do plugin** k3d/kubectl ao controlador asdf, **intalação** no sistema operacional e definição do escopo de utilizaçõa da **última versão como Global**

Para validar a ação do asdf, utilize o comando descrito abaixo

```zsh
asdf list
```

ou

```zsh
asdf current
``` 
Deverá retornar a lista de ferramentas instaladas e suas versões.

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
k3d cluster create meucluster --agents 1 --servers 1 -p "8080:30000@loadbalancer"
```

Navegue até a pasta `k8s` do projeto e usando o `kubectl` execute o manifesto de deployment

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