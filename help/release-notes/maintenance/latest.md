---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5d00bed4008c70e81f3a70d219ddc411ec8bdc59
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 29%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 21484 {#21484}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 21484, lançada publicamente em sexta-feira, 10 de julho de 2025. A versão de manutenção anterior era 21331.

A ativação de recursos do 2025.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-21484}

Nenhum.

### Problemas corrigidos {#fixed-issues-21484}

Nenhum.

#### Guias do AEM {#guides-21484}

* GUIDES-29781: Quando um comentário XML é adicionado a um elemento na exibição do Source, os espaços à esquerda e à direita em torno do comentário são perdidos ao alternar exibições.
* GUIDES-29078: ao abrir um tópico na exibição Autor após a atualização de um navegador, as tags aplicadas anteriormente no painel Propriedades do arquivo não são mantidas e a adição de novas tags substitui as existentes, principalmente quando um grande número de tags está disponível para seleção.
* GUIDES-28214: As tentativas de criar tarefas de revisão por meio do fluxo de trabalho do AEM falham consistentemente porque o nó de revisão não é criado.
* GUIDES-28104: A publicação de um mapa DITA com o atributo `chunk=to-content` cria nós JCR duplicados na nova saída do AEM Sites, resultando na estrutura de conteúdo redundante no AEM Sites.
* GUIDES-29065, GUIDES-28793: problemas de desempenho, como tempos de carregamento mais longos e tempos limite intermitentes, são observados ao trabalhar com coleções grandes.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-21484}

* O SDK disponibilizado no Portal de distribuição de software tem problemas executados localmente. Continue usando o SDK anterior para testes locais.

### Recursos e APIs obsoletos {#deprecated-21484}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-21484}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda cinco vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-21484}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
