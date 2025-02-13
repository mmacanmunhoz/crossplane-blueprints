# Crossplane Blueprints

## 📌 Visão Geral

O **Crossplane Blueprints** é um conjunto de templates e configurações pré-definidas para provisionamento de infraestrutura usando Crossplane. Esses blueprints permitem criar e gerenciar recursos de forma declarativa através de APIs Kubernetes, facilitando a adoção do *Infrastructure as Code* (IaC) no Kubernetes.

## 📂 Recursos Disponíveis

Este repositório contém blueprints para provisionamento de diferentes serviços e provedores, incluindo:

### ☁️ AWS
- Docdb (Banco de Dados Não Relacional)


### ☁️ GCP
- 

### ☁️ Azure
- 

---

## 🛠️ Requisitos

Para utilizar os blueprints deste repositório, é necessário ter:
- Um cluster Kubernetes configurado
- Crossplane instalado e configurado
- Um provedor de nuvem com as permissões necessárias

### 🔧 Instalação do Crossplane

Se ainda não tiver o Crossplane instalado, siga os passos abaixo:

```sh
kubectl create namespace crossplane-system
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm install crossplane crossplane-stable/crossplane --namespace crossplane-system
```

### 🌍 Configuração de um Provedor (Exemplo AWS)

Após instalar o Crossplane, configure um provedor usando os CRDs apropriados. Exemplo para AWS:

```sh
kubectl apply -f dependencies/provider.yaml
```

Criação de credenciais:

"Criptografe" em base 64 os valores de access-key e secret-key e coloque no arquivo dependencies/credentials.yaml


## 🔧 Aplique as Compositions

Necessário antes de aplicar o blueprint, aplicar as compositions, pois a mesma permitirá que o blueprint seja reconhecido dentro do cluster

```sh
kubectl apply -f compositions/aws/
```


### 🚀 Aplicação de um Blueprint

Para aplicar um blueprint e provisionar recursos, utilize os manifestos YAML disponíveis no repositório. Exemplo:

```sh
kubectl apply -f blueprints/aws/docdb.yaml
```

---

## 📁 Estrutura do Repositório

```
.
├── blueprints
│   └── aws
│       └── docdb.yaml
├── compositions
│   └── aws
│       └── docdb
│           ├── docdb-v1.0.0-composition.yaml
│           ├── docdb-v2.0.0-composition.yaml
│           ├── external-secret.yaml
│           └── xrd.yaml
├── dependencies
│   ├── configuration.yaml
│   ├── credentials.yaml
│   ├── external-secrets
│   │   ├── configuration.yaml
│   │   └── permission.yaml
│   ├── functions.yaml
│   └── provider.yaml
└── README.mdbuições.md
└── README.md
```

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Se deseja adicionar novos blueprints, corrigir erros ou melhorar a documentação, siga estas etapas:

1. **Fork** o repositório
2. Crie uma **branch** para suas alterações (`git checkout -b minha-mudanca`)
3. Faça as modificações e submeta um **Pull Request**
4. Aguarde a revisão e feedback da equipe

---

## 📞 Contato e Suporte

Se tiver dúvidas ou precisar de suporte, entre em contato através das **Issues** do repositório ou participe da comunidade no Slack do Crossplane.

---

✨ *Este projeto segue as melhores práticas de GitOps e infraestrutura declarativa, promovendo um ambiente mais eficiente e escalável!* 🚀

