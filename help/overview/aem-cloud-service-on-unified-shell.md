---
title: AEM as a Cloud Service no shell unificado
description: AEM as a Cloud Service no shell unificado
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: 24ae6187813de801813236f0bbcb2ea51e8fe5e1
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 100%

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

1. Navegue até **Ferramentas - Serviços na nuvem**.

   Um usuário administrador visualizará o cartão de configuração do Shell Unificado, como mostrado abaixo:

   ![imagem](/help/overview/assets/unifiedshell2.png)

1. Clique em **Configuração do Shell Unificado**. Em seguida, desmarque a caixa de seleção mostrada abaixo para desativar o Unified Shell:

   ![imagem](/help/overview/assets/unifiedshell3.png)

## Alterar para o tema escuro {#changing-to-dark-theme}

Para alterar para o tema escuro, clique no ícone do seu perfil. Isso exibirá uma janela pop-up, como mostrado abaixo. Você pode usar o botão de alternância para alternar para um tema escuro do Unified Shell.

>[!INFO]
>
>O tema escuro se aplica somente ao Unified Shell (a barra superior).

![imagem](/help/overview/assets/unifiedshell4.png)

## Identificação do ambiente do AEM as a Cloud Service {#identify-aemaacs-environment}

O AEM as a Cloud Service fornece três tipos de ambientes: produção, preparo e desenvolvimento. Consulte os [Tipos de ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=pt-BR) para obter mais detalhes. Com essa integração com o Unified Shell, o tipo de ambiente em que o usuário está conectado no serviço de Autor é exibido no cabeçalho superior por meio de um rótulo, como mostrado abaixo.

![imagem](/help/overview/assets/unifiedshell_header_label.png)

## Acessar a Caixa de entrada AEM {#accessing-the-aem-inbox}

A Caixa de entrada AEM pode ser acessada clicando no ícone de sino no Unified Shell.

>[!INFO]
>
> O número indicado no ícone de sino inclui notificações não lidas em todas as soluções dentro da Organização IMS e tarefas listadas na Caixa de entrada AEM.

![imagem](/help/overview/assets/unifiedshell5.png)

Clique no botão Caixa de entrada na janela pop-up para acessar a Caixa de entrada AEM:

![imagem](/help/overview/assets/unifiedshell6.png)
