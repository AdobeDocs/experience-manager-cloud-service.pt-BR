---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82be9b2b328343e827b90bd8266d93127757f477
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 16%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 17569 {#release-17569}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 17569, lançada publicamente em quarta-feira, 27 de agosto de 2024. A versão de manutenção anterior era a versão 17465.

A ativação de recursos do 2024.9.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-17569}

* CQ-4353778: Eventos do processo de tradução.
* CQ-4354583: envia eventos do processo de tradução por meio do pipeline de Adobe.
* CQ-4356479: permite somente o código Adobe para usar o contexto de servlet /adobe.
* CQ-4358133: otimizar o uso do trabalhador Jenkins.
* CQ-4358226: a funcionalidade de palavra-chave Save Translation não funciona para um formato de string específico.
* CQ-4358270: Kit de tradução AEM: agosto de 2008.
* CQ-4358310: adicione oak-compat-query-spi-1.2 para iniciar rapidamente.
* GRANITE-36205: atualização automatizada para lançamento interno de oak no QS.
* GRANITE-49833: Suporte em lote para remetente e proxy de eventos.
* GRANITE-52053: Remova os usos de Commons Collections 3: Platform others.
* GRANITE-52492: catchup assíncrono elástico no caso de restauração de PIT.
* GRANITE-53086: atualize a versão do plug-in jacoco para 0.8.12 no AEMaaCS.
* GRANITE-53099: Atualização para Apache Felix Http Jetty 5.1.24.
* GRANITE-53125: adicionar classificação ao CloudEvent.
* GRANITE-53328: atualização do Filevault para 3.8.0-T20240726111512-3cc11d50 contendo melhorias de registro de armazenamento.
* GRANITE-53340: AEM660: Versionamento e ramificação adequados para 660 CQ/Platform.
* GRANITE-53341: Não avise sobre o uso do ACS Commons 6.
* GRANITE-53453: atualização do commons-lang para 3.15.0.
* GRANITE-53473: Reinicie as configurações do Sling.
* GRANITE-53478: atualize o Filevault para a versão 3.8.0.
* GRANITE-53505: atualize o QS para commons-collections-3.2.2-adobe-2.
* GRANITE-53528: atualização da versão dos artefatos da plataforma.
* GRANITE-53547: Fornece API alternativa evitando o uso do Apache Commons Lang 2.
* GRANITE-53575: Use o BSAFE 6.2.5 no CS.
* GRANITE-53608: atualize o Oak para a versão pública mais recente (1.68.0).
* SITES-23583: Os testes do Sites Evergreen falham no Java 17.
* SKYOPS-79535: Atualização para o script rum v2.
* SKYOPS-79816: Ativar a Tarefa do Analisador de Recursos do Sling para Mapeamentos de Usuário de Serviço na Ferramenta FACT.
* SKYOPS-81179: AEM cria testes para alternância de pacotes.
* SKYOPS-81866: Relate avisos para pacotes conhecidos por serem incompatíveis com o Java 21.
* SKYOPS-82660: Atualização da API Sling para 2.27.6.
* SKYOPS-82961: Atualização para Sling ResourceResolver 1.12.0-T20240723153354-a0270a0.
* SKYOPS-83356: Crie um painel global para rastrear versões de JVM usadas em implantações de AEM.
* SKYOPS-83436: A implantação do Java Runtime 21 interrompe a criação de formulários adaptáveis do AEM Forms.
* SKYOPS-84272: Registre a versão do java usada na inicialização do inicializador do aem.

### Problemas corrigidos {#fixed-issues-17569}

* CMGR-60225: falha na execução do pipeline identificada no cliente do AEM Sites CS ao validar a atualização para o AEM versão 17486.
* GRANITE-45919: países embargados na lista de Países/Regiões em Editar configurações do usuário.
* GRANITE-51715: Às vezes, o seletor não insere a seleção no campo de texto.
* GRANITE-53290: Verifique corretamente o protocolo ao analisar o URL na verificação XSS.
* GRANITE-53576: definição incorreta de classificação de serviço em configurações OSGi.
* SKYOPS-82129: Vazamento de memória em Modelos Sling.

### Problemas conhecidos {#known-issues-17569}

Nenhum.

### Aviso de mudança {#change-notice-17569}

* A partir de setembro de 2024, a AEM as a Cloud Service desativará a serialização de Resource Resolvers por meio da estrutura do Exportador de modelo do Sling. Consulte [a documentação](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obter mais detalhes.

### Recursos e APIs obsoletos {#deprecated-17569}

Observe que estamos no processo de atualização do `com.day.cq.wcm.api` e, com a versão atual, marcamos como `@Deprecated` alguns de seus métodos e classes. Eles serão removidos em versões futuras. Portanto, considere mudar para as alternativas sugeridas se estiver usando alguma delas.

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-17569}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda quatro vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-17569}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak API 1.68.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.26.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
