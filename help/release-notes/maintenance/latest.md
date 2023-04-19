---
title: Notas de versão de manutenção atuais de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão de manutenção atuais de [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 4aa4954f214545dcd768fdf955f1fc2f776da939
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 34%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas da versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 11835 {#release-11835}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 11835, lançada publicamente em 19 de abril de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: 11382.

A ativação de recursos desta versão de manutenção fornecerá o conjunto completo de recursos. Consulte as [notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter detalhes completos.

### Problemas corrigidos {#fixed-issues-11835}

- SITES-12573 - As consultas do GraphQL que usam variáveis dentro de um filtro falharão se uma variável não for especificada. Por favor, não atualize para esta versão caso use o GraphQL com AEM as a Cloud Service.
- SKYOPS-51970 - Regressão identificada da versão FACT usada na etapa buildImage, levando ao mapeamento de usuário não correspondente.
- GRANITE-44542 - Problemas relatados para clientes que não especificaram um tipo de nó de pacote (fornecendo um .content.xml com jcr:primaryType) para pastas incluídas no filtro de pacote. Isso fazia com que essas pastas fossem tratadas como nt:folder, criando problemas em vários casos.
- SKYOPS-56928 - A regressão HTTPD do Apache pode causar erros 404. Se você tiver esses problemas, por motivos de segurança, é recomendável reverter para a versão anterior e evitar que qualquer pipeline seja executado durante esse período.

### Tecnologias integradas {#embedded-tech-11835}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API do Sling do AEM | Versão 2.27.0 | [API do Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.21.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
