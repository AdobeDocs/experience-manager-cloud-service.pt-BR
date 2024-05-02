---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 79dcf8a4e9834beeb466ed9270a3f5c6aa67aa9a
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 15%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 16145 {#release-16145}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 16145, lançada publicamente em quinta-feira, 1 de maio de 2024. A versão de manutenção anterior era a versão 15977.

A Ativação de recursos do 2024.4.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-16145}

* ASSETS-23489: melhorias nos insights do repositório.
* ASSETS-26926: melhorias na sondagem de upload do Dynamic Media.
* ASSETS-30351: a caixa de diálogo de download deve carregar os tamanhos de representação do Dynamic Media de forma assíncrona.
* ASSETS-30379: Melhore a resolução de licenças de DRM no download.
* ASSETS-31058: Superfície as representações de corte inteligente na interface do usuário de ativos AEM na guia representações e gere imagens cortadas inteligentes quando o usuário clica nessas representações.
* ASSETS-31218: adicione suporte para smartcrop nomeado na api de entrega de ativos.
* ASSETS-31979: adicione o indicador visual e desative as funções da interface durante as operações de Ativos assíncronos.
* ASSETS-32735: melhorias nos metadados de ativos evento atualizado.
* ASSETS-34661: API para Visualização do DM e/ou URLs de entrega do AEMaaCS Publish.
* ASSETS-37259: melhorias na análise do XMP.
* ASSETS-37263: permite o cancelamento de trabalhos assíncronos de Ativos com falha.
* CNTBF-114: Melhorias no fluxo de retorno de conteúdo.
* CNTBF-148: Melhorias no fluxo de retorno de conteúdo.
* CQ-4356992: Últimas traduções para AEM e Granite.
* SITES-19326: Atualizar links na interface do usuário do Assets para abrir o CF no novo Editor de CF.
* SITES-20686: GraphQL - Exponha a URL do Dynamic Media via _dmS7Url (para ativos que não são de imagens).
* SKYOPS-68091: Atualização para Java 11.0.20.

### Problemas corrigidos {#fixed-issues-16145}

* ASSETS-32321: a resolução do fluxo de trabalho de pós-processamento falha se a pasta antecessora não tiver o subnó &quot;jcr:content&quot;.
* ASSETS-33856: a predefinição de imagem do JPEG baixa o arquivo como TXT.
* ASSETS-34096: exibição da interface do usuário para toque de correção para relatório de download assíncrono.
* ASSETS-34493: falha ao carregar a caixa de diálogo de download após ativar a alternância do recurso multiempresa.
* ASSETS-34824: Copiar url mostra vazio para pastas desabilitadas do DM.
* ASSETS-35226: fluxo de trabalho de pós-processamento não resolvido se especificado na raiz do DAM.
* ASSETS-35559: reduza o log de falha de upload em lote do DM para AVISO.
* ASSETS-35860: conversão de fuso horário incorreta na exibição em coluna do AEM Assets.
* ASSETS-35935: navegação de pasta incorreta após o fechamento da revisão da carga.
* ASSETS-35961: o botão Adicionar recorte não funciona no perfil de imagem.
* ASSETS-36227: Desative o serviço FolderPreviewUpdaterImpl na publicação.
* ASSETS-36943: falham colunas alinhadas quando o CF e outros itens não CF estão presentes em uma pasta na exibição de lista.
* ASSETS-36990: trabalhos de metadados exportados falham/ficam lentos com um grande número de propriedades.
* ASSETS-37113: o processo Reprocessar Ativos é encerrado imediatamente se a consulta retornar somente os resultados do CF.
* ASSETS-37260: a exportação de metadados no AEM pode produzir CSV inválido.
* ASSETS-37261: problema de anotação de PPTx e PDF no AEM Assets.
* ASSETS-37282: solicitação lenta potencial para abrir uma pasta grande.
* ASSETS-37330: a importação em massa do OneDrive cria uma estrutura de pasta AEM incorreta.
* ASSETS-37609: remover a pesquisa de configuração scene7 herdada.
* ASSETS-38016: algumas atualizações de metadados não são rastreadas corretamente em eventos.
* CQ-4357161: a tela AEM Inbox Payload está retornando 404.
* GRANITE-50041: a opção Adicionar representação não funciona quando a resolução tem mais de 1440 px de largura e apenas a opção &quot;Adicionar representação&quot; está na opção suspensa.
* GRANITE-50279: Nomes de semana desordenados no componente Datepicker Coral.
* SCRNS-3949: o tempo de solicitação de busca de canal do Screens é muito longo.
* SCRNS-3981: [Canal de sequência] A tela preta resultou quando a sequência de eventos de carregamento/descarregamento de elemento é distorcida.
* SCRNS-4180: [Canal de sequência] A sequência para com uma tela em branco para canais com vídeos de duração -1 após a recuperação da miniatura de fallback.
* SCRNS-4245: [Canal de sequência] Duração limitada da tela em branco quando um vídeo é carregado e alternado da miniatura de fallback.
* SITES-16055: corrija os links da Live Copy e da Origem da Live Copy nas respectivas páginas de propriedades.
* SCRNS-4243: botões ausentes no Provedor de conteúdo para usuários não administradores.

### Problemas conhecidos {#known-issues-16145}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-16145}

* [Descontinuação de credenciais JWT no console do Adobe Developer](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* A partir de 1 de maio de 2024, o Adobe Dynamic Media encerrará o suporte para o seguinte:

   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 e 1.1
   * As seguintes cifras fracas no TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


Para saber o que está obsoleto ou foi removido no AEM as a Cloud Service, consulte [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Tecnologias integradas {#embedded-tech-16145}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API DO SLING DO AEM | 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.24.6 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
