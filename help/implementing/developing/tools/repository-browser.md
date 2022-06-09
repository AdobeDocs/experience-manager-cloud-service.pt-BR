---
title: Navegador de repositório
seo-title: Repository Browser
description: O navegador de repositório fornece uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: b4d28a0c827fb07d6f731118078ecdf448e2f58b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Navegador de repositório {#repository-browser}

>[!NOTE]
>
>O Navegador de Repositório está disponível AEM versões 6582 e posteriores.

>[!INFO]
>
>Você também pode assistir [este clipe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) para obter uma introdução rápida sobre como usar o Navegador de repositório para depurar AEM as a Cloud Service.

## Introdução {#introduction}

O navegador de repositório é uma ferramenta de desenvolvedor que fornece uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização. Ele foi projetado para facilitar a visualização da estrutura de conteúdo, de modo a facilitar a visualização ou a depuração do conteúdo.

Acessível pelo Console do desenvolvedor, ele pode ser usado para navegar pelo repositório de uma instância de autor ou publicação para um ambiente selecionado.

### Pré-requisitos de acesso {#access-prerequisites}

Essas condições devem ser atendidas para acessar o Console do desenvolvedor ou o navegador do repositório

Para acessar o Console do desenvolvedor:

* Para programas de Produção, os usuários devem ter a variável **Cloud Manager - Função do desenvolvedor** na Admin Console
* Para programas sandbox, ele está disponível para qualquer usuário com um perfil de produto que dá acesso a AEM as a Cloud Service.

Para acessar o Navegador de Repositório:

* Os usuários devem ter a **Cloud Manager - Desenvolvedor** Função no Admin Console para exibir instâncias de Autor e Publicação.
* Além disso, para o autor, os usuários com o Perfil de produto Usuários AEM podem visualizar o navegador do repositório com acesso mínimo de leitura; as permissões do usuário são respeitadas ao navegar no repositório. Os usuários com o Perfil de produto Administradores de AEM podem visualizar o navegador do repositório com acesso total de leitura.

Para obter mais informações sobre como configurar permissões de usuário, consulte o [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Iniciar o Navegador de Repositório {#launching-the-repository-browser}

O navegador de repositório pode ser iniciado seguindo as etapas abaixo.

1. No Cloud Manager, clique nos três pontos ao lado do ambiente de sua escolha e selecione **Console do desenvolvedor**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Em seguida, clique no botão **Navegador de Repositório** guia
1. Escolha qualquer pod correspondente a autor, publicar ou visualizar clicando no botão **Pod** lista suspensa.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Inicie o navegador do repositório clicando no **Abrir navegador do repositório** link mais abaixo. Isso iniciará o navegador correspondente a uma instância representativa (pod) do nível escolhido. Isso iniciará o navegador correspondente a uma instância representativa (pod) do nível escolhido. Observe que não é possível controlar o pod específico para essa camada que é iniciada.

## Recursos {#features}

### Navegar pela Hierarquia {#navigate-the-hierarchy}

Você pode usar o painel de navegação esquerdo para navegar pela hierarquia de conteúdo. Clicar em cada pasta ou nó revelará seus filhos. A estrutura de pastas reflete a árvore do Recurso do Sling, que é um superconjunto da árvore do Nó JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

<!-- Alexandru: temporarily commenting this out, please don't delete. 

Alternatively, you can navigate directly to a path by entering it in the **Path** field, as shown below. This will also expand its location in the content hierarcy view on the left.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Whenever you click a folder on the left, the Path field automatically populates with its location. This is useful for copying and pasting the value for later usage.

Additionally, when you click on a folder, the URL is dynamically modified to include the path to that folder. This allows for bookmarkable URLs.

-->

Por padrão, para publicar, o Navegador de Repositório mostrará somente conteúdo público, portanto determinadas pastas como `/conf` ou `/home` não estará visível.

Para tornar esses locais visíveis, você precisa seguir o procedimento abaixo.

1. Clique nos três pontos ao lado do ambiente de sua escolha e selecione **Gerenciar acesso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Encontre sua instância de publicação e clique nela

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Crie um novo perfil de produto para administradores de publicação. No exemplo abaixo, é chamado de **DEV - Publicação dos administradores de AEM**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Adicione os usuários apropriados, correspondentes a quem deve ser capaz de navegar pelo navegador de repositório de publicação com acesso total, ao novo perfil de produto

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Aguarde alguns minutos e abra o **Autor AEM** console
1. Adicione o grupo correspondente ao novo perfil de produto como um membro do grupo de administradores . Você pode fazer isso clicando em **Ferramentas - Segurança - Grupos no autor**, em seguida, clicando no botão **administradores** grupo. Em seguida, adicione o grupo como mostrado abaixo

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Ative o **administradores** e o novo **DEV - Publicação dos administradores de AEM** para que fiquem disponíveis na publicação

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Como uma boa prática de segurança, remova o novo **DEV - Publicação dos administradores de AEM** grupo do grupo de administradores em **autor** assim, o novo grupo é isolado para publicar

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Ao acessar o navegador de repositório para uma instância de publicação, todas as pastas são visíveis, incluindo `/home` e `/conf`.

### Exibir propriedades do JCR {#view-jcr-properties}

Clicar em um nó revelará as propriedades do JCR no painel direito do navegador de navegação. Abaixo está um exemplo para a variável `experience-fragments` nó .

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Exibir conteúdo {#view-content}

Você pode usar o navegador do repositório para exibir o conteúdo clicando em um recurso no painel de navegação. Isso abrirá uma visualização no lado direito do navegador, em uma guia nomeada após o respectivo recurso.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

A visualização está disponível atualmente para tipos de imagem na lista abaixo:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* ícone x
* tiff

E para os seguintes tipos MIME baseados em texto:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Baixar conteúdo {#download-content}

Você também pode usar o navegador do repositório para baixar conteúdo. No exemplo abaixo, você pode pressionar a tecla **download** link para baixar o `jcr:data` associado ao nó selecionado. Esse recurso está disponível para todas as propriedades binárias, navegando até o nó que contém a definição da propriedade.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
