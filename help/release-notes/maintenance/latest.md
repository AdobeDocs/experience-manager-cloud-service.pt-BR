---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a3c414f9b5e575856a942e02661e8c70a7083495
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 20%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 19149 {#19149}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 19149, lançada publicamente em quarta-feira, 21 de janeiro de 2025. A versão de manutenção anterior foi a versão 18751.

A ativação de recursos do 2025.1.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-19149}

* ASSETS-45286: mostrar progresso granular para o trabalho assíncrono de arquivamento de download.
* ASSETS-46296: suporte para modelos do Dynamic Media no Seletor de ativos.
* ASSETS-44796: acionar eventos do Assets para trabalhos de ativos assíncronos do DAM.

### Problemas corrigidos {#fixed-issues-19149}

* GRANITE-55074: certifique-se de que os cabeçalhos de resposta do CORS estejam definidos nas respostas de erro.
* ASSETS-43755: melhorias de escalabilidade para ativos em massa relacionados.
* ASSETS-45399: redirecione para o Assets Console após criar a live copy do ativo.
* ASSETS-45462: problemas de cache do navegador com miniaturas de pastas personalizadas.
* ASSETS-46398: Ocultar ações de Download e reprocessamento para Modelos DM.
* ASSETS-44484: problemas ao salvar novamente a configuração do Connected Assets.
* ASSETS-44122: o trabalho de cópia assíncrona de ativos não renomeia a pasta de destino ao copiar para a pasta atual.
* ASSETS-44463: o botão Baixar CSV não fica visível na exportação de metadados bem-sucedida.
* ASSETS-45134: Mover o trabalho com o título de destino substitui todos os títulos de pasta.
* ASSETS-45137: conflito com uploads em massa por meio do Assets View.
* ASSETS-45758: as relações de ativos recebem uma animação de ocupação/carregamento infinita após adicionar uma relação.
* ASSETS-44148: o evento NODE_MOVED no AEM pode causar NPE falso em logs.
* ASSETS-28607: Erro JS ao definir a miniatura de vídeo personalizada.
* GRANITE-55781: Melhore a sincronização de grupos entre o Adobe Developer Console e o AEM. Mais detalhes em [Alterações na Sincronização de Grupos de Usuários e Perfis de Produtos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).
* GRANITE-55754: certifique-se de que os scripts de inicialização do SDK sejam compatíveis com o Java 21.
* GRANITE-54248: não é possível rolar por todos os itens na pasta de ativos grande.
* SCRNS-4597: Melhorias na exibição da lista de resultados da pesquisa.


### Problemas conhecidos {#known-issues-19149}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-19149}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

#### Alterações na sincronização de grupos de usuários e perfis de produtos

Ao usar o Adobe Admin Console para gerenciamento de permissões, os seguintes grupos NÃO DEVEM ser usados, pois não serão mais sincronizados com o AEM:
* Grupos AEM que terminam com _GROUP_NAME_SUFFIX.
* Perfis de produto de outros ambientes, programas ou produtos.

Para obter mais detalhes, verifique [Alterações na sincronização de Grupos de Usuários e Perfis de Produtos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).

#### Substituição do editor de SPA {#deprecate-spa-editor}

[O Editor de SPA](/help/implementing/developing/hybrid/introduction.md) foi descontinuado para novos projetos a partir da versão 2025.1.0. O Editor de SPA continua sendo compatível com projetos existentes, mas não deve ser usado para novos projetos.

Os editores preferidos para gerenciar conteúdo headless no AEM são:

* [O Editor Universal](/help/edge/wysiwyg-authoring/authoring.md) para edição visual.
* [O Editor de Fragmento de Conteúdo](/help/assets/content-fragments/content-fragments-managing.md) para edição baseada em formulário.

### Correções de segurança {#security-19149}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda quatro vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-19149}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak API 1.72.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
