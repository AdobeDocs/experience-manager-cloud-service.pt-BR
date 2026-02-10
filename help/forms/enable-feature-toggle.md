---
title: Ativar a alternância de recursos para integrar os recursos de pré-lançamento e de adesão antecipada
description: O Feature Toggle é uma funcionalidade do AEM que permite aos administradores ativar novos recursos em um ambiente de tempo de execução.
feature: Adaptive Forms, Foundation Components, Core Components
role: User, Developer
exl-id: 3ad1370a-a399-4fbe-8168-c3a1cee06336
source-git-commit: c1d62f0dd5a25da7fbeef537e1c28fa8421f42cd
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# Ativar a alternância de recursos no Kit de desenvolvimento de software da Adobe Experience (AEM SDK)

A alternância de recursos no AEM permite que os administradores ativem ou desativem recursos no tempo de execução ideais para gerenciar recursos de Pré-lançamento e de Adoção Antecipada sem alterações de código. Ele oferece suporte a implantações graduais, testes A/B e desativação rápida de recursos instáveis.

Este artigo aborda como ativar opções de recursos na configuração do AEM Local SDK, que simula o AEM as a Cloud Service usando o SDK e o Dispatcher. Essa configuração ajuda as equipes a testar em um ambiente semelhante ao de produção antes de implantar na nuvem.

## Por que usar alternadores de recursos na configuração do AEM SDK?

Ao trabalhar em uma configuração do AEM SDK, o recurso alterna a ajuda em:

* Testando características experimentais com segurança.

* Lançando novos componentes em fases.

* Manutenção de uma única base de código em vários ambientes.

* Redução de riscos durante implantações e atualizações.

## Pré-requisitos

Antes de ativar a alternância de recursos na configuração do AEM SDK, verifique o seguinte:

* O usuário é membro do grupo `forms-users`.

* Navegue até `http://<author-instance-url>:portnumber/system/console/bundles` e verifique se o pacote **(com.adobe.granite.toggle.impl.dev-1.1.2.jar)** está presente ou não. Caso não esteja presente, [baixe o pacote do link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]s/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.8.jar).

  ![Alternância de recursos](/help/forms/assets/aem-web-console-bundle.png)

### Ativar alternância de recursos

Siga estas etapas para ativar opções de recursos na instância do AEM SDK:

1. Faça logon na sua instância do AEM Forms.

1. Vá até `http://author-instance-url:portnumber/system/console/configMgr`.

1. Procure o Provedor de alternância dinâmica do Adobe Granite no Gerenciador de configurações.

   ![Alternância de recursos](/help/forms/assets/aem-web-console-confi.png)

1. Clique no ícone ✏️.
1. Na seção Alternâncias Habilitadas, clique em ➕.
1. Adicione a ID de alternância do recurso, como mostrado na imagem abaixo.
   ![Alternância de recursos](/help/forms/assets/feature-toggle.png)

1. Clique em Salvar

>[!NOTE]
>
> Você pode encontrar a ID de alternância de recurso no documento específica para os recursos do adotante inicial.


### Desativar alternância de recursos

Para desativar os recursos para os recursos cujos alternadores estão ativados, siga as etapas abaixo:

1. Faça logon na sua instância do AEM Forms.
1. Vá até `http://author-instance-url:portnumber/system/console/configMgr`.
1. Procure o Provedor de alternância dinâmica do Adobe Granite no Gerenciador de configurações.
1. Clique no ícone ✏️.
1. Na seção Alternâncias Desabilitadas, clique em ➕.
1. Adicione o número de alternância para que o recurso seja desativado.

   ![Alternância de recursos](/help/forms/assets/disable-toggle-feature.png)

### Consideração técnica

Os interruptores de recursos são gerenciados por tempo de execução e são mais adequados para configurações de desenvolvimento ou teste. Em uma configuração do AEM SDK, verifique se os interruptores têm a versão controlada e se estão sincronizados com o CI/CD. Pode ser necessário atualizar a página ou limpar o cache para que as alterações sejam refletidas.

>[!NOTE]
>
> Para ativar o recurso de alternância para o ambiente de produção, entre em contato com a equipe de suporte da Adobe.
