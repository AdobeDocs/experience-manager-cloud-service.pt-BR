---
title: Aplicativo de amostra do SecurBank para o editor universal
description: Saiba mais sobre o Universal Editor com experiência prática usando o aplicativo SecurBank, projetado para mostrar a eficiência, a flexibilidade e a usabilidade do Universal Editor para acelerar a criação de conteúdo.
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Aplicativo de amostra do SecurBank para o editor universal {#securbank}

Saiba mais sobre o Universal Editor com experiência prática usando o aplicativo SecurBank, projetado para mostrar a eficiência, a flexibilidade e a usabilidade do Universal Editor para acelerar a criação de conteúdo.

## Pré-requisitos {#prerequisites}

* Você deve ser atribuído ao **Administrador do AEM** [perfil de produto](/help/journey-onboarding/assign-profiles-aem.md) para instalar o aplicativo SecurBank.
* Você deve ter o [Node.js](https://nodejs.org) versão 20 ou superior instalado para desenvolvimento local.

## Instalando o SecurBank {#installation}

A instalação do aplicativo SecurBank é direta, mas como ele abrange muitas áreas do AEM as a Cloud Service, várias etapas estão envolvidas. Veja a seguir uma visão geral das principais etapas.

1. [Criar um programa de sandbox no Cloud Manager](#create-sandbox-program).
1. [Clone o repositório Git do programa e atualize com o conteúdo do projeto AEM do SecurBank](#clone-and-update).
1. [Execute o pipeline para implantar o projeto AEM do SecurBank](#run-pipeline).
1. [Recupere as credenciais do Cloud Manager para o desenvolvimento do aplicativo Web local](#retrieve-credentials).
1. [Baixe e configure o aplicativo Web SecurBank](#download-web-app).
1. [Execute o aplicativo Web SecurBank](#run-web-app).

As seções a seguir detalham as tarefas individuais necessárias.

### Crie um programa de sandbox na Cloud Manager. {#create-sandbox-program}

Você precisará de um novo programa Cloud Manager, no qual poderá instalar o SecurBank.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada

1. Crie um novo programa de sandbox para o aplicativo SecurBank.

   * Use as opções padrão ao selecionar **Soluções e Complementos**.
   * Para obter detalhes sobre como criar um programa de sandbox, consulte o documento [Criação de programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).

### Clonar o repositório Git do programa e atualizar com o conteúdo do projeto AEM do SecurBank. {#clone-and-update}

1. Depois que o programa for criado, abra-o e, na guia **Repositórios**, toque ou clique no botão **Acessar informações do repositório** para abrir a caixa de diálogo **Informações do repositório** e exibir as credenciais necessárias para acessar o repositório Git do ambiente de sandbox.

   * Para obter detalhes sobre como acessar as informações do repositório, consulte o documento [Acessando repositórios](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Usando as credenciais na caixa de diálogo **Informações do Repositório**, clone o repositório no computador local.

1. Localize a pasta do clone local, abra-a e exclua todo o conteúdo exceto os arquivos ocultos/pontos.

1. Recupere o código de projeto do SecurBank AEM mais recente do GitHub em [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) clicando em **Código** e depois em **Baixar ZIP** na lista suspensa.

1. Descompacte o conteúdo do arquivo zip em seu sistema de arquivos local e mova-o para a pasta agora vazia do clone local do programa sandbox.

1. Usando o terminal, alterne para a pasta do projeto clonado, confirme todo o conteúdo e envie-o para o Git.

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### Execute o pipeline para implantar o projeto AEM do SecurBank. {#run-pipeline}

Com o projeto AEM do SecurBank comprometido com o repositório de sandbox, ele pode ser implantado com um pipeline.

1. Retorne à guia **Visão geral** do seu programa de sandbox na Cloud Manager e execute o pipeline de não produção de pilha completa.

   * Desmarque todas as opções para a execução do pipeline.
   * Para obter mais informações sobre como executar pipelines, consulte o documento [Gerenciamento de pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines).

### Recupere as credenciais do Cloud Manager para o desenvolvimento de aplicativos Web locais. {#retrieve-credentials}

Antes de executar o aplicativo SecurBank, você precisará de credenciais do Cloud Manager para conectar o aplicativo ao Cloud Manager.

1. Como o pipeline está em execução, retorne à guia **Visão geral** no Cloud Manager, toque ou clique no botão de reticências ao lado do nome do ambiente e selecione **Developer Console**.

1. Na Developer Console, selecione a guia **Integrações** e depois a guia **Token Local** e toque ou clique em **Obter Token de Desenvolvimento Local**.

1. Um arquivo JSON é produzido com o token de acesso. Copie somente o token em si (o JSON restante não é necessário) para um local seguro para uso em uma etapa futura antes de fechar o Developer Console e retornar ao Cloud Manager.

1. De volta ao Cloud Manager, na guia **Visão geral**, clique com o botão direito do mouse na URL do ambiente para copiá-la e salvá-la em um local seguro para uso em uma etapa futura.

### Baixe e configure o aplicativo Web SecurBank. {#download-web-app}

Agora é possível baixar e configurar o aplicativo Web SecurBank.

1. Recupere o código do aplicativo SecurBank mais recente do GitHub em [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) clicando em **Código** e depois em **Baixar ZIP** na lista suspensa.

1. Descompacte o conteúdo do arquivo zip no sistema de arquivos local.

1. Inicie seu editor de código preferido e abra o arquivo de ambiente oculto no projeto de aplicativo SecurBank em `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. Faça as seguintes alterações no arquivo `.env` e salve-as.

   * Para `REACT_APP_HOST_URI`, cole o valor da URL copiada anteriormente do seu ambiente.
   * Para `REACT_APP_DEV_TOKEN`, cole o valor do token de desenvolvimento local copiado anteriormente.

### Execute o aplicativo Web SecurBank. {#run-web-app}

Com tudo configurado no Cloud Manager e localmente, é possível executar o aplicativo Web SecurBank.

1. Na linha de comando do computador local, navegue até a pasta `react-app` do projeto de aplicativo SecurBank que você baixou e descompactou.

1. Na pasta `react-app`, instale o aplicativo SecurBank com o comando `node -i`.

1. Depois de instalado, inicie o aplicativo SecurBank com o comando `npm start`.

1. Se a instalação e o início forem bem-sucedidos, você verá:

* A seguinte saída no terminal.

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * E uma janela do navegador aberta para a URL `https://localhost:3000`.

      * Observe que isso é para fins de desenvolvimento e, como tal, nenhum certificado válido é fornecido. Dessa forma, talvez seja necessário informar seu navegador para permitir que ele acesse a página.

Parabéns! Agora você deve ver o aplicativo SecurBank sendo executado com sucesso em seu navegador.

Se o conteúdo ainda não for exibido, verifique se o pipeline **Implantar no Desenvolvimento** que você executou foi concluído com êxito.

![Aplicativo SecurBank no navegador](assets/securbank.png)

{{ue-headless-auth}}

