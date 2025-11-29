# – Estudo Orquestração de Containers com Kubernetes (Microserviços, Minikube, Docker, Pods, Services, Replicasets e Deployments)

---

# 📌 **1. Pré‑requisitos**

* **Minikube** instalado
* **kubectl** instalado
* **Docker** (necessário para o driver do Minikube)

Verifique:

```sh
minikube version
kubectl version --client
```

---

# 📁 **2. Estrutura do Projeto**

Sua estrutura atual está organizada em duas partes principais:

### **📦 Estudo Kubernetes / Conceitos Kubernetes**

Contém manifestos separados por recurso:

```
Conceitos Kubernetes/
├── deployments/
├── pods/
├── replicasets/
└── services/
```

### **📦 Estudo Kubernetes / Microserviços em Kubernetes**

Contém os arquivos da aplicação de microserviços:

```
Microserviços em Kubernetes/
├── deployments/
├── namespaces/
└── services/
```

---

# 🧱 **3. Criando o Namespace**

Antes de aplicar qualquer Deployment ou Service que usa o namespace `vote`, você deve criá-lo.

### Criar namespace:

```sh
kubectl apply -f namespace.yaml
```
<img width="980" height="37" alt="image" src="https://github.com/user-attachments/assets/4960f400-da23-4ff9-81ed-b2ed55398f2e" />

### Verificar namespaces:

```sh
kubectl get namespaces
```
<img width="637" height="139" alt="image" src="https://github.com/user-attachments/assets/1fda5c0d-c318-4792-ab1e-2d9179f2a92f" />

---

# 🚀 **4. Aplicando os Deployments**

Para criar todos os Deployments dentro da pasta `/deployments`:

```sh
kubectl apply -f ./deployments --save-config
```
<img width="788" height="103" alt="image" src="https://github.com/user-attachments/assets/118c033b-e693-425d-bac6-e8bfe5562347" />


Verificar se os pods foram criados:

```sh
kubectl get pods -n vote
```
<img width="614" height="146" alt="image" src="https://github.com/user-attachments/assets/d8b603b7-a32a-4a15-b577-08b7d31d240f" />


---

# 🌐 **5. Criando Services**

Após garantir que os Deployments estão funcionando, aplique os Services:

```sh
kubectl apply -f ./services
```
<img width="773" height="35" alt="image" src="https://github.com/user-attachments/assets/3a7e7f1e-95aa-4349-acb4-48b0a2871cae" />

Verificar os services:

```sh
kubectl get svc -n vote
```
<img width="758" height="69" alt="image" src="https://github.com/user-attachments/assets/d82959ef-d20d-44e1-a72e-1f694cf9bcf3" />

---

# 🧪 **6. Verificar Status dos Pods**

```sh
kubectl get all -n vote
```
<img width="753" height="446" alt="image" src="https://github.com/user-attachments/assets/64d079a2-2a0a-472d-9eb9-cf8cb6ae2829" />

Isso mostra Deployments, ReplicaSets e Pods em execução.

---

# 📡 **7. Expor Serviços com Minikube**

Para acessar um serviço exposto (como o `vote` ou `result`):

```sh
minikube service <service-name> -n vote --url
```

Exemplo para expor o frontend:

```sh
minikube service vote-svc -n vote --url
```

Se aparecer:

```
SVC_NOT_FOUND
```

Verifique a lista de services:

```sh
kubectl get svc -n vote
```

---

# 🔍 **8. Comandos Úteis**

### Ver informações detalhadas do Pod

```sh
kubectl describe pod <pod-name> -n vote
```
<img width="1614" height="967" alt="descripe pods" src="https://github.com/user-attachments/assets/e6d868ae-35f7-41fd-99c0-4f5814b787b8" />




### Recriar um Deployment

```sh
kubectl rollout restart deployment <name> -n vote
```

### Deletar tudo no namespace

```sh
kubectl delete all --all -n vote
```

---

# 📦 **9. Inspecionar DNS no Cluster**

Pod dentro do cluster:

```sh
nslookup kubernetes
```

Saída típica:

```
Server: 10.96.0.10
Name: kubernetes.default.svc.cluster.local
Address: 10.96.0.1
```

<img width="721" height="175" alt="nslookup" src="https://github.com/user-attachments/assets/81c02f88-94d0-4e0e-9717-96e3974f91bd" />


---

# 🖥️ **10. Entrando em um Pod**

```sh
kubectl exec -it <pod-name> -n vote -- sh
```
<img width="1615" height="990" alt="kubeclt exec" src="https://github.com/user-attachments/assets/23620e33-352a-4df8-9052-4800dcc9d7d3" />

Para sair do pod:

```sh
exit
```

---

# 🗄️ **11. Verificar IP do Minikube**

```sh
minikube ip
```
<img width="832" height="107" alt="minikube ip" src="https://github.com/user-attachments/assets/3c068b3d-ca86-4cf3-8039-7a763b1599c1" />

Esse IP geralmente é usado para NodePort.

---
