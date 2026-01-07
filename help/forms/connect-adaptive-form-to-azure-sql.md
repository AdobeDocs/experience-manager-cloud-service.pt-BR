---
Title: How to Connect AEM Adaptive Forms with Azure SQL Storage
Description: Learn how to configure an Azure SQL Database connection in AEM Forms and integrate it with your Adaptive Forms to store or retrieve data efficiently using JDBC.
Keywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 40193d89f2a4ef864a564eb9932403531eaf1ff7
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Conectar um Formulário adaptável ao Armazenamento SQL do Azure

O Forms adaptável no Adobe Experience Manager (AEM) pode se integrar a bancos de dados externos para armazenar ou recuperar dados.
Este artigo descreve como conectar um formulário adaptável a um banco de dados SQL do Azure usando JDBC por meio do AEM as a Cloud Service.

> 
> 
> Este guia se aplica a ambientes AEM as a Cloud Service que não sejam de sandbox com rede avançada ativada.

## Vantagens

A integração do Adaptive Forms com o Azure SQL oferece vários benefícios:

* **Interação de dados em tempo real:** habilita a leitura e gravação ao vivo de dados entre formulários e o banco de dados do Azure.
* **Escalabilidade:** o Azure SQL fornece desempenho de banco de dados escalável adequado para aplicativos de nível empresarial.
* **Armazenamento de dados centralizado:** Mantém os envios de formulários e os dados recuperados armazenados com segurança em um local central.
* **Conformidade de segurança:** aproveita as opções de rede, firewall e criptografia integradas do Azure para garantir comunicação segura.
* **Integração nativa em nuvem:** ideal para arquiteturas modernas e inovadoras que usam o AEM as a Cloud Service.

## Pré-requisitos

* Crie o [Banco de Dados SQL do Azure](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal) e verifique se a **conexão de proxy** está habilitada.

  >[!NOTE]
  >
  > Navegue até: `Azure Portal → SQL Server → Security → Networking → Connectivity` para habilitar **conexão de proxy**.

  ![Criar Azure Db](/help/forms/assets/create-azure-db.png)

* Habilitar a rede avançada [configurada usando um IP de saída dedicado](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address) para o banco de dados do Azure criado.

  >[!NOTE]
  >
  >    Após ativar o IP de saída dedicado. Vá para `Azure Portal → SQL Server → Security → Networking → Public Access` e adicione o IP de saída às regras de firewall.

  ![IP de saída](/help/forms/assets/cretae-azure-db-egress-ip.png)

* Defina o encaminhamento de portas no ambiente de nuvem com:
   * **portOrigin**: Entre `30000–30999`
   * **portDest**: `1433` (porta padrão para o SQL do Azure)
Por exemplo: `portOrigin: 30433 → portDest: 1433`

     > 
     > 
     > Você pode entrar em contato com o suporte da Adobe Cloud Manager para configurar o encaminhamento de portas.


## Etapas para conectar o Adaptive Forms ao Azure SQL

**Etapa1: clonar repositório Git do AEM as a Cloud Service**

1. Abra a linha de comando e escolha um diretório para armazenar seu repositório do AEM as a Cloud Service, como `/cloud-service-repository/`.

1. Execute o comando abaixo para clonar o repositório:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **Onde encontrar essas informações?**

   Para obter as instruções passo a passo sobre como localizar esses detalhes, consulte o artigo &quot;[Acessando o Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=pt-BR#accessing-git)&quot; da Adobe Experience League.

   Quando o comando for concluído com sucesso, você verá uma nova pasta criada no diretório local. Esta pasta é nomeada em homenagem ao seu aplicativo.

1. Abra a pasta do repositório em um editor.

**Etapa2: adicionar JARs necessários**

Inclua a [dependência de driver SQL](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true) no projeto do AEM por meio do pacote `all`.:

>[!NOTE]
>
> Para incluir a dependência SQL em seu projeto, consulte a seção [Dependências do driver SQL](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies).

**Etapa 3: Adicionar configuração JDBC**

1. Navegue até o seguinte diretório em seu `<application folder>`, onde a configuração OSGi do pool JDBC deve ser colocada:

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**Etapa 4: Criar o Arquivo de Configuração de Conexão SQL do Azure**

1. Crie o arquivo:

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. Adicione as linhas de código abaixo:

   ```json
   {
   "datasource.name": "azuredbshr",
   "jdbc.driver.class": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
   "jdbc.username": "<azureuser>",
   "jdbc.connection.uri": "jdbc:sqlserver://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30433;database=testdb;user=<azureuser>;password=<azurepassword>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;",
   "jdbc.password": "******",
   "jdbc.validation.query": "SELECT 1"
       }
   ```

   > 
   >
   > Substitua `jdbc.username` pelo nome de usuário real do Azure e `jdbc.password` pela senha segura real.

**Etapa 5: confirmar e enviar as alterações**

Abra o terminal e execute os comandos abaixo:

```bash
git add .
git commit -m "<commit message>"
git push 
```

**Etapa 6: implantar as alterações via pipeline de Cloud Manager**

1. Faça logon no **AEM Cloud Manager**.
1. Navegue até o projeto e execute o pipeline para implantar as alterações.

**Etapa 7: Criar um Modelo de Dados de Formulário (FDM)**

Quando a configuração do AEM e do Azure for concluída e as alterações no código forem implantadas:

1. Vá para a instância do autor do AEM.
1. Navegue até **Ferramentas** > **Forms** > **Integrações de Dados**.
1. Criar novo **Modelo de Dados de Formulário**.
1. Na guia **Fontes de dados**, selecione a configuração JDBC criada.
1. Clique em **[!UICONTROL Criar]** e verifique a conexão.

![Criar modelo de dados de formulário](/help/forms/assets/create-azure-sql-fdm.png)

**Etapa 8: usar o FDM criado em um Formulário Adaptável**

1. Abra um Formulário adaptável no modo de edição.
1. Selecione o FDM criado na etapa anterior como o modelo de dados.
1. Use [associações de dados para conectar campos de formulário com a fonte de dados SQL do Azure](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services) e configurar a ação de envio.

## Práticas recomendadas

* Use o **gerenciamento de segredos** para evitar a codificação rígida de senhas em arquivos de configuração.
* Roteie regularmente as credenciais do banco de dados e atualize a configuração com segurança.
* Monitore logs de conectividade JDBC em busca de falhas e latência.
* Siga as práticas recomendadas do Azure para proteger bancos de dados SQL e configurações de firewall.
* Evite usar contas de banco de dados de alto privilégio para acessar formulários.

## Artigos relacionados

{{af-submit-action}}