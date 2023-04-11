---
title: Notas de versão de manutenção atuais de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão de manutenção atuais de [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: ea71ca9fe259fbbf497a35930a10450bd4e26ce8
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 24%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas da versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 11382 {#release-11382}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 11382, lançada publicamente em 28 de março de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: 11289.

A ativação de recursos desta versão de manutenção fornecerá o conjunto completo de recursos. Consulte as [notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter detalhes completos.

### Problemas conhecidos {#known-issues-11382}

- SITES-12573 - As consultas do GraphQL que usam variáveis dentro de um filtro falharão se uma variável não for especificada. Por favor, não atualize para esta versão caso use o GraphQL com AEM as a Cloud Service.
- SKYOPS-51970 - Regressão identificada da versão FACT usada na etapa buildImage, levando ao mapeamento de usuário não correspondente.
- GRANITE-44542 - Problemas relatados para clientes que não especificaram um tipo de nó de pacote (fornecendo um .content.xml com jcr:primaryType) para pastas incluídas no filtro de pacote. Isso fazia com que essas pastas fossem tratadas como nt:folder, criando problemas em vários casos.

### Problemas corrigidos {#fixed-issues-11382}

- ASSETS-21023 - Correção da renderização do Smart Crop, em que os clientes podiam observar uma exceção de Null Pointer na instância do Publisher de todos os ambientes AEM quando tentavam acessar essas renderizações por meio da API.
- SKYOPS-49280 - Ao instalar uma configuração ou atualização de pacote usando RDE em Publicar, o resultado pode não ser observável porque o cache do Publicar dispatcher não é invalidado

#### Sites {#sites-issues-11382}

- SITES-7796 - Capacidade do autor de conteúdo publicar o Fragmento de conteúdo Principal e suas respectivas variações ao exportar para o target
- SITES-97 - GraphQL: Paginação e classificação, filtragem híbrida

>[!NOTE]
>
> No SITES-97, algumas melhorias foram feitas na implementação do GraphQL que podem causar comportamento inesperado. Consulte [AEM alterações do GraphQL em relação à manipulação de valores nulos](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html) para obter mais informações.

#### Assets {#assets-issues-11382}

- ASSETS-20076 - Adicionar suporte para marcas d&#39;água de vídeo que corresponda ao suporte atual para marcas d&#39;água de imagem
- ASSETS-21428 - Exclusões adicionadas para alterações de CSS

#### Forms {#forms-issues-11382}

- CQ-4351502 - Atualização do mapeamento de usuário do serviço para permitir acesso de leitura no Sites

#### Platform {#platform-issues-11382}

- SITES-11040 - Ativação condicional de armazenamento em cache de consultas persistentes do GraphQL no dispatcher

### Tecnologias integradas {#embedded-tech-11382}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API do Sling do AEM | Versão 2.27.0 | [API do Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.21.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
