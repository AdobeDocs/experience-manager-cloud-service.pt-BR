---
title: Recuperar informações de acesso do repositório Git
description: Saiba como o desenvolvedor de front-end usa o Cloud Manager para acessar informações de repositório Git.
exl-id: 3ef1cf86-6da4-4c09-9cfc-acafc8f6dd5c
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 4%

---

# Recuperar informações de acesso do repositório Git {#retrieve-access}

Saiba como o desenvolvedor de front-end usa o Cloud Manager para acessar informações de repositório Git.

## A História Até Agora {#story-so-far}

Se você for um desenvolvedor de front-end responsável apenas pela personalização do tema do site, não precisará de conhecimento sobre como o AEM foi configurado e poderá pular para o [Objetivo](#objective) seção deste documento.

Se você também desempenha a função de administrador do Cloud Manager ou de AEM, bem como de desenvolvedor front-end, você aprendeu no documento anterior da jornada AEM Quick Site Creation, [Conceder acesso ao desenvolvedor de front-end,](grant-access.md) como integrar o desenvolvedor de front-end para que ele tenha acesso ao repositório Git, e agora você deve saber:

* Como adicionar um desenvolvedor de front-end como usuário.
* Como conceder as funções necessárias ao desenvolvedor de front-end.

Este artigo tira a próxima etapa de mostrar como o desenvolvedor front-end usa o acesso do Cloud Manager para recuperar credenciais para acessar o repositório Git AEM.

Agora que há um site criado com base em um modelo, há um pipeline configurado, o desenvolvedor front-end é integrado e tem todas as informações necessárias, este artigo afasta a perspectiva dos administradores e exclusivamente para a função de desenvolvedor front-end.

## Objetivo {#objective}

Este documento explica como você, na função de desenvolvedor front-end, pode acessar o Cloud Manager e recuperar credenciais de acesso ao repositório Git AEM. Depois de ler, você:

* Entenda em alto nível o que é o Cloud Manager.
* Recuperou suas credenciais para acessar o git de AEM para confirmar as personalizações.

## Função responsável {#responsible-role}

Essa parte da jornada se aplica ao desenvolvedor de front-end.

## Requisitos {#requirements}

A ferramenta de Criação rápida de sites permite que desenvolvedores de front-end trabalhem de maneira independente sem ter conhecimento de AEM ou como ela é configurada. No entanto, o administrador do Cloud Manager deve integrar o desenvolvedor de front-end na equipe do projeto e o administrador do AEM deve fornecer algumas informações necessárias. Certifique-se de ter as seguintes informações antes de continuar.

* No administrador AEM:
   * Arquivos de origem de tema a serem personalizados
   * Caminho para uma página de exemplo a ser usada como base de referência
   * Credenciais do usuário proxy para testar suas personalizações em relação ao conteúdo do live AEM
   * Requisitos de concepção de front-end
* No administrador do Cloud Manager:
   * Um email de boas-vindas do Cloud Manager que informa você sobre o acesso
   * O nome do programa ou o URL para ele no Cloud Manager

Se você não tiver nenhum desses itens, entre em contato com o administrador do AEM ou com o administrador do Cloud Manager.

Pressupõe-se que o desenvolvedor de front-end tenha ampla experiência com fluxos de trabalho de desenvolvimento de front-end e com ferramentas comuns instaladas, incluindo:

* git
* npm
* webpack
* Um editor preferencial

## Noções básicas sobre o Cloud Manager {#understanding-cloud-manager}

O Cloud Manager permite que as organizações autogerenciem AEM na nuvem. Inclui uma estrutura de integração contínua e entrega contínua (CI/CD) que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações, sem comprometer o desempenho ou a segurança.

Para o desenvolvedor de front-end, é o gateway para:

* Acesse AEM informações do repositório Git para confirmar as personalizações de front-end.
* Inicie o pipeline de implantação para implantar suas personalizações.

O administrador do Cloud Manager terá integrado você como um usuário do Cloud Manager. Você deve ter recebido um email de boas-vindas semelhante ao seguinte.

![Email de boas-vindas](assets/welcome-email.png)

Se você não recebeu esse email, entre em contato com o administrador do Cloud Manager.

## Access Cloud Manager {#access-cloud-manager}

1. Faça logon no Adobe Experience Cloud em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) ou clique no link fornecido no email de boas-vindas.

1. O Cloud Manager lista os vários programas disponíveis. Toque ou clique no link que você precisa acessar, conforme fornecido pelo administrador do Cloud Manager. Se esse for seu primeiro projeto front-end para AEMaaCS, você provavelmente terá apenas um programa disponível.

   ![Seleção de um programa no Cloud Manager](assets/cloud-manager-select-program.png)

Agora você verá uma visão geral do seu programa. Sua página será diferente, mas semelhante a este exemplo.

![Visão geral do Cloud Manager](assets/cloud-manager-overview.png)

## Recuperar informações de acesso do repositório {#repo-access}

1. No **Pipelines** na página Cloud Manager , toque ou clique no botão **Acessar informações do repositório** botão.

   ![Pipelines](assets/pipelines-repo-info.png)

1. O **Informações do repositório** será aberta.

   ![Informações do acordo de recompra](assets/repo-info.png)

1. Toque ou clique no botão **Gerar senha** para criar uma senha para você mesmo.

1. Salve a senha gerada em um gerenciador de senhas seguro. A senha nunca será exibida novamente.

1. Copie também a **username** e **Linha de comando Git** campos. Você usará essas informações posteriormente para acessar o acordo de recompra.

1. Toque ou clique **Fechar**.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de Criação de Site Rápido de AEM, é necessário:

* Entenda em alto nível o que é o Cloud Manager.
* Recuperou suas credenciais para acessar o git de AEM para confirmar as personalizações.

Crie com base nesse conhecimento e prossiga sua jornada de Criação de Site Rápido de AEM revisando o documento [Personalizar o Tema do Site,](customize-theme.md) onde você aprenderá como o tema do site é criado, como personalizar e como testar usando conteúdo de AEM ao vivo.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Site revisando o documento [Personalizar o Tema do Site,](customize-theme.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Documentação do Adobe Experience Manager Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=pt-BR) - Explore a documentação do Cloud Manager para obter detalhes completos sobre seus recursos.
