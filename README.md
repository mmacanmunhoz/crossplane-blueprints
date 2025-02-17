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


## 🚀 CI/CD - Geração Automática das Configurations

Este repositório conta com um workflow automatizado de CI/CD no GitHub Actions, que empacota e publica as Configurations para o GitHub Container Registry (GHCR).
- O que esse CI/CD faz?

    Sempre que um novo commit ou tag for adicionado, o CI/CD gera e publica a Configuration correspondente.
    Essa Configuration contém todos os providers, functions e compositions necessários para o funcionamento dos blueprints.
    A instalação da Configuration automatiza o provisionamento do Crossplane.

📌 Como instalar a Configuration?

Após o CI/CD gerar a Configuration, basta aplicá-la no cluster para que todos os componentes necessários sejam instalados automaticamente:

kubectl apply -f dependencies/configuration.yaml

Esse comando irá instalar automaticamente:

    Providers (como AWS, GCP, Azure)
    Functions (caso existam funções personalizadas para validações e transformações)
    Compositions (para provisionamento dos recursos)


No caso como estamos usando o github como registry privado, é necessário criar o segredo do github e associa-lo ao configuration para que possamos autenticar no registry privado

```
kubectl create secret docker-registry ghcr-credentials \
  --namespace crossplane-system \
  --docker-server=ghcr.io \
  --docker-username=<username>> \
  --docker-password=<token>
```

```
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: configuration-gh-docdb
  namespace: crossplane-system
spec:
  package: ghcr.io/<organization>/crossplane-pkg/docdb:v4.0.0
  packagePullSecrets:
    - name: ghcr-credentials
``


### 🚀 Aplicação de um Blueprint

Para aplicar um blueprint e provisionar recursos, utilize os manifestos YAML disponíveis no repositório. Exemplo:

```sh
kubectl apply -f blueprints/aws/docdb.yaml
```

---

## 📁 Estrutura do Repositório

```
├── blueprints
│   └── aws
│       └── docdb.yaml
├── configurations
│   └── docdb
│       ├── crossplane.yaml
│       ├── docdb-v1.0.0-composition.yaml
│       ├── docdb-v2.0.0-composition.yaml
│       └── xrd.yaml
├── dependencies
│   ├── configuration.yaml
│   ├── credentials.yaml
│   ├── external-secrets
│   │   ├── configuration.yaml
│   │   └── permission.yaml
│   ├── functions.yaml
│   └── provider.yaml
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

