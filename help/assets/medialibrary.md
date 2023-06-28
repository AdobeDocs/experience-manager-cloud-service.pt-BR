---
title: Use o Media Library para o gerenciamento básico de ativos digitais
description: "[!DNL Experience Manager Assets] e Media Library para gerenciamento de ativos."
contentOwner: AG
feature: Asset Management,Publishing
role: User,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 9%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Usar o Media Library para gerenciamento básico de ativos {#manage-assets-using-media-library}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/medialibrary.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

[!DNL Adobe Experience Manager] A plataforma fornece diferentes recursos para gerenciar ativos. O Media Library permite que os usuários façam upload de um pequeno número de ativos no repositório, pesquisem e usem esses ativos nas páginas da Web e realizem tarefas simples de gerenciamento de ativos nos ativos.

O Media Library é uma solução leve de gerenciamento de ativos digitais (DAM) que vem complementar com [!DNL Adobe Experience Manager Sites] licença. [!DNL Sites] O é uma oferta de Gerenciamento de conteúdo da Web (WCM). O Media Library funciona com todos os recursos do Experience Manager.

[!DNL Adobe Experience Manager Assets] A licença do está disponível separadamente para compra. [!DNL Experience Manager Assets] O permite a manipulação robusta de ativos por meio de casos de uso corporativos, personalizações de metadados, esquemas, pesquisa e interface do usuário, além de muitos outros recursos além do que o Media Library oferece.

## Requisitos de licenciamento {#avail-media-library-license}

Clientes que têm [!DNL Sites] estão autorizadas a usar o Media Library. Funciona com todos os componentes do [!DNL Experience Manager].

O Media Library é instalado como parte do Sites. Não é necessária nenhuma licença ou pacote adicional além da licença e instalação do Sites.

## [!DNL Assets] versus Media Library {#assets-and-media-library}

A Experience Manager Assets oferece a funcionalidade DAM de nível empresarial. A funcionalidade de ativos é fornecida com o [!DNL Experience Manager] em um único pacote. No entanto, os usuários que não compraram uma licença do Assets não estão autorizados a usar os recursos avançados do DAM. Sem a licença do Assets, somente [Recursos do Media Library](#use-media-library) estão disponíveis.

Se você quiser impedir o uso não intencional de [!DNL Assets] recursos que você não licenciou, remova todas as [!DNL Assets]fluxos de trabalho específicos do, componentes, taxonomias, opções e a [!DNL Assets] administrador de [!DNL Experience Manager]. Isso evita que os usuários usem acidentalmente [!DNL Assets] recursos que você não licenciou.

## Usar o Media Library {#use-media-library}

O Media Library abrange amplamente os seguintes casos de uso:

* Fornecer recursos básicos do DAM para páginas da Web criadas com o [!DNL Adobe Experience Manager Sites].
* Formulários e comunicações adaptáveis criados usando o [!DNL Adobe Experience Manager Forms].
* Experiências de tela digital criadas com o [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] APIs REST HTTP para operações headless.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

Para usar a funcionalidade Media Library, é possível usar o padrão [!DNL Experience Manager] interface do usuário. O Media Library faz parte da [!DNL Experience Manager Sites] instalação e nenhuma interface ou complemento separado é necessário. Usando a interface existente, os usuários do Media Library estão autorizados a realizar as seguintes tarefas:

* Criar pastas para organizar ativos.
* Fazer upload de ativos.
* Publicar ativos.
* Editar, mover e copiar ativos.
* Procurar, filtrar e pesquisar (inclui pesquisa de semelhança) ativos.
* Adicione valores e edite-os nos campos de metadados, exceto no campo Tags inteligentes, que estão disponíveis na [!UICONTROL Básico] de um ativo [!UICONTROL Propriedades] por padrão.
* Adicionar e excluir representações estáticas.
* Baixe pastas, ativos e representações de ativos.
* Criar versões de ativos.
* Criar e executar tarefas de revisão em ativos.
* Anotar ativos.
* Adicionar ativos ao [!DNL Sites] páginas por meio do Localizador de conteúdo.
* Uso [!DNL Content Fragments].
* Use APIs REST e GraphQL HTTP para [!DNL Content Fragments] e ativos de mídia referenciados, sob licença do Sites.
* integração com o Marketing Cloud.
* Personalizar e estender a interface do usuário do gerenciamento de ativos.
* Acesse o Construtor de consultas (API) para estender a funcionalidade de pesquisa.
* Criar tags estáticas.
* Crie projetos e tarefas.
* Fluxo de atividade (linha do tempo).
* Comentários e anotações.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Muitos casos de uso de DAM avançados são atendidos pelo [!DNL Experience Manager Assets]. A licença da Media Library permite que você preencha apenas os casos de uso listados usando o Media Library. Se um caso de uso não estiver listado, não o use com a licença da Media Library. Em caso de dúvidas, entre em contato com o Suporte ao cliente.

Observe que não é possível usar tags inteligentes, [!DNL Asset] link, [!DNL Asset] seletor, marcação em massa, modificar fluxos de trabalho de ativos ou padrão [!DNL Adobe Experience Manager] para acessar o Media Library sem [!DNL Assets] licença.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Recursos do DAM em [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=pt-BR)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] descrição do produto](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)
