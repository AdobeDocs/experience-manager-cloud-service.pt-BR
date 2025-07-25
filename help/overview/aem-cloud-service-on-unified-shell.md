---
title: AEM as a Cloud Service no shell unificado
description: Saiba mais sobre os benefícios do AEM as a Cloud Service no shell unificado
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
feature: Release Information
role: Admin
source-git-commit: 55cf6a10c2cb4c62aa8f89fac7f9d1fb4c012d26
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 92%

---

# AEM as a Cloud Service no shell unificado {#aem-as-a-cloud-service-on-unified-shell}

## Visão geral {#overview}

O AEM as a Cloud Service (Serviço do autor) está integrado ao Unified Shell para melhorar a experiência do usuário e unificá-la com todos os outros aplicativos da Experience Cloud. O impacto dessa integração pode ser visto no cabeçalho superior do aplicativo, como mostrado abaixo.

![imagem](/help/overview/assets/unifiedshell_header.png)

Os benefícios disso são:

* Logon único em todos os aplicativos da Experience Cloud
* Fácil alternação entre organizações ou para um aplicativo diferente
* Ajuda do produto aprimorada
* Botão de feedback de fácil acesso no produto para reportar problemas ou compartilhar ideias com a Adobe
* Acesso a anúncios e notificações de produtos globais, além de notificações específicas do AEM as a Cloud Service

## Desabilitar o Unified Shell {#disabling-unified-shell}

Por padrão, o AEM as a Cloud Service vem com o Unified Shell ativado. No entanto, caso o cabeçalho superior tenha sido personalizado, é recomendável desativar o Unified Shell para evitar problemas com as personalizações. Para desativar o Unified Shell, siga as etapas abaixo:

>[!NOTE]
>O Unified Shell só pode ser desativado por uma conta com privilégios administrativos.

1. Clique em **Ferramentas > Cloud Services**.

   Admins veem o cartão de configuração do Unified Shell como mostrado abaixo:

   ![imagem](/help/overview/assets/unifiedshell2.png)

1. Clique em **Configuração do Unified Shell**. Em seguida, desmarque a caixa de seleção mostrada abaixo para desativar o Unified Shell:

   ![imagem](/help/overview/assets/unifiedshell3.png)

>[!NOTE]
>
>O Unified Shell também pode ser desativado no código do projeto. Consulte [Estrutura da interface do AEM - Shell Unificado](/help/implementing/developing/introduction/ui-structure.md#unified-shell).

## Alterar para o tema escuro {#changing-to-dark-theme}

Para alterar para o tema escuro, clique no ícone do seu perfil. Essa ação exibe um popover, conforme mostrado abaixo. Você pode usar o botão de alternância para alternar para um tema escuro do Unified Shell.

>[!INFO]
>
>O tema escuro se aplica somente ao Unified Shell (a barra superior).

![imagem](/help/overview/assets/unifiedshell4.png)

## Identificação do ambiente do AEM as a Cloud Service {#identify-aemaacs-environment}

O AEM as a Cloud Service fornece três tipos de ambientes: produção, preparo e desenvolvimento. Consulte [Tipos de ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=pt-BR) para obter mais detalhes. Com essa integração com o Unified Shell, o tipo de ambiente em que o usuário está conectado no serviço de Autor é exibido no cabeçalho superior por meio de um rótulo, como mostrado abaixo.

![imagem](/help/overview/assets/unifiedshell_header_label.png)

## Acessar a Caixa de entrada AEM {#accessing-the-aem-inbox}

A caixa de entrada do AEM pode ser acessada clicando no ícone de sino no Unified Shell.

>[!INFO]
>
> O número indicado no ícone de sino inclui notificações não lidas em todas as soluções dentro da Organização IMS e tarefas listadas na Caixa de entrada AEM.

![imagem](/help/overview/assets/unifiedshell5.png)

Clique no botão da caixa de entrada no popover para acessar a caixa de entrada do AEM:

![imagem](/help/overview/assets/unifiedshell6.png)

