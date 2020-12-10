---
title: Exclusão de um certificado SSL - Gerenciamento de certificados SSL
description: Exclusão de um certificado SSL - Gerenciamento de certificados SSL
translation-type: tm+mt
source-git-commit: 84c8204d257de4ecdee3728176f6d4ef545346f5
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Excluindo um Certificado SSL {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>Remover certificados do Gerenciador de nuvem é uma ação permanente que não pode ser desfeita. A prática recomendada é salvar os arquivos SSL necessários localmente antes de excluí-los na interface do usuário do Cloud Manager.

>[!NOTE]
>Um usuário deve estar na função Proprietário de Negócios ou Gerenciador de Implantação para excluir um certificado SSL no Cloud Manager. O Cloud Manager não permitirá que você exclua um certificado SSL que tenha um ou mais domínios associados a ele.  Todos os domínios associados devem ser excluídos antes de excluir o certificado SSL. Consulte [Excluindo um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para saber mais.

Siga as etapas abaixo para excluir um certificado SSL:

1. Navegue até a tela Certificados SSL na página Ambientes
1. Identifique a linha na qual o nome do certificado SSL que você deseja excluir está listado.
1. Selecione **...** na extremidade direita da linha.
1. Selecione **Eliminar**.
1. Confirme seu envio.
