---
title: Ferramenta AEM Repo
description: A AEM Repo Tool é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor do AEM por meio da linha de comando comparável ao FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# Ferramenta AEM Repo {#aem-repo-tool}

A AEM Repo Tool é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor do AEM por meio da linha de comando comparável ao FTP. A AEM Repo Tool é semelhante ao [plug-in Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), mas é mais rápida, tem dependências mínimas e é um script bash simples.

Essa ferramenta simplifica a transferência de arquivos para o desenvolvedor e também pode ser integrada ao Eclipse e ao IntelliJ para tornar o desenvolvimento ainda mais eficiente.

## Visão geral {#overview}

Para um determinado caminho dentro de uma estrutura FileVault `jcr_root` no sistema de arquivos, a Ferramenta de Repositório da AEM cria um pacote com um único filtro para toda a subárvore e envia-o para o servidor (semelhante ao FTP `put`), busca-o no servidor ( `get`) ou compara as diferenças ( `status` e `diff`).

A ferramenta não oferece suporte a vários caminhos de filtro ou ao `filter.xml` do FileVault.

>[!CAUTION]
>
>A AEM Repo Tool sempre substitui todo o arquivo ou diretório especificado.

## Download e documentação {#download-and-documentation}

A [AEM Repo Tool está disponível no GitHub neste link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo), juntamente com instruções detalhadas de instalação e uso.

Se quiser baixar a origem da ferramenta AEM Repo, consulte o projeto GitHub vinculado abaixo.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto de ferramentas no GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
