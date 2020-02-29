---
title: Referência dos esquemas de metadados
description: 'Saiba mais sobre as convenções padrão para descrever metadados de ativos, incluindo Dublin Core, IPTC e outros esquemas de metadados. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# Referência dos esquemas de metadados {#metadata-schemata-reference}

A referência a seguir inclui informações sobre esquemas de metadados específicos (em ordem alfabética), bem como uma lista de propriedades e suas definições.

## Dublin Core {#dublin-core}

Os metadados do Dublin Core fornecem um conjunto padronizado de convenções para descrever ativos para facilitar sua localização. Nos ativos AEM, o Dublin Core descreve ativos digitais, incluindo vídeo, som, imagens e documentos.

O conjunto simples de elementos de metadados principais de Dublin (DCMES) contém 15 elementos de metadados, conforme listados na tabela a seguir. Cada elemento de Dublin Core é opcional e pode ser repetido. Você pode adicionar ou excluir informações de metadados do Dublin Core como faria para metadados específicos de tipos de mídia.

Além do DCMES, existem outros elementos de metadados criados pela iniciativa Dublin Core. Consulte a iniciativa [](https://dublincore.org/) Dublin Core para obter mais informações.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td> 
   <td><strong>Descrição</strong></td> 
  </tr>
  <tr>
   <td>contribuinte</td> 
   <td>A pessoa ou empresa responsável pela contribuição para o conteúdo.</td> 
  </tr>
  <tr>
   <td>cobertura</td> 
   <td>A localização geográfica ou o período de tempo que o ativo cobre.<br /> </td> 
  </tr>
  <tr>
   <td>criadora</td> 
   <td>A pessoa ou empresa responsável pela criação do conteúdo.</td> 
  </tr>
  <tr>
   <td>date</td> 
   <td>Data ou período associado ao ativo.<br /> </td> 
  </tr>
  <tr>
   <td>descrição</td> 
   <td>Mais informações sobre o ativo.</td> 
  </tr>
  <tr>
   <td>format</td> 
   <td>O formato de arquivo, a mídia física ou as dimensões do ativo. O AEM usa <code>dc:format</code> para indicar o tipo MIME do ativo.<br /> </td> 
  </tr>
  <tr>
   <td>identifier</td> 
   <td>Uma referência exclusiva ao ativo.</td> 
  </tr>
  <tr>
   <td>language</td> 
   <td>O idioma do ativo (por exemplo, en para inglês).</td> 
  </tr>
  <tr>
   <td>editor</td> 
   <td>A pessoa ou empresa responsável pela disponibilização do ativo.</td> 
  </tr>
  <tr>
   <td>relation</td> 
   <td>Um ativo relacionado.</td> 
  </tr>
  <tr>
   <td>direitos</td> 
   <td>Informações sobre quem tem os direitos a este ativo.</td> 
  </tr>
  <tr>
   <td>source</td> 
   <td>Um ativo relacionado do qual o ativo é derivado.</td> 
  </tr>
  <tr>
   <td>assunto</td> 
   <td>O tópico do ativo.<br /> </td> 
  </tr>
  <tr>
   <td>título</td> 
   <td>Um nome para o ativo.</td> 
  </tr>
  <tr>
   <td>tipo</td> 
   <td>A natureza ou o gênero do ativo.</td> 
  </tr>
 </tbody>
</table>

## IPTC {#iptc}

O International Press Telecommunications Council (IPTC) é um consórcio de agências de notícias ao redor do mundo - um de seus objetivos é desenvolver e manter padrões técnicos. O IPTC definiu um conjunto de padrões de metadados de fotos para imagens que são aceitos quase universalmente pelos fotógrafos. Esses padrões de metadados faziam parte do padrão mais amplo conhecido como IPTC Information Interchange Model (IIM), criado nos anos 90.

Embora as informações do cabeçalho IPTC tenham sido substituídas principalmente por XMP, um esquema principal IPTC e um esquema de extensão estão disponíveis para XMP. Em programas de imagem, as propriedades XMP e IPTC são sincronizadas.
