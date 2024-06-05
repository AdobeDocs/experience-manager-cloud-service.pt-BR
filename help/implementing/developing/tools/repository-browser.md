---
title: Navegador de repositório
seo-title: Repository Browser
description: O navegador do repositório fornece uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 1%

---

# Navegador de repositório {#repository-browser}

>[!NOTE]
>
>O Navegador do repositório está disponível nas versões AEM 6582 e superior.

>[!INFO]
>
>Você também pode assistir [este clipe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) para obter uma introdução rápida em vídeo sobre como usar o Navegador do repositório para depurar o AEM as a Cloud Service.

## Introdução {#introduction}

O navegador do repositório é uma ferramenta de desenvolvedor que fornece uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização. Ele foi projetado para facilitar a exibição da estrutura de conteúdo e facilitar a visualização ou depuração do conteúdo.

Acessível a partir do [Console do desenvolvedor AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console), ele pode ser usado para navegar pelo repositório de uma instância de autor ou publicação para um ambiente selecionado.

### Pré-requisitos de acesso {#access-prerequisites}

Estas condições devem ser atendidas para acessar o Console do desenvolvedor as a Cloud Service AEM ou o navegador do Repositório

Para acessar o Console do desenvolvedor do AEM as a Cloud Service:

* Para programas de Produção, os usuários devem ter o **Cloud Manager - Função do desenvolvedor** no Adobe Admin Console
* Para programas de sandbox, está disponível para qualquer usuário com um perfil de produto que dê acesso ao AEM as a Cloud Service.

Para acessar o Navegador do repositório:

* Os usuários devem ter o **Cloud Manager - Desenvolvedor** Função no Console do desenvolvedor as a Cloud Service AEM para exibir instâncias de Autor e Publicação.
* Além disso, para o autor, os usuários com o Perfil de produto de usuários AEM podem visualizar o navegador do repositório com acesso mínimo de leitura; as permissões do usuário são respeitadas ao navegar pelo repositório. Os usuários com o Perfil de produto de administradores do AEM podem visualizar o navegador do repositório com acesso de leitura completo.

Para obter mais informações sobre a configuração de permissões de usuário, consulte [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html).

### Iniciar o navegador do repositório {#launching-the-repository-browser}

O navegador do repositório pode ser iniciado seguindo as etapas abaixo.

1. No Cloud Manager, clique nos três pontos ao lado do ambiente de sua escolha e selecione **Console do desenvolvedor**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Clique em **Navegador do repositório** guia
1. Escolha qualquer pod correspondente ao autor, publicação ou visualização clicando no **Pod** lista suspensa.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Inicie o navegador do repositório clicando no ícone **Abrir navegador do repositório** mais abaixo. O navegador correspondente a uma instância representativa (pod) do nível escolhido é iniciado. Você não pode controlar o pod específico para esse nível que é iniciado.

## Recursos {#features}

### Navegar pela Hierarquia {#navigate-the-hierarchy}

Você pode usar o painel de navegação esquerdo para navegar pela hierarquia de conteúdo. Clicar em cada pasta ou nó revela seus filhos. A estrutura de pastas reflete a árvore do Sling Resource, que é um superconjunto da árvore de nós JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

Como alternativa, você pode navegar diretamente para um caminho inserindo-o na **Caminho** como mostrado abaixo. Esse caminho também expande sua localização na visualização da hierarquia de conteúdo à esquerda.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Ao clicar em uma pasta à esquerda, o campo Caminho é preenchido automaticamente com seu local. Essa funcionalidade é útil para copiar e colar o valor para uso posterior.

Além disso, ao clicar em uma pasta, o URL é modificado dinamicamente para incluir o caminho para essa pasta. Essa funcionalidade permite URLs marcáveis.

Para publicação, por padrão, o Navegador do repositório mostra apenas o conteúdo público, portanto, determinadas pastas, como `/conf` ou `/home` não estão visíveis.

Para tornar esses locais visíveis, faça o seguinte.

1. Clique nos três pontos ao lado do ambiente de sua escolha e selecione **Gerenciar acesso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Encontre sua instância de publicação e clique nela

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Criar um perfil de produto para administradores de publicação. No exemplo abaixo, ele é chamado de **DEV - Publicação de administradores do AEM**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Adicione os usuários apropriados, correspondentes a quem deve ser capaz de navegar pelo navegador do repositório de publicação com acesso total, ao novo perfil de produto

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Aguarde alguns minutos e abra a janela **Autor do AEM** console
1. Adicione o grupo correspondente ao novo perfil de produto como membro do grupo do administrador clicando em **Ferramentas - Segurança - Grupos no autor** e, em seguida, clicando na guia **administradores** grupo. Em seguida, adicione o grupo como mostrado abaixo

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Ativar o **administradores** e o novo **DEV - Publicação de administradores do AEM** para que fiquem disponíveis na publicação

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Como uma boa prática de segurança, remova o novo **DEV - Publicação de administradores do AEM** grupo do grupo do administrador em **autor** portanto, o novo grupo é isolado para publicação

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Ao acessar o navegador do repositório de uma instância de publicação, todas as pastas ficam visíveis, incluindo `/home` e `/conf`.

### Visualizar propriedades do JCR {#view-jcr-properties}

Clicar em um nó revela suas propriedades JCR no painel direito do navegador de navegação. Veja abaixo um exemplo de `experience-fragments` nó.

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

Você também pode usar o navegador do repositório para baixar o conteúdo. No exemplo abaixo, você pode pressionar a tecla **baixar** link para baixar o `jcr:data` associado ao nó selecionado. Esse recurso está disponível para todas as propriedades binárias navegando até o nó que contém a definição da propriedade.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
