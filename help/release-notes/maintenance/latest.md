---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6fa6fc9015624bec9113a198285531a3bdd7e29c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 18175 {#release-18175}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 18175, lançada publicamente em sexta-feira, 10 de outubro de 2024. A versão de manutenção anterior foi a de 17964. A versão 18099 foi tornada privada devido a um problema.

A ativação de recursos 2024.10.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-18175}

* ASSETS-38322: Ativando o evento de solicitação http para AEM.
* ASSETS-41448: atualize o pacote auth.ims para suportar FI para agrupar mapeamentos.
* ASSETS-41684: adicione configurações OSGI OOB para definir FI para agrupar o mapeamento para Assets, Foundation, Sites e Forms.
* ASSETS-43015: atualização para o pacote auth.ims mais recente.
* CQ-4356633: adicione caractere extra na dica de ferramenta &quot;Somente conteúdo&quot;.
* GRANITE-50948: Integrar o serviço de repositório ao Suporte AEM para serviço de repositório.
* GRANITE-52454: Adicionando o auxiliar de suporte 0.1.2.
* GRANITE-52454: Atualizando o auxiliar de suporte GRANITE-52454 atualizando o auxiliar de suporte para usar a versão mais recente do AEMaaCS.
* GRANITE-53287: atualizando a versão de teste da integração de privilégios de segurança.
* GRANITE-53485: Autenticação da Entidade de Serviço de Suporte para replicação do Armazenamento Azure Blob.
* GRANITE-53514: Treeativation atualizado para a versão 1.0.26.
* GRANITE-53870: crie um mecanismo interno para ignorar a verificação máxima de versão JVM para o início rápido.
* GRANITE-53914: Corrija falhas no teste da Platform com a versão atualizada do módulo Java 17.
* GRANITE-53966: use um pool de threads separado para distribuição de conteúdo.
* GRANITE-54006: atualização de Jackson para 2.17.2.
* GRANITE-54038: Adicione o cliente IMS Creative Cloud Enterprise ao incluo na lista de permissões do cliente IMS AEM.
* GRANITE-54054: Variável de ambiente para com.adobe.granite.repository.impl.SystemUserValidation warnOnly.
* GRANITE-54266: Falta o serviço Search Suggestor no SDK de produção.
* GRANITE-54274: Aceitar o cliente IMS Firefly.
* GRANITE-54300: atualize o Oak para a versão pública mais recente (1.70.0).
* GUIDES-19069: Adicionar guias PeerLinkIndex para o complemento guias do aem.
* SITES-23584: correção de falha no teste do componente Foundation no Java 17.
* SKYOPS-69768: SlingModels não desserializa ResourceResolvers.
* SKYOPS-76378: Melhore a segurança de thread do registro/cancelamento de ResourceBundle no i18n.
* SKYOPS-79285: Atualização do Sling XSS para 2.4.2.
* SKYOPS-82383: Exponha o resultado &quot;helm-values&quot; convert-merge-analyze no descritor de execução do comando.
* SKYOPS-84810: ignore a execução &quot;40-initialize-publish.sh&quot; na inicialização do RDE.
* SKYOPS-84951: Corrigir código de geração de soma de verificação de conteúdo mutável.
* SKYOPS-85335: Atualização de org.apache.sling.jcr.repoinit para 1.1.52.
* SKYOPS-85336: Atualização do Sling Commons Threads para 3.3.0.
* SKYOPS-86329: atualização de versões dos módulos de teste da plataforma para suporte ao sdk do java 21.

### Problemas corrigidos {#fixed-issues-18175}

* CNTBF-298: remova jcr:uuid de pacotes exportados CC.
* SKYOPS-83910: correção de problemas de simultaneidade encontrados no SKYOPS-82371.
* GRANITE-52876: atualização para com.adobe.granite.ui.content 0.8.1448.
* GUIDES-14445: Falha na geração de PDF nativo com um erro relacionado à obtenção de dependências para Node.js.
* GUIDES-16961: O título com `<conref>` não é resolvido nos painéis Linha de Base e Tradução do Editor da Web.
* GUIDES-17283: Ao selecionar a opção **Usar metadados adicionados ao topicmeta**, as propriedades de metadados não são propagadas nas propriedades de documento da saída de PDF nativo.
* GUIDES-17793: O PDF referenciado não é ativado no **Painel do Publish em massa** durante a Ativação em massa do conteúdo publicado.

Para obter mais informações sobre os recursos novos e aprimorados do Guides e os problemas corrigidos nessa versão, consulte o [roteiro de versões do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-18175}

* FORMS-15818: A entrada do descritor de componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` não encontrou instruções nos logs do servidor. Estas são instruções de registro inofensivas.

### Recursos e APIs obsoletos {#deprecated-18175}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

Veja a seguir um resumo dos recursos que foram descontinuados recentemente ou daqueles em processo de descontinuação.

#### API de uso do JavaScript {#javascript-use-api}

[A API de uso do JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) está oficialmente obsoleta devido aos desafios que os usuários têm na depuração e manutenção do código que aproveita a API, bem como limitações de desempenho em comparação com a alternativa do Java.

Você deve fazer a transição para [a API de Uso do Java](https://experienceleague.adobe.com/en/docs/experience-manager-htl/content/java-use-api), que oferece melhor desempenho, depuração mais fácil e maior suporte a longo prazo.

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

Observe que o Adobe está no processo de atualização de `com.day.cq.wcm.api`. Alguns de seus métodos e classes foram marcados como `@Deprecated` na versão atual. Eles serão removidos em versões futuras. Considere alternar para as alternativas sugeridas.

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165: substitua org.apache.jackrabbit.oak.plugins.blob na API pública.

### Correções de segurança {#security-18175}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda duas vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-18175}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
