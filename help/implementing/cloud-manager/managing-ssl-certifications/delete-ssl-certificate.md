---
title: Excluir um certificado SSL - Gerenciar certificados SSL
description: Excluir um certificado SSL - Gerenciar certificados SSL
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---

# Excluir um certificado SSL {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>Remover certificados do Cloud Manager é uma ação permanente que não pode ser desfeita. A prática recomendada é salvar os arquivos SSL necessários localmente antes de excluí-los na interface do usuário do Cloud Manager.

Um usuário deve estar na função Proprietário comercial ou Gerente de implantação para excluir um certificado SSL no Cloud Manager. O Cloud Manager não permitirá que você exclua um certificado SSL que tenha um ou mais domínios associados a ele.  Todos os domínios associados devem ser excluídos antes de excluir o certificado SSL. Consulte [Excluindo um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para saber mais.

Siga as etapas abaixo para excluir um certificado SSL:

1. Navegue até o **Certificados SSL** da tela **Ambientes** página.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. Identifique a linha na qual o nome do certificado SSL que você deseja excluir está listado.
1. Selecione o **...** na extremidade direita da linha.
1. Selecionar **Excluir**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. Confirme seu envio a partir de **Excluir Certificado SSL** caixa de diálogo.
