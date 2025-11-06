---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.7.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.7.0.
exl-id: 7866d94c-e54c-4bb2-aaa6-66c019e46336
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 49%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.7.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.7.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.7.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 27 de julho de 2023. O próximo lançamento de recursos (2023.8.0) está planejado para sexta-feira, 31 de agosto de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de julho de 2023 para ver um resumo dos recursos adicionados na versão 2023.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* MSM para fragmentos de conteúdo. O Gerenciador de vários sites do AEM agora está disponível para Fragmentos de conteúdo, permitindo criar Live Copies de fragmento de conteúdo para distribuição de conteúdo em massa. Os controles de herança granular estão disponíveis até o nível do Elemento do fragmento de conteúdo e Variação.

### Novos recursos no pré-lançamento do [!DNL Experience Manager Sites] {#prerelease-sites}

* O [Console de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html) agora permite que os usuários exibam marcas e pesquisem por marcas aplicadas como metadados aos fragmentos de conteúdo. Os usuários não precisarão mais alternar para a interface do Assets para esse recurso, reduzindo a alternância de contexto e melhorando a eficiência.

![Marcação no Console de Fragmentos de Conteúdo](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na visualização de ativos {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**Estrutura de inteligência artificial aprimorada para Tags inteligentes de imagem**

O Experience Manager Assets agora usa uma estrutura de inteligência artificial aprimorada para Tags inteligentes de imagem. Essa inteligência de conteúdo resulta em melhor relevância e precisão das Tags inteligentes disponíveis para todos os ativos de imagem na ingestão.

**Configuração da exibição de colunas da exibição Lista de ativos**

O Assets Essentials agora oferece a capacidade de selecionar as colunas mostradas na exibição Lista de ativos, como Status, Formato, Dimensões, Tamanho e assim por diante.

![Configuração de colunas](/help/release-notes/assets/configure-columns.png)

**Classificação de resultados de pesquisa com base na relevância**

Por padrão, o Assets Essentials agora classifica os resultados de pesquisa com base na relevância. É possível classificar os ativos pesquisados em ordem crescente ou decrescente de `Name`, `Relevance`, `Size`, `Modified` e `Created`.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Temas**](/help/forms/using-themes-in-core-components.md) **e modelos** prontos: inicie seu processo de criação de formulários com nossos temas e modelos prontos para uso, personalizados para capacitar profissionais experientes e novos autores de formulários. Construídos de maneira contínua usando os Componentes principais do Adaptive Forms, esses temas e modelos meticulosamente preparados permitem que você comece a criar formulários rapidamente para casos de uso comuns.

* **[React Components do Headless Forms](https://github.com/adobe/aem-forms-headless-components/tree/main/packages/react-vanilla-components)**: agora é possível visualizar e personalizar   Representações do formulário adaptável headless com os componentes do React fornecidos imediatamente. Esses componentes usam classes BEM dos Componentes principais do Forms adaptável para estilo, facilitando a personalização da aparência de acordo com suas necessidades específicas.

* [**Criar Forms Adaptável com seções que podem ser repetidas**](/help/forms/create-forms-repeatable-sections.md): Agora você pode fazer com que os componentes de [Acordeão](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=pt-BR), [Assistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=pt-br), [Painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) e [Guias Horizontais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=pt-br) baseados em Formulário Adaptável sejam repetidos para captura de vários registros de dados.  Essas seções repetíveis permitem fornecer várias entradas de dados facilmente. É útil quando as instâncias de dados necessárias são desconhecidas. Um preenchimento de formulário pode adicionar ou remover seções facilmente, tornando os formulários adaptáveis a diferentes cenários de entrada de dados e simplificando a coleta de várias ocorrências do mesmo registro de dados.


### Recursos de pré-lançamento disponíveis em [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Suporte empresarial para o Google reCAPTCHA**](/help/forms/captcha-adaptive-forms.md): use o Google reCAPTCHA Enterprise em um Formulário adaptável para fornecer proteção aprimorada contra atividades fraudulentas e spam, proporcionando uma experiência mais segura para o usuário. Com a análise de risco avançada e a integração perfeita, os usuários genuínos podem enviar formulários facilmente, enquanto os bots são bloqueados de maneira eficaz.

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Use [Formulários adaptáveis Headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR) para permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e manuseados por meio de APIs, em vez de utilizar uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* aproveitar o potencial do Adobe Experience Manager Forms

Você pode enviar um email para `aem-forms-headless@adobe.com` utilizando sua ID de email oficial para participar do programa de adoção antecipada.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Centro de ações {#actions-center}

Assine notificações por email que o alertam quando ocorrem incidentes críticos que exigem ação imediata, e também com recomendações personalizadas para otimizar seu site. [Centro de Ações](/help/operations/actions-center.md) serve como um hub onde você pode examinar esses alertas, como filas de replicação bloqueadas ou credenciais com expiração, e marcá-los como resolvidos.

![Captura de tela do Centro de Ações](/help/assets/assets/actions-center.png)

### Programa de adoção antecipada das Regras CDN e WAF {#waf-early-adopter}

Filtrar o tráfego na CDN com base em:

* cabeçalhos e propriedades de solicitação (por exemplo, endereço IP)
* padrões de tráfego conhecidos por estarem associados a tráfego mal-intencionado

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para **aemcs-waf-adopter@adobe.com** a partir da sua ID de email oficial para saber mais sobre o programa de adoção antecipada. O espaço é limitado.

Saiba mais sobre o recurso no artigo [aqui](/help/security/traffic-filter-rules-including-waf.md).

### Outras alterações de base {#other-foundation-changes}

* Durante a semana de 7 de agosto, o AEM retornará o código de erro 429 em vez do código de erro 503 quando as solicitações para instâncias do AEM excederem um nível íntegro. [Saiba mais](/help/implementing/developing/introduction/development-guidelines.md).

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
