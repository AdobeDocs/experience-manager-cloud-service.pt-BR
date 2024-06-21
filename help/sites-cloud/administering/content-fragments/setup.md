---
title: Fragmentos de conteúdo - Configuração
description: Saiba como ativar a funcionalidade Fragmento de conteúdo e GraphQL para uso com recursos de entrega sem cabeçalho AEM e criação de página.
feature: Content Fragments
role: Developer, Architect
exl-id: 3974d698-1e7d-4a5f-a6d5-cbf8d96b4095
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 37%

---

# Fragmentos de conteúdo - Configuração {#content-fragments-setup}

Fragmentos de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service permitem preparar conteúdo pronto para uso em vários locais e canais. Isso é ideal para entrega headless e criação de página.

Para habilitar sua instância para a funcionalidade de Fragmento de conteúdo, é necessário habilitar:

* **Modelos de fragmentos de conteúdo** (obrigatório)

  >[!CAUTION]
  >
  >Se você não habilitar os **modelos de fragmentos de conteúdo**:
  >
  >* o **Criar** A opção não estará disponível para criar modelos.
  >* você não poderá [selecionar a configuração de sites para criar o ponto de acesso relacionado](/help/headless/graphql-api/graphql-endpoint.md).

* **Consultas GraphQL persistidas** - opcional

A configuração da sua instância foi concluída:

* por [ativando a funcionalidade no Navegador de configuração](#enable-content-fragment-functionality-configuration-browser)
* depois [aplicar a configuração às pastas individuais de ativos](#apply-the-configuration-to-your-folder)

## Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-configuration-browser}

Para usar a funcionalidade Fragmento de conteúdo, dos Modelos de fragmento de conteúdo e das Consultas persistentes do GraphQL, você **deve** primeiro ative-os por meio da **Navegador de configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte [Navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Subconfigurações](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (uma configuração aninhada em outra configuração) são totalmente compatíveis com o uso de fragmentos de conteúdo, modelos de fragmento de conteúdo e consultas GraphQL.
>
>Apenas observe que:
>
>* Após criar modelos em uma subconfiguração, NÃO é possível mover ou copiar o modelo para outra subconfiguração.
>
>* Um ponto de acesso de GraphQL (ainda) será baseado em uma configuração principal (raiz).
>
>* As consultas persistentes (ainda) serão salvas relativas à configuração principal (raiz).

1. Navegue até **Ferramentas**, **Geral**, e abra o **Navegador de configuração**.

1. Selecione **Criar** para abrir a caixa de diálogo, onde você:

   1. Especifica um **Título**.
   1. Após a criação, o **Nome** torna-se o nome do nó no repositório.
Você pode inserir um nome. Se você deixar o campo em branco, ele será gerado automaticamente com base no título e ajustado de acordo com [Convenções de nomenclatura do AEM](/help/implementing/developing/introduction/naming-conventions.md); você poderá ajustar o resultado, se necessário.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas GraphQL persistidas**

      ![Definir configuração](assets/cf-setup-create-conf.png)

1. Selecione **Criar** para salvar a definição.

## Aplicar a configuração à sua pasta {#apply-the-configuration-to-your-folder}

Quando a configuração **global** estiver ativado para a funcionalidade Fragmento de conteúdo, ele se aplica a qualquer pasta de ativos - acessível por meio do **Assets** console.

Para usar outras configurações (portanto, excluindo globais) com uma pasta do Assets comparável, é necessário definir a conexão. Faça isso selecionando o **Configuração** no **Cloud Service** guia do **Propriedades da pasta** da pasta apropriada.

![Aplicar configuração](assets/cf-setup-apply-conf.png)
