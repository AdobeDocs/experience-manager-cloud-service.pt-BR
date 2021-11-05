---
title: Personalizar o Tema do Site
description: Saiba como o tema do site é criado, como personalizar e como testar usando conteúdo de AEM ao vivo.
source-git-commit: 348e26a9af260d89841d19d00ce4102c00ae34ed
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---


# Personalizar o Tema do Site {#customize-the-site-theme}

Saiba como o tema do site é criado, como personalizar e como testar usando conteúdo de AEM ao vivo.

>[!CAUTION]
>
>No momento, a ferramenta Criação rápida de site é uma visualização técnica. É disponibilizado para fins de ensaio e avaliação e não se destina à utilização da produção, a menos que acordado com o apoio ao Adobe.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de Criação AEM de Site Rápido, [Recuperar informações de acesso do repositório Git,](retrieve-access.md) você aprendeu como os usuários front-end do desenvolvedor do Cloud Manager acessam as informações do repositório Git e agora deve:

* Entenda em alto nível o que é o Cloud Manager.
* Recuperou suas credenciais para acessar o git de AEM para confirmar as personalizações.

Essa parte da jornada dá o próximo passo e desenha o tema do site e mostra como personalizá-la e depois confirmar essas personalizações usando as credenciais de acesso recuperadas.

## Objetivo {#objective}

Este documento explica como o tema do site AEM é criado, como personalizá-lo e como testá-lo usando conteúdo AEM ativo. Depois de ler, você deve:

* Entenda a estrutura básica do tema do site e como editá-lo.
* Veja como testar as personalizações de tema usando conteúdo de AEM real por proxy local.
* Saiba como confirmar as alterações no repositório Git AEM.

## Função responsável {#responsible-role}

Essa parte da jornada se aplica ao desenvolvedor de front-end.

## Entender a estrutura do tema {#understand-theme}

Extraia o tema fornecido pelo administrador do AEM para onde deseja editar o tema e abri-lo no editor preferido.

![Edição do tema](assets/edit-theme.png)

Você vê que o tema é um projeto front-end típico. As partes mais importantes da estrutura são:

* `src/main.ts`: O principal ponto de entrada do seu tema JS &amp; CSS
* `src/site`: Arquivos JS e CSS que se aplicam a todo o site
* `src/components`: Arquivos JS e CSS específicos para componentes AEM
* `src/resources`: Arquivos estáticos como ícones, logotipos e fontes

>[!TIP]
>
>Se você quiser saber mais sobre o tema padrão do AEM site, consulte o link GitHub na seção [Recursos adicionais](#additional-resources) no final deste documento.

Quando estiver confortável com a estrutura do projeto de tema, inicie o proxy local para que possa ver quaisquer personalizações de tema em tempo real com base no conteúdo real do AEM.

## Iniciando o Proxy Local {#starting-proxy}

1. Na linha de comando, navegue até a raiz do tema no computador local.
1. Executar `npm install` e npm recupera dependências e instala o projeto.

   ![instalação do npm](assets/npm-install.png)

1. Executar `npm run live` e o servidor proxy é iniciado.

   ![npm run live](assets/npm-run-live.png)

1. Quando o servidor proxy é iniciado, ele abre automaticamente um navegador para `http://localhost:7001/`. Toque ou clique **FAZER LOGON LOCALMENTE (SOMENTE TAREFAS DE ADMINISTRADOR)** e entre com as credenciais do usuário proxy fornecidas pelo administrador do AEM.

   ![Fazer logon localmente](assets/sign-in-locally.png)

1. Depois de fazer logon, altere o URL no navegador para apontar para o caminho para o conteúdo de amostra que o administrador do AEM forneceu a você.

   * Por exemplo, se o caminho fornecido foi `/content/<your-site>/en/home.html?wcmmode=disabled`
   * Você alteraria o URL para `http://localhost:7001/content/<your-site>/en/home.html?wcmmode=disabled`

   ![Conteúdo de amostra proxy](assets/proxied-sample-content.png)

Você pode navegar pelo site para explorar o conteúdo. O site é extraído ao vivo da instância de AEM ao vivo para que você possa fazer suas personalizações de tema em relação ao conteúdo real.

## Personalizar o Tema {#customize-theme}

Agora você pode começar a personalizar o tema. Este é um exemplo simples para ilustrar como você pode ver suas alterações ao vivo por meio do proxy.

1. No editor, abra o arquivo `<your-theme-sources>/src/site/_variables.scss`

   ![Editar tema](assets/edit-theme.png)

1. Editar a variável `$color-background` e defina-o como um valor diferente de branco. Neste exemplo, `orange` é usada.

   ![Tema editado](assets/edited-theme.png)

1. Ao salvar o arquivo, você vê que o servidor proxy reconhece a alteração através da linha `[Browsersync] File event [change]`.

   ![Browsersync de proxy](assets/proxy-browsersync.png)

1. Ao retornar ao navegador do servidor proxy, a alteração é imediatamente visível.

   ![Tema laranja](assets/orange-theme.png)

Você pode continuar personalizando o tema com base nos requisitos fornecidos pelo administrador do AEM.

## Confirmando as Alterações {#committing-changes}

Depois que as personalizações forem concluídas, você poderá confirmá-las no repositório Git AEM. Primeiro, você deve clonar o repositório no computador local.

1. Na linha de comando, navegue até o local em que deseja clonar o acordo de recompra.
1. Execute o comando [anteriormente recuperado do Cloud Manager.](retrieve-access.md) Deve ser semelhante a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`. Use o nome de usuário e a senha do git que [você recuperou na parte anterior desta jornada.](retrieve-access.md)

   ![Clone o repositório](assets/clone-repo.png)

1. Mova o projeto de tema que você estava editando para o repositório clonado com um comando semelhante a `mv <site-theme-sources> <cloned-repo>`
1. No diretório do repositório clonado, confira os arquivos de tema que você acabou de mover com os seguintes comandos.

   ```text
   git add .
   git commit -m "Adding theme sources"
   git push
   ```

1. As personalizações são enviadas para o repositório Git AEM.

   ![Alterações confirmadas](assets/changes-committed.png)

Suas personalizações agora são armazenadas com segurança no repositório Git AEM.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de Criação de Site Rápido de AEM, é necessário:

* Entenda a estrutura básica do tema do site e como editá-lo.
* Veja como testar as personalizações de tema usando conteúdo de AEM real por proxy local.
* Saiba como confirmar as alterações no repositório Git AEM.

Crie com base nesse conhecimento e prossiga sua jornada de Criação de Site Rápido de AEM revisando o documento [Implante Seu Tema Personalizado,](deploy-theme.md) onde você aprenderá a implantar o tema usando o pipeline front-end.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Site revisando o documento [Implante Seu Tema Personalizado,](deploy-theme.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Tema do Site AEM](https://github.com/adobe/aem-site-template-standard-theme-e2e) - Este é o repositório GitHub do Tema do Site AEM.
* [npm](https://www.npmjs.com) - AEM temas usados para criar sites rapidamente se baseiam em npm.
* [webpack](https://webpack.js.org) - AEM temas usados para criar sites rapidamente dependem do webpack.