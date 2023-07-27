---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 71af59cae28332793471568069204e9c88acd6a5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 32%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] A versão atual do recurso (2023.7.0) é 27 de julho de 2023. A próxima versão do recurso (2023.8.0) está planejada para 31 de agosto de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de julho de 2023 para ver um resumo dos recursos adicionados na versão 2023.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* MSM para fragmentos de conteúdo. O Gerenciador de vários sites do AEM agora está disponível para Fragmentos de conteúdo, permitindo criar Live Copies de fragmento de conteúdo para distribuição de conteúdo em massa. Os controles de herança granular estão disponíveis até o nível do Elemento do fragmento de conteúdo e Variação.

### Novos recursos no pré-lançamento do [!DNL Experience Manager Sites] {#prerelease-sites}

* A variável [Console de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=pt-BR) O agora permite que os usuários visualizem tags e pesquisem por tags aplicadas como metadados aos fragmentos de conteúdo. Os usuários não precisarão mais alternar para a interface do Assets para esse recurso, reduzindo a alternância de contexto e melhorando a eficiência.

![Marcação no Console de fragmentos de conteúdo](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na exibição do Assets {#assets-view-features}

**Atribuir formulário de metadados a uma pasta**

Agora é possível atribuir o formulário de metadados a uma pasta específica na implantação do Assets Essentials. Todos os ativos na pasta, incluindo ativos nas subpastas, em seguida, exibem as propriedades definidas no formulário de metadados atribuído.

![atribuir formulário de metadados a uma pasta](/help/release-notes/assets/assign-to-folder.png)

**Estrutura de inteligência artificial aprimorada para Tags inteligentes de imagem**

O Experience Manager Assets agora usa uma estrutura de inteligência artificial aprimorada para tags inteligentes de imagem. Essa inteligência de conteúdo resulta em melhor relevância e precisão das Tags inteligentes disponíveis para todos os ativos de imagem na assimilação.

**Configurar exibição de colunas para a exibição da Lista de ativos**

O Assets Essentials agora oferece a capacidade de selecionar as colunas exibidas na exibição da Lista de ativos, como Status, Formato, Dimension, Tamanho e assim por diante.

![Configurar colunas](/help/release-notes/assets/configure-columns.png)

**Classificar resultados da pesquisa com base na relevância**

Por padrão, o Assets Essentials agora classifica os resultados da pesquisa com base em Relevância. Você pode classificar os ativos pesquisados em ordem crescente ou decrescente de `Name`, `Relevance`, `Size`, `Modified` e `Created`.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Temas prontos para uso**](/help/forms/using-themes-in-core-components.md) **e modelos**: Inicie seu processo de criação de formulários com nossos temas e modelos OOTB prontos para uso, personalizados para capacitar profissionais experientes e novos autores de formulários. Construídos de maneira contínua usando os Componentes principais do Adaptive Forms, esses temas e modelos meticulosamente preparados permitem que você comece a criar formulários rapidamente para casos de uso comuns.

  ![Modelos prontos para uso](/help/forms/assets/form-templates-ootb.png)

* **Componentes do React para o Forms headless**: agora você pode visualizar e personalizar representações do Formulário adaptável headless com os componentes do React fornecidos imediatamente. Esses componentes aproveitam as classes BEM dos Componentes principais do Adaptive Forms para estilizar, facilitando a personalização da aparência de acordo com suas necessidades específicas.

* [**Criar Forms adaptável com seções que podem ser repetidas**](/help/forms/create-forms-repeatable-sections.md): Agora você pode fazer [Acordeão](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [Assistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html), [Painel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html), e [Guias Horizontais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) formulários adaptáveis com base em componentes repetíveis para captura de vários registros de dados.  Essas seções repetíveis permitem fornecer várias entradas de dados facilmente. É útil quando as instâncias de dados necessárias são desconhecidas antecipadamente. Um preenchimento de formulário pode adicionar ou remover seções facilmente, tornando os formulários adaptáveis a diferentes cenários de entrada de dados e simplificando a coleta de várias ocorrências do mesmo registro de dados.


### Recursos de pré-lançamento disponíveis em [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Suporte corporativo ao Google reCAPTCHA**](/help/forms/captcha-adaptive-forms.md): use o Google reCAPTCHA Enterprise em um formulário adaptável para fornecer proteção aprimorada contra atividades fraudulentas e spam, proporcionando uma experiência mais segura ao usuário. Com a análise de risco avançada e a integração perfeita, os usuários genuínos podem enviar formulários facilmente, enquanto os bots são bloqueados de maneira eficaz.

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Uso [Forms adaptável headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) para permitir que os desenvolvedores criem, publiquem e gerenciem formulários interativos que possam ser acessados e interagidos por meio de APIs, em vez de uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* aproveitar o potencial do Adobe Experience Manager Forms

Você pode enviar um email para `aem-forms-headless@adobe.com` utilizando sua ID de email oficial para participar do programa de adoção antecipada.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Centro de ações {#actions-center}

Assine notificações por email que o alertam quando ocorrem incidentes críticos que exigem ação imediata, e também com recomendações personalizadas para otimizar seu site. [Centro de ações](/help/operations/actions-center.md) serve como um hub onde você pode revisar esses alertas, como filas de replicação bloqueadas ou credenciais com expiração, e marcá-los como resolvidos.

![Captura de tela do Centro de ações](/help/assets/assets/actions-center.png)

### Programa de adoção antecipada das regras CDN e WAF {#waf-early-adopter}

Filtrar o tráfego na CDN com base em:
* cabeçalhos e propriedades de solicitação (por exemplo, endereço IP)
* padrões de tráfego conhecidos por estarem associados a tráfego mal-intencionado

Interessado em experimentar o recurso e compartilhar feedback? Enviar um email para **aemcs-waf-adopter@adobe.com** da sua ID de e-mail oficial para saber mais sobre o programa dos participantes antecipados. O espaço é limitado.

Saiba mais sobre o recurso no artigo [aqui](/help/security/cdn-and-waf-rules.md).

### Outras alterações de base {#other-foundation-changes}

* Durante a semana de 7 de agosto, o AEM retornará o código de erro 429 em vez do código de erro 503 quando as solicitações para instâncias AEM excederem um nível saudável. [Saiba mais](/help/implementing/developing/introduction/development-guidelines.md).

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
