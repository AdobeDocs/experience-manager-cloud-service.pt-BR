---
title: Fragmentos de conteúdo - Configuração
description: Saiba como ativar a funcionalidade Fragmento de conteúdo e GraphQL para uso com os recursos de entrega headless do AEM e criação de página.
feature: Content Fragments
role: Developer
exl-id: 3974d698-1e7d-4a5f-a6d5-cbf8d96b4095
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
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
  >* a opção **Criar** não estará disponível para criar modelos.
  >* você não poderá [selecionar a configuração de sites para criar o ponto de acesso relacionado](/help/headless/graphql-api/graphql-endpoint.md).

* **Consultas GraphQL persistidas** - opcional

A configuração da sua instância foi concluída:

* por [habilitando a funcionalidade no Navegador de Configuração](#enable-content-fragment-functionality-configuration-browser)
* em seguida, [aplicando a configuração às suas pastas individuais do Assets](#apply-the-configuration-to-your-folder)

## Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-configuration-browser}

Para usar a funcionalidade Fragmento de Conteúdo, dos Modelos de Fragmento de Conteúdo e das Consultas Persistentes do GraphQL, você **deve** habilitá-los primeiro por meio do **Navegador de Configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte [Navegador de Configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

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
Você pode inserir um nome. Se você deixar o campo em branco, ele será gerado automaticamente com base no título e ajustado de acordo com as [Convenções de nomenclatura do AEM](/help/implementing/developing/introduction/naming-conventions.md); você poderá ajustar o resultado, se necessário.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas GraphQL persistidas**

      ![Definir configuração](assets/cf-setup-create-conf.png)

1. Selecione **Criar** para salvar a definição.

## Aplicar a configuração à sua pasta {#apply-the-configuration-to-your-folder}

Quando a configuração **global** está habilitada para a funcionalidade de Fragmento de Conteúdo, ela se aplica a qualquer pasta do Assets, acessível por meio do console **Assets**.

Para usar outras configurações (portanto, excluindo globais) com uma pasta do Assets comparável, é necessário definir a conexão. Faça isso selecionando a **Configuração** apropriada na guia **Serviços da Nuvem** das **Propriedades da Pasta** da pasta apropriada.

![Aplicar configuração](assets/cf-setup-apply-conf.png)
