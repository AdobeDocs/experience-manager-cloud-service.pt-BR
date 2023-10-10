---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3fbdb150a9a1c133b4910603682e37f1c5d885d2
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 35%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 13804 {#release-13804}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 13804, que foi lançada publicamente em 10 de outubro de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: versão 13665.

A Ativação de recursos 2023.10.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-13804}

* GRANITE-47238: Manutenção do registro de auditoria - Limpe os cronjobs para usar a configuração do cliente.
* GRANITE-47123: Publicar (Sling) - Melhore o tempo de inicialização inicializando o cache de caminho personalizado de forma assíncrona por padrão.
* GRANITE-46618: Publicar (Replicação) - Melhore a velocidade de inicialização da publicação por meio do agrupamento de mensagens de status de replicação.
* GRANITE-47136: Indexação (Download) - Melhore a velocidade de download do novo downloader de índice paralelo (desabilitando a validação da soma de verificação).
* GRANITE-47211: Publicação (Infra) - Melhore a dissociação de implantações do nível de publicação (armazenando e buscando o nome de revisão do armazenamento de segmentos).
* GRANITE-47267: atualização para Apache Felix Http Jetty 4.2.18 (inclui a correção de erros para o tratamento do parâmetro de solicitação ([FELIX-6625](https://issues.apache.org/jira/browse/FELIX-6625)com melhorias de desempenho para os desenvolvimentos locais e RDE).
* GRANITE-47247: atualização para o Sling Servlets Resolver 2.9.14 com melhorias de desempenho na resolução do servlet.

### Problemas corrigidos {#fixed-issues-13804}

* GRANITE-47376: Autor (Infra) - Correção de erros DiscoveryTopologyUndefined após a reinicialização do roll.
* CQ-4353436: Console da Web AEM (Sling) - Configurações vazias em ServiceUserMapperImpl Validators (Principal/Usuário) interrompe a instância do AEM ([SLING-11912](https://issues.apache.org/jira/browse/SLING-11912)).
* SKYOPS-63925: Tarefa de Transformação - Evitar falhas de TransformJob com JDK 11 - ZipException: Erros de cabeçalho CEN inválidos (com sinalizador JVM disableZip64ExtraFieldValidation).
* SKYOPS-63361: Trabalho de Transformação (Log) Registro aprimorado com Trabalhos de Transformação (subetapa CUSTOMER_EXTRACT).
* SKYOPS-64103: Ferramenta FACT (Log) - Reduza ou trunque mensagens de erro e aviso da biblioteca Clientlib.
* SKYOPS-65109: Ferramenta FACT (Tratamento de Erros) - Pacotes de Conteúdo com dependências não resolvidas resultam em um erro relatado corretamente.
* SKYOPS-65368: Ferramenta FACT (Tratamento de erros) - A ferramenta é executada em ciclos de inclusão infinitos e, por fim, atinge o tempo limite em incorporações circulares de Clientlibs.
* SKYOPS-64031: RDE - ComponentCacheImpl pode entrar em estado inconsistente devido ao registro ResourceResolverFactory duplicado ([SLING-12019](https://issues.apache.org/jira/browse/SLING-12019)).
* ATIVOS-29105: RDE - Provedor de restrição ausente de SecurityProviderRegistration requiredServicePids no modelo de recursos RDE.
* GRANITE-44674: CoralUI - A funcionalidade de campo obrigatório do Datepicker está incorreta.

### Problemas conhecidos {#known-issues-13804}

Nenhum.

### Tecnologias integradas {#embedded-tech-13804}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [API Oak API 1.56.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| API DO SLING DO AEM | Versão 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.4 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
