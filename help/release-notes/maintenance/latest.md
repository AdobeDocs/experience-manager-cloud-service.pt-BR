---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 67b9a5f73f1f8c599e902a0ac0d8efbc614c7f75
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 17%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão X {#X}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção X, que foi lançada publicamente em 1 de abril de 2025. A versão de manutenção anterior foi lançada em 19823.

A ativação de recursos do 2025.4.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-X}

FORMS-19068: adição de suporte para ações de envio do AEP Connector nas APIs do Forms Manager para aprimorar os recursos de integração de dados de formulário.

FORMS-18513: Implementação do suporte à transformação da árvore de dados no AEP Connector para aprimorar a funcionalidade do assistente e os recursos de manipulação de dados.

FORMS-18432: Implementação da configuração de preenchimento prévio do lado do cliente específico do formulário (baseado em regex) para ativar a funcionalidade de preenchimento prévio seletivo sem alterações no nível de OSGI.

FORMS-17551: adição do suporte ao Documento de registro (DoR) para integrações de lista do SharePoint.

### Problemas corrigidos {#fixed-issues-X}

FORMS-19028: a funcionalidade de preenchimento prévio do lado do cliente interrompe o manuseio de eventos de formulário, impedindo que a confirmação de valor e os eventos DOMContentLoaded sejam acionados corretamente no carregamento do formulário.

FORMS-18360: Gerenciamento aprimorado do escopo de lista do SharePoint para sites de equipes no Gerenciamento de documentos do Forms para melhorar a organização de dados e o controle de acesso.

FORMS-18325: adição da configuração da nuvem do Adobe Experience Platform (AEP) para aprimorar a integração de dados de formulário e os recursos de processamento.

FORMS-18213: Implementação da funcionalidade para ocultar/excluir campos desativados do Documento de registro (DoR) para melhorar a clareza do documento e a experiência do usuário.

FORMS-18189: manipulação de função personalizada modificada para impedir o registro de erros em bibliotecas de clientes vazias e melhorar a exibição de erros na interface do usuário.

FORMS-18426: a funcionalidade de pesquisa de lista do SharePoint falha quando os nomes de lista contêm caracteres especiais (por exemplo, &#39;-&#39;), afetando a integração de formulários com listas do SharePoint.

FORMS-18375: formulários baseados em Componentes do Foundation selecionam incorretamente configurações recaptcha da pasta `conf/global` quando nenhum contêiner de configuração específico é selecionado.

FORMS-18304: os documentos do PDF/A-1b que passam na validação no Acrobat e no LiveCycle ES4 são sinalizados incorretamente como não compatíveis no AEM 6.5 Forms devido a erros de cor dependentes do dispositivo.

FORMS-18271: o Editor de temas do Forms exibe mensagens de erro não localizadas, afetando a experiência do usuário na configuração do formulário e na personalização do tema.

FORMS-18068: problemas de renderização de texto em negrito no Documento de registro (DoR) para grupos de botões de opção e caixas de seleção usando campos de rich text.

FORMS-7016: a ordem de foco do teclado no Editor de formulários não segue a navegação lógica.

FORMS-6950: adição de funções e atributos ARIA necessários aos componentes de visualização em árvore do navegador do sistema de arquivos para melhorar a acessibilidade do leitor de tela e estar em conformidade com o padrão WCAG 4.1.2 Name, Role, Value (Level A).

### Problemas conhecidos {#known-issues-X}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-X}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-X}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda X vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-X}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.76.0 | [API Oak API 1.76.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.26-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
