---
title: Chaves gerenciadas pelo cliente para o AEM as a Cloud Service
description: Saiba como gerenciar chaves de criptografia para o AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
source-git-commit: d00a3099d5468c711ed80a69d74f0a3d51f24672
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# Configuração de chaves gerenciadas pelo cliente para AEM as a Cloud Service {#cusomer-managed-keys-for-aem-as-a-cloud-service}

Atualmente, a AEM as a Cloud Service armazena dados do cliente no Armazenamento Azure Blob e no MongoDB, utilizando chaves de criptografia gerenciadas por provedor por padrão para proteger os dados. Embora essa configuração atenda às necessidades de segurança de muitas organizações, as empresas de setores regulamentados ou que exigem soberania aprimorada de dados podem buscar maior controle sobre suas práticas de criptografia. Para organizações que priorizam a segurança de dados, a conformidade e a capacidade de gerenciar suas chaves de criptografia, a solução CMK (Customer-Managed Keys, chaves gerenciadas pelo cliente) oferece um aprimoramento essencial.

## O problema que está sendo resolvido {#the-problem-being-solved}

Chaves gerenciadas pelo provedor podem criar preocupações para empresas em setores como financeiro, saúde e governo, onde normas rigorosas exigem controle abrangente sobre a segurança dos dados. Sem controle sobre o gerenciamento de chaves, as organizações enfrentam desafios para atender aos requisitos de conformidade, implementar políticas personalizadas de segurança e garantir a total soberania dos dados.

A introdução do CMK (Customer-Managed Keys, chaves gerenciadas pelo cliente) soluciona essas preocupações ao capacitar os clientes de AEM com controle total sobre suas chaves de criptografia. Ao autenticar por meio da Microsoft Entra ID (antigo Azure Ative Diretory), o AEM CS se conecta com segurança ao Cofre de Chaves do Azure do cliente, permitindo que eles gerenciem o ciclo de vida de suas chaves de criptografia — abrangendo criação, rotação e revogação de chaves.

A CMK oferece várias vantagens:

* **Segurança aprimorada:** os clientes podem garantir que suas práticas de criptografia atendam a requisitos específicos de segurança, dando-lhes tranquilidade sobre a proteção de dados.
* **Flexibilidade de conformidade:** com controle total sobre o ciclo de vida da chave, as empresas podem se adaptar facilmente a padrões normativos em evolução, como GDPR, HIPAA ou CCPA, garantindo que sua postura de conformidade permaneça forte.
* **Integração perfeita:** a solução CMK integra-se diretamente ao Armazenamento Azure Blob e ao MongoDB no AEM CS, garantindo que não haja interrupção das operações de armazenamento ou da usabilidade e, ao mesmo tempo, fornecendo aos clientes recursos avançados de criptografia.

Com a adoção do CMK, os clientes podem aumentar o controle sobre suas práticas de segurança e criptografia de dados, aprimorando a conformidade e reduzindo riscos, tudo isso enquanto continuam desfrutando da escalabilidade e flexibilidade do AEM CS.

O AEM as a Cloud Service permite trazer suas próprias chaves de criptografia para criptografar dados em repouso. Este guia fornece etapas para configurar uma chave gerenciada pelo cliente (CMK) no Cofre de Chaves do Azure para AEM as a Cloud Service.

>[!WARNING]
>
>Após configurar o CMK, não é possível reverter para chaves gerenciadas pelo sistema. Você é responsável por gerenciar com segurança suas chaves e fornecer acesso ao Cofre da Chave, Chave e aplicativo CMK no Azure para evitar a perda de acesso aos seus dados.

Você também será guiado pelas seguintes etapas para criar e configurar a infraestrutura necessária:

1. Configurar o ambiente
1. Obter uma ID de aplicativo do Adobe
1. Criar um novo grupo de recursos
1. Criar um cofre de chaves
1. Conceder acesso de Adobe ao cofre de chaves
1. Criar uma chave de criptografia

Você precisará compartilhar o URL do cofre de chaves, o nome da chave de criptografia e as informações sobre o cofre de chaves com o Adobe.

## Configurar o ambiente {#setup-your-environment}

A Interface de Linha de Comando (CLI) do Azure é o único requisito para este guia. Se você ainda não tiver o Azure CLI instalado, siga as instruções oficiais de instalação [aqui](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).

Antes de continuar com o restante deste guia, faça login na CLI com `az login`.

>[!NOTE]
>
>Embora este guia use a CLI do Azure, é possível executar as mesmas operações por meio do console do Azure. Se preferir usar o console do Azure, use os comandos abaixo como referência.

## Obter uma ID de aplicativo do Adobe {#obtain-an-application-id-from-adobe}

O Adobe fornecerá uma ID do aplicativo Entra necessária no restante deste guia. Se você ainda não tiver uma ID do aplicativo, entre em contato com o Adobe para obter uma.

## Criar um novo grupo de recursos {#create-a-new-resource-group}

Crie um novo grupo de recursos em um local de sua escolha.

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

Se você já tiver um grupo de recursos, sinta-se à vontade para usá-lo. No restante deste guia, o local do grupo de recursos e seu nome são identificados com `$location` e `$resourceGroup`, respectivamente.

## Criar um Cofre de Chaves {#create-a-key-vault}

Será necessário criar um cofre de chaves para conter sua chave de criptografia. O cofre de chaves deve ter a proteção de limpeza habilitada. A proteção de limpeza é necessária para criptografar dados em repouso de outros serviços do Azure. O acesso à rede pública também deve ser habilitado para garantir que o locatário do Adobe possa acessar o cofre de chaves.

>[!IMPORTANT]
>A criação do Cofre da Chave com Acesso de Rede Pública desativado impõe que todas as operações relacionadas ao Cofre da Chave, como Criação ou Rotação de Chaves, tenham que ser executadas de um ambiente que tenha acesso de rede ao Cofre da Chave - por exemplo, uma VM que possa acessar o Cofre da Chave.

```powershell
# Reuse this information from the previous step.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Choose a name for the key vault.
$keyVaultName="<KEY VAULT NAME>"

# Create the key vault.
az keyvault create `
  --location $location `
  --resource-group $resourceGroup `
  --name $keyVaultName `
  --default-action=Deny `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Disabled
```

## Conceder acesso de Adobe ao Cofre da Chave {#grant-adone-access-to-the-key-vault}

Nesta etapa, você permitirá que o Adobe acesse seu cofre de chaves por meio de um aplicativo Entra. A ID do aplicativo Entra já deve ter sido fornecida pelo Adobe.

Primeiro, você deve criar uma entidade de serviço anexada ao aplicativo Entra e atribuir a ela as funções **Reader do Cofre de Chaves** e **Usuário da Criptografia do Cofre de Chaves**. As funções estão limitadas ao cofre de chaves criado neste guia.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# The application ID is provided by Adobe.
$appId="<APPLICATION ID>"

# Retrieve the ID of the key vault.
$keyVaultId=(az keyvault show --resource-group $resourceGroup --name $keyVaultName --query id --output tsv)

# Create a new service principal.
$servicePrincipalId=(az ad sp create --id $appId --query id --out tsv)

# Assign the roles to the service principal.
az role assignment create --assignee $servicePrincipalId --role "Key Vault Reader" --scope $keyVaultId
az role assignment create --assignee $servicePrincipalId --role "Key Vault Crypto User" --scope $keyVaultId
```

## Criar uma chave de criptografia {#create-an-ecryption-key}

Por fim, você pode criar uma chave de criptografia no cofre de chaves. Observe que você precisará da função **Criptografador do Cofre de Chaves** para concluir esta etapa. Se o usuário conectado não tiver essa função, entre em contato com o administrador do sistema para que essa função seja concedida a você ou peça a alguém que já tenha essa função para concluir esta etapa para você.

O acesso de rede ao cofre de chaves é necessário para criar a chave de criptografia. Primeiro, verifique se você pode acessar o cofre de chaves e prossiga com a criação da chave:

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Compartilhar as informações do Cofre de Chaves {#share-the-key-vault-information}

Neste ponto, você está pronto. Você só precisa compartilhar algumas informações necessárias com o Adobe, que cuidará da configuração do seu ambiente para você.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# Retrieve the URL of your key vault.
$keyVaultUri=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.vaultUri `
    --output tsv)

# In addition we would need the tenantId and the subscriptionId in order to setup the connection.
$tenantId=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.tenantId `
    --output tsv)
$subscriptionId="<Subscription ID>"
```


## Implicações da revogação do acesso à chave {#implications-of-revoking-key-access}

Revogar ou desabilitar o acesso ao Cofre da chave, chave ou aplicativo CMK pode resultar em interrupções significativas, que incluem alterações nas operações da sua plataforma. Depois que essas chaves forem desativadas, os dados na Platform poderão se tornar inacessíveis e qualquer operação downstream que depende desses dados deixará de funcionar. É fundamental entender totalmente os impactos downstream antes de fazer qualquer alteração nas principais configurações.

Se você decidir revogar o acesso da Platform aos seus dados, poderá fazê-lo removendo a função de usuário associada ao aplicativo do Cofre de Chaves no Azure.

## Próximas etapas {#next-steps}

Adobe de contato e compartilhamento:

* O URL do cofre de chaves. Você a recuperou nesta etapa e a salvou na variável `$keyVaultUri`.
* O nome da chave de criptografia. Você criou a chave em uma etapa anterior e a salvou na variável `$keyName`.
* Os `$resourceGroup`, `$subscriptionId` e `$tenantId` que são necessários para configurar a conexão com o cofre de chaves.

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Chaves gerenciadas pelo cliente no Private Beta {#customer-managed-keys-in-private-beta}

A equipe de engenharia da Adobe está trabalhando atualmente em uma implementação aprimorada do CMK aproveitando o Link privado do Azure. A nova implementação permitirá o compartilhamento da chave por meio do backbone do Azure graças a uma conexão direta de Link privado entre o locatário do Adobe e o Cofre da Chave.

Essa implementação aprimorada está atualmente na Private Beta e pode ser ativada para clientes selecionados que concordam em assinar o programa da Private Beta e trabalhar em conjunto com a Engenharia de Adobe. Se você estiver interessado no Private Beta para CMK usando Private Link, entre em contato com a Adobe para obter mais informações.
