---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 859af15f4038b28e6e1398e5168dc008d22985e9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 19%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

>[!NOTE]
>
> As versões de 20936 e 20783 foram tornadas privadas.

## Versão 20626 {#20626}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 20626, lançada publicamente em quarta-feira, 29 de abril de 2025. A versão de manutenção anterior era 20476.

A ativação de recursos do 2025.5.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-20626}

* ASSETS-46413, ASSETS-46580: adição de um novo status de revisão &quot;Pré-visualização&quot;.
* ASSETS-49542: expansão de idiomas compatíveis para transcrição e tradução de vídeo e áudio.
* ASSETS-48264: Expansão do suporte à qualidade de PNG para execuções.

### Problemas corrigidos {#fixed-issues-20626}

* ASSETS-50387: Miniatura padrão do fragmento de conteúdo correto para uso no GenStudio.
* ASSETS-49006: exibe propriedades de vídeo quando o usuário não tem permissões de gravação.
* ASSETS-46757, ASSETS-46997: melhore a acessibilidade no editor de recorte inteligente.
* ASSETS-48018: Melhore o rastreamento de referência de ativos no Relatório de publicação do Assets.
* ASSETS-35846: melhore a consistência do acesso entre o autor e o nível de entrega.
* ASSETS-48171: melhore a consistência da modelagem do Dynamic Media com o Canvas.
* ASSETS-49813: Melhore a notificação de expiração.
* ASSETS-47768, ASSETS-49825, ASSETS-49008, ASSETS-48287: Melhore o gerenciamento e a visibilidade de operações em massa.
* ASSETS-50003, ASSETS-50004: melhore a nomenclatura e o controle sobre as representações incluídas em um download de ativo.
* ASSETS-47939: melhore a organização das respostas para o Content Hub.
* ASSETS-46738: melhore o desempenho de coleções muito grandes.
* ASSETS-50121: Melhore a confiabilidade dos eventos publicados de ativos.
* ASSETS-48490: melhore a resiliência do processamento automatizado durante a assimilação de imagens.
* ASSETS-28106, ASSETS-49404: melhore a robustez da pesquisa de texto completo.
* ASSETS-50006, ASSETS-50423: Melhore o desempenho de pesquisa e percurso em uma pasta grande.
* ASSETS-46021: Melhore a exibição de vídeo para navegadores Safari e móveis.
* ASSETS-49002: Melhore a manipulação da edição de modelos do Dynamic Media.
* ASSETS-48376: vários aprimoramentos na interface do usuário do Content Hub.
* ASSETS-48504, ASSETS-49378: Várias melhorias no comportamento da interface.
* ASSETS-49540: retirar a OpenAPI das relações de ativos da fase experimental.
* ASSETS-40284: atualize a documentação sobre a integração do Adobe Stock.
* ASSETS-49739: Trabalhe para integrar o Figma a partir do Seletor de ativos.

#### Guias do AEM {#guides}

* GUIDES-21734: Novas IDs não são geradas para elementos quando esses elementos são adicionados por trechos ou criados por modelos, mesmo quando a opção de geração automática de ID está habilitada no XMLEditorConfig.
* GUIDES-25969: Se o atributo `scope=external` estiver ausente em links externos em um tópico DITA, a publicação do HTML5 falhará sem indicar os arquivos em que esse atributo está ausente nos logs de erro, especialmente quando o microsserviço está habilitado.
* GUIDES-27288: Não é possível transmitir as propriedades de metadados para mapear páginas de aterrissagem geradas usando a nova publicação do AEM Sites.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-20626}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-20626}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-20626}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 11 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-20626}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.78.0 | [API Oak API 1.78.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.26-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
