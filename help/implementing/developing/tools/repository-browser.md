---
title: Navegador de repositório
seo-title: Repository Browser
description: O navegador do repositório fornece uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# Navegador de repositório {#repository-browser}

>[!NOTE]
>
>O Navegador do repositório está disponível no AEM versões 6582 e superior.

>[!INFO]
>
>Você também pode assistir a [este clipe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) para obter uma introdução rápida em vídeo sobre como usar o Navegador do Repositório para depurar o AEM as a Cloud Service.

## Introdução {#introduction}

O navegador do repositório é uma ferramenta de desenvolvedor que fornece uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização. Ele foi projetado para facilitar a exibição da estrutura de conteúdo e facilitar a visualização ou depuração do conteúdo.

Acessível a partir do [AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console), ele pode ser usado para procurar o repositório de um autor ou instância de publicação para um ambiente selecionado.

### Pré-requisitos de acesso {#access-prerequisites}

As seguintes condições devem ser atendidas para acessar o AEM as a Cloud Service Developer Console ou o Navegador do repositório

Para acessar o AEM as a Cloud Service Developer Console, consulte [Acesso ao Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access).

Para acessar o Navegador do repositório, os requisitos são os mesmos do AEM as a Cloud Service Developer Console (especificados acima). Para exibir o conteúdo do Navegador do repositório de uma instância específica:

* Instâncias de autor: usuários com o Perfil de Produto de Usuários do AEM para a **Instância de autor** podem exibir o navegador do repositório com acesso mínimo de leitura; as permissões do usuário são respeitadas ao navegar pelo repositório. Os usuários com o Perfil de produto de administradores do AEM podem exibir o navegador do repositório com acesso de leitura completo.

* Instâncias de publicação: os usuários com o Perfil de Produto de Usuários do AEM para a **Instância de publicação** podem exibir o navegador do repositório com acesso mínimo de leitura. Sem esse conjunto de perfis de produto, os usuários navegarão como um usuário anônimo e alguns caminhos não serão exibidos devido a permissões limitadas.

Para obter mais informações sobre como configurar permissões de usuário, consulte a [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html).

### Iniciar o navegador do repositório {#launching-the-repository-browser}

O navegador do repositório pode ser iniciado seguindo as etapas abaixo.

1. No Cloud Manager, clique nos três pontos ao lado do ambiente de sua escolha e selecione **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Em seguida, clique na guia **Navegador do repositório**
1. Escolha qualquer pod correspondente ao autor, publicação ou visualização clicando na lista suspensa **Pod**.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Inicie o navegador do repositório clicando no link **Abrir Navegador do Repositório** mais abaixo. O navegador correspondente a uma instância representativa (pod) do nível escolhido é iniciado. Você não pode controlar o pod específico para esse nível que é iniciado.

## Recursos {#features}

### Navegar pela Hierarquia {#navigate-the-hierarchy}

Você pode usar o painel de navegação esquerdo para navegar pela hierarquia de conteúdo. Clicar em cada pasta ou nó revela seus filhos. A estrutura de pastas reflete a árvore do Sling Resource, que é um superconjunto da árvore de nós JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

Como alternativa, você pode navegar diretamente para um caminho inserindo-o no campo **Caminho**, conforme mostrado abaixo. Esse caminho também expande sua localização na visualização da hierarquia de conteúdo à esquerda.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Ao clicar em uma pasta à esquerda, o campo Caminho é preenchido automaticamente com seu local. Essa funcionalidade é útil para copiar e colar o valor para uso posterior.

Além disso, ao clicar em uma pasta, o URL é modificado dinamicamente para incluir o caminho para essa pasta. Essa funcionalidade permite URLs marcáveis.

Para publicação, por padrão, o Navegador do Repositório mostra apenas conteúdo público, portanto, determinadas pastas como `/conf` ou `/home` não estão visíveis.

Para tornar esses locais visíveis, faça o seguinte.

1. Clique nos três pontos ao lado do ambiente de sua escolha e selecione **Gerenciar Acesso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Encontre sua instância de publicação e clique nela

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Criar um perfil de produto para administradores de publicação. No exemplo abaixo, ele é chamado de **DEV - Publicação de administradores do AEM**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Adicione os usuários apropriados, correspondentes a quem deve ser capaz de navegar pelo navegador do repositório de publicação com acesso total, ao novo perfil de produto

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Aguarde alguns minutos e abra o console **Autor do AEM**
1. Adicione o grupo correspondente ao novo perfil de produto como membro do grupo do administrador clicando em **Ferramentas - Segurança - Grupos no autor** e depois no grupo **administradores**. Em seguida, adicione o grupo como mostrado abaixo

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Ative os **administradores** e o novo grupo **DEV - Publicação de Administradores do AEM** para que eles fiquem disponíveis na publicação

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Como prática de segurança recomendada, remova o novo grupo **DEV - Publicação de Administradores do AEM** do grupo de administradores no **autor** para que o novo grupo seja isolado para publicação

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Ao acessar o navegador do repositório para uma instância de publicação, todas as pastas ficam visíveis, incluindo `/home` e `/conf`.

### Visualizar propriedades do JCR {#view-jcr-properties}

Clicar em um nó revela suas propriedades JCR no painel direito do navegador de navegação. Veja abaixo um exemplo do nó `experience-fragments`.

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Exibir conteúdo {#view-content}

Você pode usar o navegador do repositório para visualizar o conteúdo. Clique em um recurso no painel de navegação para abrir uma visualização no lado direito do navegador, em uma guia nomeada com base no respectivo recurso.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

A visualização está disponível para os seguintes tipos de imagem:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* tiff

E para os seguintes tipos MIME baseados em texto:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Baixar conteúdo {#download-content}

Você também pode usar o navegador do repositório para baixar o conteúdo. No exemplo abaixo, você pode pressionar o link **baixar** para baixar o `jcr:data` associado ao nó selecionado. Esse recurso está disponível para todas as propriedades binárias navegando até o nó que contém a definição da propriedade.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
