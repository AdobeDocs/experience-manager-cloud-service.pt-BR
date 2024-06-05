---
title: Ferramenta AEM Repo
description: A ferramenta AEM Repo é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor AEM por meio da linha de comando comparável ao FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# Ferramenta AEM Repo {#aem-repo-tool}

A ferramenta AEM Repo é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor AEM por meio da linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante ao [Plug-in Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), mas é mais rápido, tem dependências mínimas e é um script bash simples.

Essa ferramenta simplifica a transferência de arquivos para o desenvolvedor e também pode ser integrada ao Eclipse e ao IntelliJ para tornar o desenvolvimento ainda mais eficiente.

## Visão geral {#overview}

Para um determinado caminho dentro de um `jcr_root` Estrutura FileVault no sistema de arquivos, a ferramenta AEM Repo cria um pacote com um único filtro para toda a subárvore e o envia para o servidor (semelhante ao FTP `put`), o busca no servidor ( `get`) ou compara as diferenças ( `status` e `diff`).

A ferramenta não é compatível com vários caminhos de filtro ou com o `filter.xml`.

>[!CAUTION]
>
>A ferramenta AEM Repo sempre substitui todo o arquivo ou diretório especificado.

## Download e documentação {#download-and-documentation}

A variável [A ferramenta AEM Repo está disponível no GitHub por meio deste link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) juntamente com instruções detalhadas de instalação e uso.

Se você quiser baixar a fonte da ferramenta AEM Repo, consulte o projeto GitHub vinculado abaixo.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto de ferramentas no GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
