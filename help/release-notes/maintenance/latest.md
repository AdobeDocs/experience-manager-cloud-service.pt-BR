---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 24%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 20476 {#20476}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 20476, lançada publicamente em quarta-feira, 15 de abril de 2025. A versão de manutenção anterior foi lançada em 2013.

A ativação de recursos do 2025.4.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-20476}

* CNTBF-411: adicione a possibilidade de excluir o trabalho do sling caso ele seja descartado pelo JCR.
* CQ-4359813: AEM Translation Kit: 20 de março.
* CQ-4359811: Kit de tradução do Granite: 20 de março.
* GRANITE-57863: atualização do Filevault para a versão 3.8.4.
* GRANITE-56154: configure tentativas exponenciais em oak-segment-azure.
* GRANITE-55999: Melhore o desempenho do UserPropertiesService.
* GRANITE-55781: Evite a reconfiguração redundante de associação de usuário.
* GRANITE-53956: atualize o Azure SDK V8 para V12 para oak-segment-azure.
* GRANITE-50654: na guia de permissões principais, remova a carga &quot;todos&quot; por padrão no front-end.
* SKYOPS-103444: Atualização para Sling ResourceResolver 1.12.6.
* SKYOPS-101147: Atualizar caconfig impl.
* SKYOPS-97124: Adicione avisos do analisador para versões desatualizadas do pacote SPIFly.
* SKYOPS-95826: Atualize as versões de tempo de execução do Java para 11.0.26 e 21.0.6.
* SKYOPS-53671: Use artefatos instalados pelo cliente a partir de modelos de recursos no (RDE) AEM reinicia.

### Problemas corrigidos {#fixed-issues-20476}

* ASSETS-49027: [Regressão] O AemRequestEventFilter interrompe as solicitações POST para o console da Web OSGI.
* ASSETS-44956: Não é possível selecionar nenhuma representação do Dynamic Media - as tags de script devem ser carregadas no componente de nível superior.
* CNTBF-410: ponteiro nulo CheckJob getId no Pacote ContentCopy.
* CNTBF-341: Índice de exportação de ContentCopy fora dos limites.
* CQ-4355411: as dicas de ferramentas permanecem na tela na caixa de diálogo &quot;Preferências do usuário&quot;.
* GRANITE-57265: os valores de seleção suspensos não estão sendo selecionados.
* GRANITE-57067 - Faltam políticas eficazes na interface.
* SITES-30727: arrastar e soltar pode falhar para subcomponentes dentro do editor do AEM.
* SKYOPS-90607: Os trabalhos do Sling são executados em implantação inativa/conteúdo mutável.
* SKYOPS-95722: Remova o tamanho `MaxPermSize` dos sinalizadores de início rápido no AEM-SDK.
* SKYOPS-103569: Determinadas imagens não podem ser carregadas com o Java 21: `javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`.

### Problemas conhecidos {#known-issues-20476}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-20476}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-20476}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda cinco vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-20476}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.78.0 | [API Oak API 1.78.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.26-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.28.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
