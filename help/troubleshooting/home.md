---
title: Solução de problemas no AEM Assets e no Forms
description: Solucione problemas comuns do AEM Assets e do Forms usando os links de artigo para áreas principais, como uploads, metadados, pesquisa, delivery, criação de formulários, envio e integração.
hidefromtoc: true
hide: true
source-git-commit: 5074e777c68c51955b9ad8f055e04067163b9596
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 1%

---


# Solução de problemas do AEM Assets e do Forms {#troubleshoot-aem-assets-forms}

A AEM as a Cloud Service oferece soluções abrangentes para o Gerenciamento de ativos digitais por meio do AEM Assets e recursos avançados de criação de formulários por meio do AEM Forms. Ambos os serviços fornecem soluções PaaS nativas em nuvem com recursos inteligentes de última geração, como IA/ML, tudo em um sistema que está sempre atualizado, sempre disponível e aprendendo.

No entanto, os ambientes corporativos complexos podem enfrentar vários desafios técnicos em diferentes áreas.

Este abrangente guia de solução de problemas fornece abordagens de diagnóstico sistemáticas, soluções categorizadas e caminhos de resolução passo a passo para AEM Assets e Forms. Cada seção inclui guias de referência rápida, metodologias detalhadas de solução de problemas e links abrangentes de recursos para ajudar você a resolver problemas com eficiência e otimizar seu ambiente do AEM Cloud Service.

## Solução de problemas do AEM Assets {#aem-assets-troubleshooting}

O AEM Assets simplifica a forma como você gerencia, organiza e fornece ativos digitais em todas as experiências. No entanto, podem surgir problemas que afetem os uploads de ativos, metadados, integrações ou delivery. Este artigo fornece etapas de solução de problemas para ajudá-lo a diagnosticar e resolver problemas comuns do AEM Assets. Seguindo as orientações aqui, você pode restaurar workflows com eficiência e garantir que os ativos permaneçam acessíveis, precisos e prontos para uso em todos os canais.

### Processamento de ativos e representações {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Upload e processamento</strong></td>
    <td><strong>Representações</strong></td>
    <td><strong>PDF e Extração de texto</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26610">O processamento de ativos falhou para arquivos MP4 grandes no AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26639">Representações DAM não correspondem aos arquivos originais</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26785">O AEM trunca o texto extraído de PDFs grandes após 100 mil tokens</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-23916">O arquivo Tiff com uploads de compactação ZIP não gera representações</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26233">Imagens que não mostram representações em miniatura no AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25518">Limitações de extração de texto para PDFs grandes no AEM as a Cloud Service</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-21865">Falha ao arrastar e soltar uma pasta de ativos para a interface do usuário da Web do AEM Assets</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26528">Problema de rotação de ativos torna invisíveis as rotações subsequentes</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26450">Aumento do limite de upload de ativos de parte única para a integração da API do Firefly com o Photoshop</a></td>
  <td></td>
  <td></td>
  </tr>
  </tbody>
</table>

### Dynamic Media {#dynamic-media-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Vídeo</strong></td>
    <td><strong>Conjuntos de rotação e corte inteligente</strong></td>
    <td><strong>Entrega e configurações</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26533">Corrigir problemas de upload, processamento e renderização de vídeo no AEM</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26715">Conjuntos de rotação paralisados no estado de processamento</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-17628">Alteração do URL do Dynamic Media para ativos</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26677">Incompatibilidade de miniatura de vídeo entre o Dynamic Media e a exibição de placa DAM</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26873">Representações de Recorte inteligente não geradas no AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26367">Problema de imagem corrompida com o recorte inteligente no AEM 6.5</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26610">Falha no processamento de ativos no AEM Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26637">Problema de cor de fundo para representações do TIFF</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25294">A página Configurações gerais do Dynamic Media não abre</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26197">Resolva problemas de áudio em arquivos de vídeo com o Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25885">Falha na sincronização de ativos no Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26461">Resolver discrepâncias de nome de ativo entre ambientes</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26871">O reprodutor de vídeo Dynamic Media não funciona em ambientes inferiores</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25471">Recomendações do usuário de sincronização do Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26902">Exportar ativos e metadados do Dynamic Media usando a API</a></td>
  </tr>
  </tbody>
</table>

### Metadados, marcação e compartilhamento {#metadata-tagging-sharing-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Metadados</strong></td>
    <td><strong>Tags inteligentes</strong></td>
    <td><strong>Acesso e compartilhamento</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25828">Discrepância de metadados de imagem no AEM Assets</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25925">Marcação automática de ativos recém-carregados</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26928">Comentário restrito na Visualização do Assets apesar do acesso de leitura</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26655">Resolução de problemas de visibilidade de esquema de metadados para usuários não administradores</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25889">As Tags inteligentes não funcionam após a migração do JWT para o OAuth</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25903">Resolver problemas de link compartilhado no AEM Managed Services</a></td>
  </tr>

</tbody>
</table>

### Integrações e acesso {#integrations-access}

<table>
  <tbody>
    <tr>
      <td><strong>Asset Link</strong></td>
      <td><strong>Licenciamento e personalizações</strong></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26922">O Adobe Asset Link deixa os links inacessíveis no InDesign</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26616">Fragmentos de conteúdo não incluídos na licença do AEM Assets</a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25562">Resolução de problemas de conexão do AEM Asset Link no InDesign</a></td>
      <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25525">Resolução de problemas de processamento de ativos no AEM as a Cloud Service</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25506">Erro de rede do plug-in do Adobe Asset Link: servidor inacessível</a></td>
      <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25829">Atualizando miniaturas personalizadas de ativos de vídeo no AEM as a Cloud Service</a>
      </td>
    </tr>
  </tbody>
</table>




## Solução de problemas do AEM Forms {#aem-forms-troubleshooting}

O AEM Forms as a Cloud Service oferece recursos avançados de criação e gerenciamento de formulários. No entanto, você pode encontrar problemas durante os processos de instalação, configuração, criação de formulários ou envio. Esta seção fornece orientação abrangente de solução de problemas comuns do AEM Forms.

### Problemas de instalação e configuração

<table>
  <tbody>
  <tr>
    <td><strong>Instalação e configuração</strong></td>
    <td><strong>Problemas de criação de formulário</strong></td>
    <td><strong>Desempenho e cache</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">Opção do Forms indisponível na navegação</a></td>
    <td><a href="/help/forms/form-creation-failing.md">Falha na criação do formulário após a publicação do modelo</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">Problemas de cache adaptável do Forms</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">Falhas de build de pipeline</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">Problemas de sequência de publicação de modelo</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Problemas de invalidação do cache do Dispatcher</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">Problemas de ativação de pacote</a></td>
    <td><a href="/help/forms/known-issues.md">Limitações conhecidas da criação de formulários</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">Falhas de armazenamento em cache do CDN</a></td>
  </tr>
  </tbody>
</table>

### Problemas de envio e integração de formulários

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>Ações de envio personalizadas</strong></td>
    <td><strong>Problemas de integração</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403 Erros proibidos no envio do formulário</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">502 erros em ações de envio personalizadas</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-27434">Falhas de redirecionamento de DRM-SAML</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">Problemas de configuração do CORS</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">Tratamento de exceção sem tratamento</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-27075">O botão Enviar está desativado no AEM Sites</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">Configuração do Filtro referenciador</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">Práticas recomendadas para ações personalizadas</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26532">Visibilidade de campos ocultos após atualizações</a></td>
  </tr>
  </tbody>
</table>

### Problemas do Designer e de desenvolvimento

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>Ambiente de desenvolvimento</strong></td>
    <td><strong>Versão e compatibilidade</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26558">O Designer 6.5 não abre após a atualização</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-27089">Falha dos localizadores ao iniciar com o JDK 8/11</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26862">Problemas de exibição da versão do pacote do AEM Forms (AEMFD)</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-21018">Erros do PDF Generator JPEG 2000</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-22689">Configuração do caminho do log JBoss</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26846">Números de versão incorretos no Windows</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-27406">Botão ausente na saída do PDF</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-18084">Erros de atualização do Configuration Manager</a></td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-17339">Soluções alternativas de corrupção de índice</a></td>
  </tr>
  </tbody>
</table>



