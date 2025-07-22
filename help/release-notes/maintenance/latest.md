---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 13124956fcce105ad42767f67b700284c8250012
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 17%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 21644 {#21644}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 21644, lançada publicamente em quarta-feira, 22 de julho de 2025. A versão de manutenção anterior era 21570.

A ativação de recursos do 2025.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-21644}

* ASSETS-39377: melhore a manipulação de 429s do armazenamento remoto no Assets Bulk Importer.
* ASSETS-46026: profundidade máxima configurável para exportador de metadados.
* ASSETS-49172: os ativos do modelo de Dynamic Media devem herdar os metadados da pasta.
* ASSETS-50209: suporte para substring em modelos DM.
* ASSETS-52326: página de configuração do AEM Assets para definir as preferências de exibição do Título do Assets.
* ASSETS-52805: adicionar suporte à saída/download de CSV para trabalho de Operação em massa.
* ASSETS-52873: adicione uma nova configuração nas propriedades da pasta para desativar o processamento de IA para essa pasta.
* ASSETS-53535: desempenho aprimorado do upload de vídeo do YouTube.
* ASSETS-53612: Controle para pesquisa híbrida no Assets Omnisearch.
* GRANITE-60183: atualizar a dependência commons-fileupload para 1.6.0.
* GRANITE-60287: atualização do QS para Jackrabbit 2.22.1.
* SITES-30452: API de conteúdo com ASO - Sugestões de título e descrição.
* SITES-31677: o espaço de trabalho personalizado oferece suporte à exportação do fragmento de conteúdo do AEM para o Target.
* SKYOPS-112741: Remova o pacote `com.adobe.granite.product.support` do AEM-CS SDK.

### Problemas corrigidos {#fixed-issues-21644}

* ASSETS-12882: problemas de alinhamento da interface do usuário após abrir predefinições do visualizador.
* ASSETS-48958: problema com a sincronização de ativos alterando o status publicado no AEM local do Sites.
* ASSETS-50856: `dam:processingAttempts` não sendo redefinido em completeUpload.
* ASSETS-51604: Falta dados &quot;Compartilhados com&quot; no CSV de relatório de compartilhamento de links.
* ASSETS-51783: Fallback para a configuração DM em `/conf/global` se nenhuma configuração for encontrada usando a consulta de pesquisa.
* ASSETS-51857: itens da tabela de ativos não reorganizáveis.
* ASSETS-52169: Nova representação de máquina do BAT incluída incorretamente nos downloads de ativos.
* ASSETS-52229: notificações da caixa de entrada ausentes para relatórios de ativos no AEM as a Cloud Service.
* ASSETS-52399: O aumento de versão em com.day.cq.dam.api pode quebrar o código do cliente.
* ASSETS-52780: o ativo pode ser marcado para visualização mesmo sem a opção de alternância ativada.
* ASSETS-52866: os vídeos DM migrados permanecem no estado de processamento na pasta com a Sincronização DM desativada.
* ASSETS-53237: lista suspensa Perfil de cor em branco no editor de predefinição de imagem.
* ASSETS-53240: Relatório de ativos - Falha no uso do disco ao obter o tamanho de representação do ativo do Dynamic Media.
* ASSETS-53446: falhas intermitentes de atualização do token de autenticação do YouTube devido ao NPE.
* ASSETS-53827: Blocos de validação de ACL que salvam conjuntos de mídias mistas.
* ASSETS-5403: Dynamicmedia clientlibs usadas na instância de publicação devem ter `allowProxy=true`.
* ASSETS-54261: A importação de metadados vaza conexões e se torna bloqueada se o arquivo não for baixado.
* CQ-4359863: a pesquisa de tags foi interrompida para palavras-chave fora de ordem no Editor de fragmento de conteúdo/Editor de ativos.
* CQ-4359958: Torne o openapi-support compatível com o AEM 6.5.22.0 e superior.
* CQ-4360256: inclua o caminho de contexto do servlet no caminho da solicitação para solicitações HTTP tratadas por meio do contexto do servlet `/adobe`.
* CQ-4360317: adicione o método para definir o cabeçalho de data de desativação ao criar respostas.
* GRANITE-60311: AEM SDK Quickstart - NPE em &quot;OSGi Installer Configuration Printer&quot; (Impressora de configuração do instalador OSGi).
* GS-15285: os usuários são exibidos como desativados.

### Problemas conhecidos {#known-issues-21644}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-21644}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-21644}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda quatro vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-21644}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
