---
title: '[!DNL Experience Manager Assets] integração com [!DNL Adobe Workfront]'
description: Introdução à integração entre [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: f295eead13bcdeed910ae6b8c82373e2b70f1224
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] integração com [!DNL Adobe Workfront] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Este artigo |

O [!DNL Adobe Workfront] é um aplicativo de gerenciamento de trabalho que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. A integração [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] O permite que as organizações melhorem a velocidade do conteúdo e o prazo para comercialização, conectando intrinsecamente o gerenciamento de trabalho e de ativos digitais. No contexto do gerenciamento de trabalho no Workfront, os usuários têm acesso aos documentos e imagens necessários.

Adobe oferece para [integrar [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] nativamente (compatível com Assets Essentials e Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html).

Com a integração de Experience Manager nativa, é possível:

* Configure rapidamente a integração dentro do Workfront.

* Crie automaticamente pastas vinculadas entre o Workfront e o Experience Manager.

* Sincronizar facilmente metadados de ativos vinculados existentes.

* Atualize automaticamente os metadados do projeto quando ele for alterado no Workfront.

* Conecte sem problemas vários repositórios Experience Manager Assets a um ambiente Workfront ou vários ambientes Workfront a um repositório Experience Manager Assets em IDs de organização.


## Conector aprimorado do Adobe Workfront para Experience Manager {#enhanced-connector-information}


A partir de junho de 2022, o Adobe lançou uma nova integração nativa para conectar o Workfront ao Adobe Experience Manager Assets as a Cloud Service. Essa integração se tornou o método necessário para conectar essas duas soluções. Qualquer nova implementação futura do conector aprimorado (1.9.8 e posterior) para conectar o Workfront com o AEM Assets as a Cloud Service será bloqueada. Para obter mais informações sobre como configurar essa integração, consulte [Configurar a integração as a Cloud Service do Experience Manager Assets](workfront-connector-configure.md).

>[!NOTE]
>
>O Adobe não suporta o uso do conector Workfront para Experience Manager e a integração Experience Manager em paralelo.

Para instalações anteriores a junho de 2022, os itens a seguir são alguns pontos a serem observados para a implantação e configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector]:

* O Adobe exige a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], não é compatível com o Adobe.
* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam esse conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso desse conector.
* O Adobe suporta o conector aprimorado versões 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, consulte a etapa 5(a) do [instruções de instalação do conector aprimorado](workfront-connector-install.md).
* Consulte [Exame de certificação de parceiros para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia do exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).