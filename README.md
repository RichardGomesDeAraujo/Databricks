<img src="Logo.png" alt="Hands On Data" style="height: 100px; width:115px;"/>



###### by Richard Gomes de Araújo - 25/01/2023



# Deploy de Dados no Synapse do Azure

> O Objetivo deste trabalho é criar um guia para estudo e compreensão do Databricks com o intuito de evoluir na função de Data Engineer.
>
>
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
- [Notebook no Cluster](README.md#Notebook-no-Cluster)
- [Importar Bibliotecas PySpark](README.md#Importar-Bibliotecas-PySpark)
- [Diretório no Notebook com Código](README.md#Diretório-no-Notebook-com-Código)
- [Unidade com Código](README.md#Unidade-com-Código)
- [Comandos de Visualização PySpark](README.md#Comandos-de-Visualização-PySpark)
- [Create Database](README.md#Create-Database)
- [Create Table](README.md#Create-Table)
- [Azure Synapse Analytics](README.md#Azure-Synapse-Analytics)
- [Security](README.md#Security)
- [Servidor Dedicado](README.md#Servidor-Dedicado)
  - [Create Master Key](README.md#Create-Master-Key)
  - [Create Schema](README.md#Create-Schema)
- [Camada de Conexão](README.md#Camada-de-Conexão)
- [Azure Synapse Parameters](README.md#Azure-Synapse-Parameters)
- [Save no Delta](README.md#Save-no-Delta)

---


### Subscription

Siga as instruções do site da Azure para criar uma conta gratuita, que será utilizada para prepararmos o ambiente de trabalho.

Acesse: [**portal.azure.com**](https://portal.azure.com/#home) e faça uma ***subscription*** do tipo ***free trial***.


###### [⏪](README.md#Índice)

---

### Resource Groups

Crie um **Resource Groups** e utilize um nome com a abreviação rg de *Resource Groups* e em seguida algum nome que identifique os dados, ex.: rg-monitorimagens. 

Escolha uma região para armazenar os dados. 

Salve o código da criação do *Resource Groups* para utilizar nos próximos passos.

###### [⏪](README.md#Índice)

---

### Storage Accounts

Crie um ***Storage Accounts*** para criar o seu *Data Lake* e utilize o prefixo st de *Storage Accounts* no nome seguido do nome que identifique os dados, ex.: st-monitorimagens.

Escolha a região para armazenamento e a Performance do tipo *Standard*.

> ❕ IMPORTANTE: em *Advanced*, marque a opção *Data Lake Storage* Gen2 para criar um *Azure Data Lake*.

Salve o código da criação do *Storage Accounts* para utilizar nos próximos passos.


###### [⏪](README.md#Índice)

---

### Azure Active Directory

Crie um ***Azure Active Directory*** para criar um *application* que é um usuário para se conectar entre o Databricks e o *Data Lake*
Utilize o prefixo ap de *application* e o nome que identifique os dados, ex.: apmonitorimagens

> ❕ IMPORTANTE: Após efetuar o registro, anotar o *Application (Client) ID* e anotar o *Directory (tenant) ID*


###### [⏪](README.md#Índice)

---

### Certificates and Secrets

Em seguida, na mesma tela, clique em **Certificates & Secrets** para criar a sua chave.
Utilize o prefixo key seguido do nome que identifique os dados, ex.: keymonitorimagens

Após criado a chave, anote o código gerado da *Value* e o código gerado do *Secret ID*


###### [⏪](README.md#Índice)

---

### Conteiner

Após estes passos, volte ao seu *Storage Accounts* e clique em *Data Lake Storage* para criar um **Conteiner**.
Utilize o prefixo ct seguido do nome que identifique os dados, ex.: ctmonitorimagens

Anote o código gerado para o *Conteiner*.


###### [⏪](README.md#Índice)

---

### Upload de Dados

Após ter criado o *Conteiner*, clique no *Conteiner* e faça um *Upload* de dados navegando em “Meu Computador” para identificar as tabelas que serão carregadas.


###### [⏪](README.md#Índice)

---

### Role Assingments

Enquanto os dados carregam, é necessário ir no **Access Control (IAM)** e atribuir papéis ao *Conteiner* no *Role Assingments*.


- #### Storage Blob Data Contributor

Clique em *Storage Blob Data Contributor* para fazer a atribuição. 

Em seguida clique em *Select Members* e coloque o *application* criado anteriormente, ex.: apmonitorimagens

- #### Storage Blob Data Reader
  
Em Seguida, Atribua o *Storage Blob Data Reader* e coloque o *application* novamente igual ao passo anterior. 

###### [⏪](README.md#Índice)

---

### Permissões no Manage ACL

Em *Manage ACL*, atribua permissões para *Other* de *Read* e *Write* e adicione em *Add principal* o apmonitorimagens e atribua *Read* e *Write* para ele também.

###### [⏪](README.md#Índice)

---

### Databricks Community

Depois disso, se você não tiver uma conta corporativa do *Azure Databricks*, você pode utilizar o *Databricks Community*, para isso, basta se cadastrar com uma conta do Google, Hotmail, ou outras.

###### [⏪](README.md#Índice)

---

### Cluster

Uma vez no ambiente do Databricks, crie um *Cluster* em *Create Cluster* e utilize o prefixo db para referenciar Databricks, ex.: dbmonitorimagenscanal

###### [⏪](README.md#Índice)

---

### Notebook no Cluster

Uma vez criado o *cluster*, vá até *Workspace*, *Users*, e em *Users* deverá ter um *Notebook* previamente criado.
Ao acessar o *Notebook*, vá até o botão *Clear* e clique em *Clear All Outputs*.
No campo *Detached*, procure e clique no dbmonitorimagenscanal para anexar o seu *cluster*.


###### [⏪](README.md#Índice)

---

### Importar Bibliotecas PySpark

Para fazer agregações em PySpark que serão realizadas nos passos abaixo, é necessário importar algumas bibliotecas com os seguintes comandos:

```

from pyspark.sql.functions import *
from pyspark.sql.types import *
from pyspark.sql.window import *

```

###### [⏪](README.md#Índice)
---

### Diretório no Notebook com Código

Em seguida crie um diretório com o seguinte código PySpark:

```python

Dbutils.fs.mkdirs(“/mnt/dadosmonitorimagens”)

```

###### [⏪](README.md#Índice)

---

### Unidade com Código

Em seguida crie a unidade com as seguintes informações: 
1.	Substituir o “xxxxx” pelos códigos que foram anotados anteriormente 
2.	O *oauth2.secret.id* solicitado abaixo será substituído pelo *Value* anotado e não pelo *secret.id* anotado
3.	Na linha do *cliente.endpoint* deve substituir o /xxxx/ pelo código do *Directory ID* anotado anteriormente
4.	Na linha do *source* substitua o nome do *container* antes do @ e o nome do *storage account* depois do @
5.	No *mount_point* informe em qual unidade você deseja montar os dados

```

configs = {“fs.azure.account.auth.type”: “OAuth”,
   “fs.azure.account.oauth.provider.type”: “org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider”,
   “fs.azure.account.oauth2.client.id”: “xxxxxx”,
   “fs.azure.account.oauth2.client.secret”: “xxxx”,
   “fs.azure.account.oauth2.client.endpoint”: “https://login.microsoftonline.com/xxxxxxx/oauth2”
   “fs.azure.createRemoteFileSystemDuringInitialization”: “true”}

dbutils.fs.mount(
source = “abfss://ctmonitorimagens@stmonitorimagens.dfs.core.windows.net/”,
mount_point = “/mnt/dadosmonitorimagens”,
extra_config = configs)

```

Em seguida, ao rodar novamente o comando abaixo, todos os arquivos que foram feitos *upload* no *storage Account* devem aparecer listados:

```

Dbutils.fs.mkdirs(“/mnt/dadosmonitorimagens”)

```

### Comandos de Visualização PySpark

Para ler e visualizar algum dos arquivos carregados no *Data Lake*, execute o comando abaixo:

##### spark.read.format()

```

cl = spark.read.format(‘csv’).options(header=’true’, inferschema=’true’).load(‘/mt/dadosmonitorimagens/TABELA_PEDIDOS.csv’)
cl.display()

```

##### cl.count()

Use o cl.count() para visualizar a quantidade de registros na tabela conforme abaixo:

```

cl.count("tipo_produto).display()

```

##### cl.groupby()

Para agrupar usamos o seguinte comando:

```

cl.groupBy(“tipo_produto”).display()

```


##### cl.agg(count().alias())

Para agregar e nomear a coluna agregada usamos o seguinte comando:

```

cl.agg(count(“*”).alias(“Qtd.”)).display()

```

###### [⏪](README.md#Índice)

---

### Create Database

Crie um Database com os seguintes comandos:

```sql

%sql
Create database if not exists gold_monitorimagens
Location ‘/mnt/dadosmonitorimagens/gold_monitorimages

```
Em Seguida vá até o ícone *Data* no menu da Databricks e verifique em *Databases* que o gold_monitorimagens já está criado e com a tabela criada no Delta.


###### [⏪](README.md#Índice)

---
 
### Create Table

Em seguida crie a tabela com os seguintes comandos:

```sql

%sql
create table if not exists gold_monitorimagens.TbMonitorImagensGold
(
CustomerID string,
CustomerUniqueID string,
CustomerZipCodePrefix Integer,
CustomerCity string,
CustomerState string
) 
using delta
location ‘mnt/dadosmonitorimagens/gold_monitorimagens/TbMonitorImagensGold’

```

Depois execute o comando save para salvar no Delta:

```

cl.write.mode(‘overwrite’).saveAsTable(“gold_monitorimagens.TbMonitorImagensGold”)

```

###### [⏪](README.md#Índice)

---

# Feito tudo isso, começa o processo de escrever no Synapse

> Busque no Access Keys o nome do storage e a key do storage e anotar separadamente para usar posteriormente



### Azure Synapse Analytics

Crie o Azure Synapse Analytics, informe na tela de criação o:
-	Resource Group = rg-monitorimagens
-	Workspace Name = snpmonitorimagens
-	Account Name = stmonitorimagens (observe após este passo, se aparece no File System Name o nome do seu container = ctmonitorimagens)

###### [⏪](README.md#Índice)

---

### Security

No próximo passo irá aparecer a tela de *Security*, onde você terá a opção de alterar o nome do SQL Server Admin Login e poderá determinar uma senha (um password).

###### [⏪](README.md#Índice)

---

### Servidor Dedicado

No Analytics pools, em SQL pools, crie um tipo (*Type*) de servidor que não seja *Serverless*, para termos um servidor dedicado.
Defina na tela Basics de criação:
Dedicated SQL pool name = snpdedicated
Diminua a Performance level para DW200c

Após criado, vá para Overview e clique em *Open Synapse Studio*.

Depois de aberto, verifique em *Data*, *Workspace*, SQL Database o nome do servidor snpdedicated criado acima.

Em seguida, clique com o botão da esquerda sobre o snpdedicated, abra um New SQL Script/Empty Script* e digite o seguinte comando:


#### Create Master Key

```sql

GO
CREATE MASTER KEY ENCRYPTION BY PASSWORD = ‘Jdfcs9017demCloud627kb’;
GO

```

Em seguida digite:

#### Create Schema

```sql

CREATE SCHEMA dvry

```


###### [⏪](README.md#Índice)

---

Feito isso, siga os passos abaixo.

### Camada de Conexão

Começe substituindo os valores nos comandos abaixo:

```

#Azure Storage Account for Polybase

storage_account_name = “stmonitorimagens”
storage_account_key = “xxxxx”  -- substituir pelo código anotado
storage_container_name = “ctmonitorimagens”

temp_dir_url = “wasbs://{}@{}.blob.core.windows.net/”.format(storage_container_name, storage_account_name)

spark_config_key = “fs.azure.account.key.{}.blob.core.windows.net”.format(storage_account_name)
spark_config_value = storage_account_key

spark.conf.set(spark_config_key, spark_config_value)

```

### Azure Synapse Parameters

```

#Azure Synapse parameters

servername = “snpmonitorimagens”
databasename = “snpdedicated”
username = “sqladminuser”
password = “” –Se tiver criado uma senha é só colocar aqui entre aspas

sql_dw_connection_string = “jdbc:sqlserver://{}.database.windows.net:1433;database={};user={}@{};password=
{};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;”.format(servername,databasename,username,password)

```


Substituído os valores, rode o comando acima e siga para o próximo comando para salvar no Synapse:

###### [⏪](README.md#Índice)

---

### Save no Delta

Substituído os valores, rode o comando acima e siga para o próximo comando para salvar no Synapse:

```

#Writing Dataframe to Table on Azure Synapse

new_table_name = “bi. TbMonitorImagensGold”

cl.write \
   .format(“com.databricks.spark.sqldw”) \
   .option(“url”,sql_dw_connection_string) \
   .option(“format_spark_azure_storage_credentials”, “true”) \
   .option(“dbtable”, new_table_name) \
   .option(“tempdir”, temp_dir_url) \
   .save()

```


###### [⏪](README.md#Índice)





