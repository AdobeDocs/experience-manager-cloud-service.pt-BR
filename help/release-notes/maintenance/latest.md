---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 16%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 18751 {#18751}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 18751, lançada publicamente em quinta-feira, 11 de dezembro de 2024. A versão de manutenção anterior foi a versão 18598.

A ativação de recursos do 2025.1.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-18751}

* SKYOPS-88509: Suporte a Java 21 para o SDK do AEM.

### Problemas corrigidos {#fixed-issues-18751}

* ASSETS-42802: O botão Voltar no MFE nem sempre funciona e mostra uma caixa de diálogo extra.
* ASSETS-44148: evento NODE_MOVED corrigido no AEM pode causar NPE.
* ASSETS-44418: a correção de ambiente correta não está configurada no skyline.
* ASSETS-44821: correção do filtro de eventos Update para incluir dados codificados em url de formulário para eventos de upload.
* CNTBF-298: a cópia de conteúdo fixo falha com conflitos UUID.
* CNTBF-331: [content-copy-bundle] versão 2.0.14.
* FORMS-16572: Remover falhas de teste de fluxo de trabalho para a build do SDK do java 21.
* GRANITE-36205: atualização automatizada para lançamento interno de oak no QS.
* GRANITE-53704: reavalie a descoberta do Sling no serviço do repositório.
* GRANITE-54300: atualize o Oak para a versão pública mais recente (1.70.0).
* GRANITE-54416: atualize o Filevault para a versão 3.8.2.
* GRANITE-54462: Configure o SubscriberAgents para usar hc.tags de &quot;systemready&quot;.
* GRANITE-54542: atualize a dependência do commons-io para 2.17.0.
* GRANITE-54658: adicione o delayFactor e as configurações OSGi de tamanho de lote para fullGC no QS.
* GRANITE-54696: Amplie o intervalo de importação para a API Jackrabbit.
* GRANITE-54803: Desative o ClusterAtExchange no AEM quando o imsauth estiver ativo.
* GRANITE-55095: atualize o Oak para a versão pública mais recente (1.72.0).
* GUIDES-20006: O estado do documento marcado como Concluído reverte para Rascunho antes de salvar uma nova versão, fazendo com que o estado Concluído não persista em nenhuma versão do documento.
* GUIDES-21840: Na saída do PDF nativo, os títulos de capítulo estão ausentes do índice, levando a uma hierarquia incorreta.
* GUIDES-19558: Editar e salvar uma linha de base em uma configuração de nuvem atinge o tempo limite após 1 minuto se a linha de base tiver um grande número de tópicos ou mapas.
* GUIDES-19733: A tradução de mapas usando a linha de base fica lenta e eventualmente não carrega a lista de todos os tópicos e arquivos de mapas associados.
* SITES-26798: Ativar promoção automática não está atualizando o Status da promoção (Data da promoção).
* SITES-27137: remove a dependência de métricas do Sling commons do núcleo do MSM.
* SKYOPS-75446: Correção de AEM às vezes retorna um 404 ou páginas com conteúdo ausente.
* SKYOPS-76366: Nenhuma métrica do Jetty Threadpool no AEM versão 15977 e posterior.
* SKYOPS-82371: java.io.IOException: classFile.delete() falhou.
* SKYOPS-83369: as implantações de AEM falharão ao serem inicializadas se a execução do trabalho de transformação não gerar pacotes.
* SKYOPS-83910: Correção de problemas de simultaneidade encontrados no SKYOPS-82371.
* SKYOPS-84821: Defina a configuração sling.includes.checkcontenttype do Sling Main Servlet como true.
* SKYOPS-85798: O trabalho de Transformação Fixa gera definições de índice vazias.
* SKYOPS-86251: Atualize para o AEM Analyzer core 1.5.6 e ative o analisador de importação de pacote de produtos no trabalho de transformação.
* SKYOPS-86710: Remover falhas de teste de Minify para build do sdk do java 21.
* SKYOPS-86745: Atualização para Sling ResourceResolver 1.12.2.
* SKYOPS-89616: Não foi possível criar uma conta técnica no Adobe Developer Console corrigida.
* SKYOPS-89691: Correção da ID de artefato incorreta usada para avisos do ASM.
* SKYOPS-89699: Avisos ausentes para versões antigas do Groovy incorporadas ao tipo &quot;orbinson&quot; do console Groovy.
* SKYOPS-88664: Registre e proteja contra um caso quando o arquivo de mapa baixado tiver uma linha acima do limite 1024.
* SKYOPS-89734: Liberação da imagem do dispatcher 2.0.235.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos no Experience Manager Guides, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conhecidos {#known-issues-18751}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-18751}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-18751}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda três vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-18751}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak API 1.72.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
