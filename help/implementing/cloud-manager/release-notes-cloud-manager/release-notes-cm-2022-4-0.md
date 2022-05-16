---
title: Notas de versão do Cloud Manager 2022.4.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2022.4.0 em AEM as a Cloud Service.
feature: Release Information
exl-id: e7ff623b-aeca-40a6-bf48-98af270a4117
source-git-commit: 458d63c27bb2ab4d09237aa3ecb96c0f6d5e67ed
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de versão do Cloud Manager 2022.4.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2022.4.0 AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento da versão 2022.4.0 do Cloud Manager em AEM as a Cloud Service é 7 de abril de 2022. A próxima versão está planejada para 5 de maio de 2022.

## Novidades {#what-is-new}

* As melhorias na duração e na taxa de sucesso das etapas de criação do pipeline foram implementadas e serão implantadas de forma incremental para todos os clientes até o mês de abril.
* Agora é possível encontrar facilmente uma ramificação git digitando os primeiros caracteres do nome no campo de entrada no assistente adicionar e editar pipeline e selecionando entre as correspondências sugeridas para ambos [produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) Gasodutos.
* Logo após a versão de abril, a Índia estará disponível para seleção ao definir a região da nuvem durante a criação do ambiente.
* O **Pipelines** A página agora tem paginação para melhorar a usabilidade de programas com um grande número de pipelines.
   * 50 linhas por página serão exibidas na tabela.
* A versão do [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) usado pelo Cloud Manager foi atualizado para a versão 36.
* O JDK do Oracle agora é o JDK padrão para o desenvolvimento e a operação de aplicativos AEM. O processo de build do Cloud Manager mudará automaticamente para o uso do JDK do Oracle, mesmo se uma opção alternativa estiver explicitamente selecionada na cadeia de ferramentas Maven.
   * Para saber mais sobre como alternar para o Oracle JDK, consulte [a documentação do Ambiente de build.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * Consulte [Perguntas frequentes sobre a política de suporte de Java para Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) para abordar perguntas comuns sobre essa alteração.
* A execução do pipeline agora falhará mais rápido ao detectar versões de AEM mais antigas durante a etapa de validação. Os usuários receberão uma mensagem na interface do usuário para orientá-los.

## Correções de erros {#bug-fixes}

* O log criado na etapa Teste da interface do usuário agora está disponível para download por meio da interface do usuário.
* Os pipelines de configuração do nível da Web agora só podem reutilizar pacotes de execuções de configuração do nível da Web.
* Foi adicionada mais clareza às mensagens na interface do usuário sobre como atualizar AEM em um ambiente desatualizado.
