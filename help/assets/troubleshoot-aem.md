---
title: Solução de problemas no AEM Assets
description: Solucione problemas comuns do AEM Assets usando os links de artigo para as principais áreas do AEM Assets, como uploads, metadados, pesquisa, delivery e assim por diante.
hidefromtoc: true
hide: true
source-git-commit: 60667c265cf480521fe0c0d646c2665540f110d0
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# Solução de problemas no AEM Assets {#troubleshoot-aem-assets}

O AEM Assets as a Cloud Service oferece uma solução PaaS nativa em nuvem para que as empresas não apenas executem suas operações de Gerenciamento de ativos digitais e Dynamic Media, mas também usem recursos inteligentes de próxima geração, como IA/ML. Tudo isso em um sistema que está sempre atualizado, sempre disponível e aprendendo.

No entanto, podem surgir problemas que afetem uploads de ativos, metadados, pesquisa ou delivery e outras áreas principais do AEM Assets. Este artigo fornece etapas de solução de problemas para ajudá-lo a diagnosticar e resolver esses problemas comuns do AEM Assets.

<table>
  <tbody>
  <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-27140">Representações ausentes no arquivo ZIP de download de ativos no AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26616">Fragmentos de conteúdo não incluídos na licença do AEM Assets</a> </td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26928">Comentário restrito na Exibição do Assets apesar do acesso de leitura</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26715">(Dynamic Media) Conjuntos de rotação presos no estado de processamento no AEM Dynamic Media</a> </td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26639">Representações do Gerenciamento de Ativos Digitais (DAM) que não correspondem aos arquivos originais no AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26873">Representações de corte inteligente não geradas no AEMaaCS</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26533">(Dynamic Media) Corrija problemas de carregamento, processamento e renderização de vídeo no AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26922">(Asset Link) O Adobe Asset Link deixa os links em um estado inacessível ao usar o InDesign</a> </td>
    <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26677">Incompatibilidade de miniatura de vídeo entre o Dynamic Media e a exibição de cartão DAM no AEMaaCS</a> </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26610">O processamento de ativos falhou para arquivos MP4 grandes no AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26871">(Dynamic Media) O reprodutor de vídeo Dynamic Media não funciona em ambientes inferiores</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26103">(Dynamic Media com OpenAPI) Ativar acesso restrito do Assets ao Dynamic Media com APIs abertas com base em grupos de usuários do IMS</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-23916">Quando um arquivo TIFF com formato de compactação ZIP é carregado no AEM Assets, nenhuma representação é gerada</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26785">O AEM trunca o texto extraído de PDFs grandes após 100 mil tokens</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-17628">(Dynamic Media) Alteração do URL do Dynamic Media para o DM Assets</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26655">Resolução de problemas de visibilidade de esquema de metadados para usuários não administradores no AEMaaCS</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26637">(Dynamic Media) Problema de alteração de cor do plano de fundo para representações de imagem do TIFF no Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26528">Problema de rotação do ativo AEMaaCS torna invisíveis as rotações subsequentes</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26367">(Dynamic Media) Resolução de um problema de imagem corrompida com o Recorte inteligente no Adobe Experience Manager 6.5 Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26450">Aumento do limite de upload de ativos de parte única para a integração da API do Firefly com o Photoshop</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26461">(Dynamic Media) Resolva as discrepâncias de nome de ativo do Dynamic Media em ambientes do AEM para arquivos PDF</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26233">Certas imagens não mostram representações de miniatura no Adobe Experience Manager (AEM) as a Cloud Service - Asset</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25294">(Dynamic Media) A página Configurações gerais do Dynamic Media não abre</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26197">(Dynamic Media) Resolva problemas de áudio em arquivos de vídeo com o Dynamic Media no AEM</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25925">Marcação automática de ativos recém-carregados no AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25889">A funcionalidade de Tags inteligentes não funciona após a migração do JWT para o OAuth no AEM</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25903">Resolver problemas de link compartilhado no AEM Managed Services</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25607">(Dynamic Media) Falha no processamento de ativos no AEM Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25885">(Dynamic Media) Falha de sincronização de ativos no Adobe Experience Manager (AEM) Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25829">Atualização de miniaturas personalizadas para ativos de vídeo no AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25828">Discrepância de metadados de imagem no Adobe Experience Manager (AEM) Assets</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-21865">Falha ao arrastar e soltar uma pasta de ativos para a interface do usuário da Web do AEM Assets</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25525">(Dynamic Media) Resolução de problemas de processamento de ativos no AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25518">Limitações de extração de texto para PDFs grandes no Adobe Experience Manager as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25562">(Link de ativos) Resolução de problemas de conexão do link de ativos do Adobe Experience Manager (AEM) no InDesign</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25506">(Asset Link) Erro de rede do plug-in do Adobe Asset Link: o servidor está inacessível</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-25471">(Dynamic Media) Recomendações do usuário para a sincronização de mídia dinâmica</a></td>
  <td><a href="https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-26902">(Dynamic Media) Exportar ativos e metadados do Dynamic Media usando a API</a></td>
  <td></td>
</tr>

</tbody>
  <table>


