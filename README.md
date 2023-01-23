

<img src="C:/Users/Usuario/Desktop/Lenovo Files/Richard Araujo/1_Preparacao_de_Dados/Imagens/logo.png" alt="Hands On Data" style="height: 100px; width:100px;"/>

# Deploy de Dados no Synapse do Azure
> O Objetivo deste trabalho é criar um guia para estudo e compreensão do Databricks com o intuito de evoluir na função de Data Engineer.


> Abaixo temos um tutorial, passo a passo, de como criar uma estrutuda de dados no Databricks, passando pelo ETL até a ingestão de dados no Synapse do Azure.

> 
## Índice
- [Subscription](README.md#Subscription)
- [Resource](README.md#Resource) Groups
- [Storage](README.md#Storage) Accounts
- [Azure](README.md#Azure) Active Directory
- [Certificates](README.md#Certificates) & Secrets
- [Conteiner](README.md#Conteiner)
- [Upload](README.md#Upload) de Dados
- [Role](README.md#Role) Assingments
  - Storage Blob Data [Contributor](README.md#Storage)
  - Storage Blob Data [Reader](README.md#Storage)
- [Permissões](README.md#Permissões) no Manage ACL
- [Databricks](README.md#Databricks) Community
- [Cluster](README.md#Cluster)
- [Notebook](README.md#Notebook) no Cluster
- [Importar](README.md#Importar) Bibliotecas PySpark
- [Diretório](README.md#Diretório) no notebook com código
- [Unidade](README.md#Unidade) com código
- [Executar](README.md#Executar) Comandos de Visualização
  - [cl.count()](README.md#cl.count())
  - [cl.groupby()](README.md#cl.groupby())
  - [cl.agg(count().alias())](README.md#cl.agg(count().alias()))
  - [cl.display](README.md#cl.display)
- Create [Database](README.md#Create)
- Create [Table](README.md#Create)
- [Security](README.md#Security)
- [Servidor](README.md#Servidor) Dedicado
- [Open](README.md#Open) Synapse Studio
  - Create [Master](README.md#Create) Key
  - Create [Schema](README.md#Create)
- [Escrever](README.md#Escrever) no Synapse
  - Camada de [Conexão](README.md#Camada)
  - Escrever no [Synapse](README.md#Escrever)
- [Save](README.md#Save) no Delta


## Subscription

###### [Voltar ao Índice](README.md#Índice)

## Resource

###### [Voltar ao Índice](README.md#Índice)

## Storage

###### [Voltar ao Índice](README.md#Índice)

## Azure

###### [Voltar ao Índice](README.md#Índice)

## Certificates

###### [Voltar ao Índice](README.md#Índice)

## Conteiner

###### [Voltar ao Índice](README.md#Índice)

## Upload

###### [Voltar ao Índice](README.md#Índice)

## Role

###### [Voltar ao Índice](README.md#Índice)

### Contributor

###### [Voltar ao Índice](README.md#Índice)

### Reader

###### [Voltar ao Índice](README.md#Índice)

## Permissões

###### [Voltar ao Índice](README.md#Índice)

## Databricks

###### [Voltar ao Índice](README.md#Índice)

## Cluster

###### [Voltar ao Índice](README.md#Índice)

## Notebook

###### [Voltar ao Índice](README.md#Índice)

## Importar

###### [Voltar ao Índice](README.md#Índice)

## Diretório

###### [Voltar ao Índice](README.md#Índice)

## Unidade

###### [Voltar ao Índice](README.md#Índice)

## Executar

###### [Voltar ao Índice](README.md#Índice)

### cl.count()

###### [Voltar ao Índice](README.md#Índice)

### cl.groupby()

###### [Voltar ao Índice](README.md#Índice)

### cl.agg(count().alias())

###### [Voltar ao Índice](README.md#Índice)

### cl.display

###### [Voltar ao Índice](README.md#Índice)

## Database

###### [Voltar ao Índice](README.md#Índice)
 
## Table

###### [Voltar ao Índice](README.md#Índice)

## Security

###### [Voltar ao Índice](README.md#Índice)

## Servidor

###### [Voltar ao Índice](README.md#Índice)

## Open

###### [Voltar ao Índice](README.md#Índice)

### Master

###### [Voltar ao Índice](README.md#Índice)

### Schema

###### [Voltar ao Índice](README.md#Índice)

## Escrever

###### [Voltar ao Índice](README.md#Índice)

### Conexão

###### [Voltar ao Índice](README.md#Índice)

### Synapse

###### [Voltar ao Índice](README.md#Índice)

## Save

###### [Voltar ao Índice](README.md#Índice)
