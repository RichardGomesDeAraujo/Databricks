<img src="Logo.png" alt="Hands On Data" style="height: 100px; width:115px;"/>

# Deploy de Dados no Synapse do Azure
> O Objetivo deste trabalho é criar um guia para estudo e compreensão do Databricks com o intuito de evoluir na função de Data Engineer.


> Abaixo temos um tutorial, passo a passo, de como criar uma estrutuda de dados no Databricks, passando pelo ETL até a ingestão de dados no Synapse do Azure.

> 
## Índice
- [Subscription](README.md#Subscription)
- [Resource Groups](README.md#Resource-Groups)
- [Storage Accounts](README.md#Storage-Accounts)
- [Azure Active Directory](README.md#Azure-Active-Directory)
- [Certificates and Secrets](README.md#Certificates-and-Secrets)
- [Conteiner](README.md#Conteiner)
- [Upload de Dados](README.md#Upload-de-Dados)
- [Role Assingments](README.md#Role-Assingments)
  - [Storage Blob Data Contributor](README.md#Storage-Blob-Data-Contributor)
  - [Storage Blob Data Reader](README.md#Storage-Blob-Data-Reader)
- [Permissões no Manage ACL](README.md#Permissões-no-Manage-ACL)
- [Databricks Community](README.md#Databricks-Community)
- [Cluster](README.md#Cluster)
- [Notebook](README.md#Notebook) no Cluster
- [Importar](README.md#Importar) Bibliotecas PySpark
- [Diretório](README.md#Diretório) no notebook com código
- [Unidade](README.md#Unidade) com código
- [Executar](README.md#Executar) Comandos de Visualização PySpark
- Create [Database](README.md#Database)
- Create [Table](README.md#Table)
- [Security](README.md#Security)
- [Servidor](README.md#Servidor) Dedicado
- [Open](README.md#Open) Synapse Studio
  - Create [Master](README.md#Master) Key
  - Create [Schema](README.md#Schema)
- [Escrever](README.md#Escrever) no Synapse
  - Camada de [Conexão](README.md#Conexão)
  - Escrever no [Synapse](README.md#Synapse)
- [Save](README.md#Save) no Delta

---


## Subscription

Siga as instruções do site da Azure para criar uma conta gratuita, que será utilizada para prepararmos o ambiente de trabalho.

Acesse: [**portal.azure.com**](https://portal.azure.com/#home) e faça uma ***subscription*** do tipo ***free trial***.


###### [⏪](README.md#Índice)

---

## Resource Groups

Crie um **Resource Groups** e utilize um nome com a abreviação rg de *Resource Groups* e em seguida algum nome que identifique os dados, ex.: rg-monitorimagens. 

Escolha uma região para armazenar os dados. 

Salve o código da criação do *Resource Groups* para utilizar nos próximos passos.

###### [⏪](README.md#Índice)

---

## Storage Accounts

Crie um ***Storage Accounts*** para criar o seu *Data Lake* e utilize o prefixo st de *Storage Accounts* no nome seguido do nome que identifique os dados, ex.: st-monitorimagens.

Escolha a região para armazenamento e a Performance do tipo *Standard*.

> ❕ IMPORTANTE: em *Advanced*, marque a opção *Data Lake Storage* Gen2 para criar um *Azure Data Lake*.

Salve o código da criação do *Storage Accounts* para utilizar nos próximos passos.


###### [⏪](README.md#Índice)

---

## Azure Active Directory

Crie um ***Azure Active Directory*** para criar um *application* que é um usuário para se conectar entre o Databricks e o *Data Lake*
Utilize o prefixo ap de *application* e o nome que identifique os dados, ex.: apmonitorimagens

> ❕ IMPORTANTE: Após efetuar o registro, anotar o *Application (Client) ID* e anotar o *Directory (tenant) ID*


###### [⏪](README.md#Índice)

---

## Certificates and Secrets

Em seguida, na mesma tela, clique em **Certificates & Secrets** para criar a sua chave.
Utilize o prefixo key seguido do nome que identifique os dados, ex.: keymonitorimagens

Após criado a chave, anote o código gerado da *Value* e o código gerado do *Secret ID*


###### [⏪](README.md#Índice)

---

## Conteiner

Após estes passos, volte ao seu *Storage Accounts* e clique em *Data Lake Storage* para criar um **Conteiner**.
Utilize o prefixo ct seguido do nome que identifique os dados, ex.: ctmonitorimagens

Anote o código gerado para o *Conteiner*.


###### [⏪](README.md#Índice)

---

## Upload de Dados

Após ter criado o *Conteiner*, clique no *Conteiner* e faça um *Upload* de dados navegando em “Meu Computador” para identificar as tabelas que serão carregadas.


###### [⏪](README.md#Índice)

---

## Role Assingments

Enquanto os dados carregam, é necessário ir no **Access Control (IAM)** e atribuir papéis ao *Conteiner* no *Role Assingments*.


- #### Storage Blob Data Contributo

Clique em **Storage Blob Data Contributor** para fazer a atribuição. 

Em seguida clique em *Select Members* e coloque o *application* criado anteriormente, ex.: apmonitorimagens

- #### Storage Blob Data Reader
  
Em Seguida, Atribua o **Storage Blob Data Reader** e coloque o *application* novamente igual ao passo anterior. 

###### [⏪](README.md#Índice)

---

## Permissões no Manage ACL

Em **Manage ACL**, atribua permissões para *Other* de *Read* e *Write* e adicione em *Add principal* o apmonitorimagens e atribua *Read* e *Write* para ele também.

###### [⏪](README.md#Índice)

---

## Databricks Community

Depois disso, se você não tiver uma conta corporativa do **Azure Databricks**, você pode utilizar o **Databricks Community**, para isso, basta se cadastrar com uma conta do Google, Hotmail, ou outras.

###### [⏪](README.md#Índice)

---

## Cluster

Uma vez no ambiente do Databricks, crie um **Cluster** em *Create Cluster* e utilize o prefixo db para referenciar Databricks, ex.: dbmonitorimagenscanal

###### [⏪](README.md#Índice)

---

## Notebook

Uma vez criado o *cluster*, vá até *Workspace*, *Users*, e em *Users* deverá ter um *Notebook* previamente criado.
Ao acessar o *Notebook*, vá até o botão *Clear* e clique em *Clear All Outputs*.
No campo *Detached*, procure e clique no dbmonitorimagenscanal para anexar o seu *cluster*.


###### [⏪](README.md#Índice)

---

## Diretório

Em seguida crie um diretório com o seguinte código PySpark:

```python
Dbutils.fs.mkdirs(“/mnt/dadosmonitorimagens”)
```

###### [⏪](README.md#Índice)

---

## Unidade

###### [⏪](README.md#Índice)

---

## Executar

###### [⏪](README.md#Índice)

---

### cl.count()

###### [⏪](README.md#Índice)

### cl.groupby()

###### [⏪](README.md#Índice)

### cl.agg(count().alias())

###### [⏪](README.md#Índice)

### cl.display

###### [⏪](README.md#Índice)

---

## Database

###### [⏪](README.md#Índice)

---
 
## Table

###### [⏪](README.md#Índice)

---

## Security

###### [⏪](README.md#Índice)

---

## Servidor

###### [⏪](README.md#Índice)

---

## Open

###### [⏪](README.md#Índice)

---

### Master

###### [⏪](README.md#Índice)

### Schema

###### [⏪](README.md#Índice)

---

## Escrever

###### [⏪](README.md#Índice)

---

### Conexão

###### [⏪](README.md#Índice)

### Synapse

###### [⏪](README.md#Índice)

---

## Save

###### [⏪](README.md#Índice)


