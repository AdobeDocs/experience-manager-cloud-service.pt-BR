---
title: Ferramenta AEM Repo
description: A ferramenta AEM Repo é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM pela linha de comando comparável ao FTP.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Ferramenta AEM Repo {#aem-repo-tool}

A ferramenta AEM Repo é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM pela linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante ao plug-in [](https://jackrabbit.apache.org/filevault-package-maven-plugin)Jackrabbit FileVault Maven, mas é mais rápida, tem dependências mínimas e é um script bash simples.

Essa ferramenta simplifica a transferência de arquivos para o desenvolvedor e também pode ser integrada ao Eclipse e ao IntelliJ para tornar o desenvolvimento ainda mais eficiente.

## Visão geral {#overview}

Para um determinado caminho dentro de uma estrutura do `jcr_root` FileVault no sistema de arquivos, a ferramenta AEM Repo cria um pacote com um único filtro para toda a subárvore e empurra-o para o servidor (semelhante ao FTP `put`), o obtém do servidor ( `get`) ou compara as diferenças ( `status` e `diff`).

A ferramenta não oferece suporte a vários caminhos de filtro ou ao FileVault `filter.xml`.

>[!CAUTION]
>
>Observe que a ferramenta AEM Repo sempre substituirá todo o arquivo ou diretório especificado.

## Download e documentação {#download-and-documentation}

A ferramenta [AEM Repo está disponível no GitHub por meio deste link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) , juntamente com instruções detalhadas de instalação e uso.

Se desejar baixar a fonte da ferramenta AEM Repo, consulte o projeto GitHub vinculado abaixo.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto de ferramentas no GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
