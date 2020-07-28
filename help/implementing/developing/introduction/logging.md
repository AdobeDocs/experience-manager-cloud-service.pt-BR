---
title: Registro
description: Saiba como configurar parâmetros globais para o serviço de registro central, configurações específicas para os serviços individuais ou como solicitar registro de dados.
translation-type: tm+mt
source-git-commit: a7c8e1ab8e0196a3a79d8e0963192775e64a2400
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Registro {#logging}

AEM como um Cloud Service é uma plataforma para os clientes incluírem código personalizado para criar experiências exclusivas para sua base de clientes. Com isso em mente, o registro em log é uma função essencial para depurar e entender a execução do código no desenvolvimento local, e ambientes em nuvem, especialmente o AEM como ambientes Cloud Service Dev.

Os níveis de registro e registro AEM são gerenciados em arquivos de configuração armazenados como parte do projeto AEM no Git e implantados como parte do projeto AEM pelo Cloud Manager. Fazer logon AEM como um Cloud Service pode ser dividido em dois conjuntos lógicos:

* AEM registro, que executa o registro em log no nível do aplicativo AEM
* Apache HTTPD Web Server/Dispatcher logging, que executa o log do servidor da Web e do Dispatcher na camada Publicar.

## Registro de AEM {#aem-loggin}

O registro no nível do aplicativo AEM é realizado por três registros:

1. AEM registros Java, que renderizam declarações de registro Java para o aplicativo AEM.
1. Registros de solicitação HTTP, que registram informações sobre solicitações HTTP e suas respostas fornecidas por AEM
1. Registros de acesso HTTP, que registram informações resumidas e solicitações HTTP fornecidas por AEM

Observe que as solicitações HTTP fornecidas pelo cache do Dispatcher da camada de publicação ou pelo CDN upstream não são refletidas nesses logs.

### AEM registro em Java {#aem-java-logging}

AEM como um Cloud Service fornece acesso às instruções do log Java Os desenvolvedores de aplicativos para AEM devem seguir as práticas recomendadas gerais de registro em Java, registrando declarações pertinentes sobre a execução do código personalizado, nos seguintes níveis de registro:

<table>
<tbody>
<tr>
<td> <b>Ambiente AEM</b></td>
<td> <b>Nível de registro</b></td>
<td> <b>Descrição</b></td>
<td> <b>Disponibilidade do demonstrativo de registro</b></td>
</tr>
<tr>
<td> Desenvolvimento</td>
<td> DEPURAR</td>
<td> Descreve o que está acontecendo no aplicativo.

Quando o registro DEBUG estiver ativo, as declarações que fornecem uma imagem clara do que ocorre com as atividades, bem como quaisquer parâmetros chave que afetam o processamento, são registradas em log.</td>
<td> <ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
</ul></td>
</tr>
<tr>
<td> Estágio</td>
<td> AVISO</td>
<td> Descreve as condições que podem se tornar erros.

Quando o registro em log do WARN estiver ativo, somente as declarações indicando os condicionais que estão se aproximando da subotimização serão registradas.</td>
<td> <ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
<li>Estágio</li>
</ul></td>
</tr>
<tr>
<td> Produção</td>
<td> ERRO</td>
<td> Descreve as condições que indicam uma falha e que precisam ser resolvidas.

Quando o registro em log ERROR está ativo, somente as declarações que indicam falhas são registradas em log. Declarações de log de ERROS indicam um problema grave que deve ser resolvido o mais rápido possível.</td>
<td> <ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
<li>Estágio</li>
<li>Produção</li>
</ul></td>
</tr>
</tbody>
</table>