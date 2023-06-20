---
title: '[!DNL Experience Manager Assets] integração com [!DNL Adobe Workfront]'
description: Introdução à integração entre [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 5568be57db4e270fcee22e637fc40f07529e0ecd
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] integração com [!DNL Adobe Workfront] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Este artigo |

O [!DNL Adobe Workfront] é um aplicativo de gerenciamento de trabalho que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. A integração [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] O permite que as organizações melhorem a velocidade do conteúdo e o prazo para comercialização, conectando intrinsecamente o gerenciamento de trabalho e de ativos digitais. No contexto do gerenciamento de trabalho no Workfront, os usuários têm acesso aos documentos e imagens necessários.

Adobe oferece para [integrar [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] nativamente (com suporte para Assets Essentials e Assets as a Cloud Service) ou usando o conector aprimorado do Workfront for Experience Manager](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). No caso de uma integração nativa, não é necessário um conector para integrar as duas soluções.

>[!NOTE]
>
>O Adobe não suporta o uso do conector Workfront para Experience Manager e a integração Experience Manager em paralelo.

Com a integração de Experience Manager nativa e [!DNL Workfront for Experience Manager enhanced connector], você pode:

| Nativo [!DNL Adobe Experience Manager Assets] recursos | [!DNL Workfront for Experience Manager enhanced connector] recursos |
|---|---|
| <ul><li>Configure rapidamente a integração dentro do Workfront.</li><li>Crie automaticamente pastas vinculadas entre o Workfront e o Experience Manager.</li><li>Sincronizar facilmente metadados de ativos vinculados existentes.</li><li>Atualize automaticamente os metadados do projeto quando ele for alterado no Workfront.</li><li>Conecte sem problemas vários repositórios Experience Manager Assets a um ambiente Workfront ou vários ambientes Workfront a um repositório Experience Manager Assets em IDs de organização.</li> | <ul><li>Crie pastas de Experience Manager vinculadas automaticamente no Workfront e organize as pastas com base em Portfolio, Programas e Projetos Workfront.</li><li>Sincronizar metadados de projeto do Workfront com pastas de Experience Manager vinculadas.</li><li>Atualizações de metadados Experience Manager com novas versões.</li><li>Defina os status dos objetos do Workfront com base nas condições configuráveis usando workflows Experience Manager.</li><li>Publicar ativos no ambiente de publicação do Experience Manager ou no Brand Portal.</li> |

Consulte a [recursos suportados abaixo para uma comparação](#feature-parity-matrix) entre uma integração nativa ou uma integração usando conectores entre as duas soluções.

>[!IMPORTANT]
>
>A partir de junho de 2022, o Adobe lançou uma nova integração nativa para conectar o Workfront ao Adobe Experience Manager Assets as a Cloud Service. Essa integração se tornou o método necessário para conectar essas duas soluções. Qualquer nova implementação futura do conector aprimorado (1.9.8 e posterior) para conectar o Workfront com o AEM Assets as a Cloud Service será bloqueada. Para obter mais informações sobre como configurar essa integração, consulte [Configurar a integração as a Cloud Service do Experience Manager Assets](workfront-connector-configure.md).
>

Consulte o site de suporte e [pré-requisitos para o conector aprimorado](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* O Adobe exige a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], não é compatível com o Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam esse conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso desse conector.
>
>* O Adobe suporta o conector aprimorado versões 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, consulte a etapa 5(a) do [instruções de instalação do conector aprimorado](workfront-connector-install.md).
>
>* Consulte [Exame de certificação de parceiros para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia do exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Comparar diferentes integrações entre [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Veja a seguir os detalhes das funcionalidades disponíveis por meio de vários tipos de integrações entre [!DNL Assets] e [!DNL Workfront].

| Destaque | Descrição | [!DNL Workfront] e [!DNL Assets Essentials] *Sem conector (OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *Requer conector* | WORKFRONT e [!DNL Experience Manager as a Cloud Service] *Sem conector (OOTB)* |
|----|----|----|-----|-----|
| Métodos de implantação | Adequado para o qual [!DNL Assets] oferta. | Assets Essentials | Adobe Managed Services, no local | Serviço em nuvem |
| **Geral** |
| Enviar arquivos digitais de [!DNL Workfront] para [!DNL Assets] | A versão mais recente de um documento WF pode ser carregada no AEM Assets, que está vinculado como uma nova versão do documento. | ✓ | ✓ | ✓ |
| Vincular manualmente pastas do AEM a objetos do Workfront | As pastas AEM existentes podem ser vinculadas como uma pasta do Workfront e seus ativos secundários são vinculados como novos documentos do Workfront. | ✓ | ✓ | ✓ |
| Link [!DNL Assets] para objetos do Workfront | Os ativos existentes no AEM podem ser vinculados a um novo documento do Workfront ou como uma nova versão de um documento existente. | ✓ | ✓ | ✓ |
| Os ativos adicionados às pastas vinculadas são enviados automaticamente para o AEM | Se um documento for adicionado a uma pasta vinculada, o ativo associado será carregado automaticamente no AEM Assets como um novo ativo. | ✓ | ✓ | ✓ |
| Baixar o AEM Assets vinculado no Workfront | Quando um ativo é vinculado no Workfront, o usuário pode baixar os bytes do ativo. | ✓ | ✓ | ✓ |
| Pesquisar por AEM Assets no Workfront | O seletor de AEM Assets no Workfront permite pesquisas de texto completo por ativos. | ✓ | ✓ | ✓ |
| Pesquisar pastas AEM de dentro do Workfront | O seletor de AEM Assets no Workfront permite pesquisas de texto completo para pastas. | ✓ | ✓ | ✓ |
| Exibir e navegar pela hierarquia de pastas do AEM a partir do Workfront | O seletor de AEM Assets no Workfront permite a navegação da hierarquia do AEM Assets AEM limitada pelos controles de acesso e permissões associados do usuário definidos no. | ✓ | ✓ | ✓ |
| Rastrear as versões do ativo nas linhas do tempo do AEM | Manter o histórico de versões do documento entre o Workfront e o AEM. | ✓ | ✓ | ✓ |
| Desvincular ativos do AEM Assets no Workfront | Um ativo vinculado existente do AEM pode ser desvinculado do documento associado do Workfront. Isso não exclui o ativo original dentro do AEM. | ✓ | ✓ | ✓ |
| Adicionar ativo de nova versão do Workfront ao AEM Assets | Quando uma versão recém-adicionada é adicionada em um documento no Workfront, um usuário pode enviar a nova versão para AEM para substituir a versão existente. | ✓ | ✓ | ✓ |
| Ativos vinculados ao Workfront quando clicados Direcionam o usuário para AEM | Os usuários são direcionados ao AEM para visualizar um ativo vinculado no Workfront. | ✓ | ✓ | Próximos |
| Criar automaticamente pastas vinculadas do AEM no Workfront | Crie automaticamente pastas vinculadas do AEM no Workfront usando status de projeto. Automaticamente, configure as pastas do AEM com base em Portfolio, programas e projetos do Workfront. | Não | ✓ | Não |
| Navegar diretamente para repositórios AEM no Workfront | Permitir que os usuários naveguem até repositórios AEM disponíveis configurados no Workfront. | ✓ | Não | ✓ |
| Criar pastas vinculadas do AEM no Workfront | Crie manualmente pastas vinculadas do AEM no Workfront usando a opção disponível na guia Documents. | ✓ | Não | ✓ |
| Sincronização de comentários | Sincronizar comentários automaticamente para ativos do [!DNL Workfront] para [!DNL Assets] | Não | ✓ | Não |
| Suporte a vários ambientes Workfront conectados a um único ambiente AEM | Usuários de vários ambientes do Workfront podem se conectar a um único ambiente AEM. | ✓ | Não | ✓ |
| Suporte a vários ambientes AEM conectados a um único ambiente Workfront | Os usuários em um único ambiente do Workfront podem enviar ou vincular ativos entre vários ambientes AEM. | ✓ | ✓ | ✓ |
| **Metadados** |
| Mapear metadados de ativos do Workfront para o AEM Assets | As propriedades de objetos e formulários personalizados do Workfront podem ser mapeadas para propriedades de metadados de ativos AEM. Os valores são enviados no upload/link inicial. | ✓ | ✓ | ✓ |
| Criar automaticamente Forms personalizados de documentos no Workfront | Anexe formulários personalizados a documentos, tarefas e problemas do Workfront usando workflows AEM. | Não | ✓ | Não |
| Atualização automática bidirecional de metadados entre o AEM Assets e o Workfront | Atualize automaticamente os metadados entre o AEM Assets e o Workfront. O ativo deve ser inicialmente enviado do Workfront para o AEM e os metadados de ativos do Workfront devem ser mapeados para ativos do AEM para que as atualizações de metadados bidirecionais funcionem adequadamente. | Não | ✓ | Não |
| Visualização em tempo real no Workfront para metadados mapeados para AEM | Visualize os metadados mapeados atualizados para AEM nos painéis Detalhes do documento e Resumo do documento do Workfront. | ✓ | Não | ✓ |
| Envio em tempo real de metadados atualizados do Workfront para AEM | Atualizar automaticamente os metadados do Workfront mapeados para AEM sem recarregar um ativo ou uma nova versão de um ativo. | ✓ | Não | ✓ |
| Mapear metadados do Workfront para pastas do AEM Assets | Sincronizar metadados de projeto do Workfront com pastas AEM vinculadas. | Não | ✓ | ✓ |
| Atualizações de metadados AEM com novas versões | Uma configuração no AEM pode ser feita para determinar se um ativo de versão recente no Workfront também envia com qualquer alteração feita em seus metadados. | Não | ✓ | Não |
| Atualizar automaticamente metadados AEM nas alterações no Forms personalizado no Workfront | O AEM permite que você se inscreva nas atualizações dos formulários de documento no Workfront. Como resultado, qualquer atualização nos metadados de formulário personalizado do documento do Workfront modifica os valores dos campos de metadados AEM mapeados. | Não | ✓ | Não |
| **Fluxos de trabalho (prontos para uso)** |
| Criar nova versão de prova em ativos vinculados | Ao vincular um ativo no Workfront, uma prova pode ser gerada automaticamente. | Não | Personalizado | Não |
| Definir status em objetos do Workfront | Definir status de objetos do Workfront com base em condições configuráveis usando workflows AEM | Não | ✓ | Próximos |
| Publicar ativos no ambiente de publicação do AEM ou no Brand Portal | Dê aos usuários do Workfront a opção de publicar automaticamente ativos vinculados em um ambiente de publicação do AEM ou Brand Portal. | Não | ✓ | Próximos |
