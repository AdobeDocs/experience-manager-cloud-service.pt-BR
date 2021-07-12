---
title: Práticas recomendadas para organizar ativos digitais para usar perfis de imagem ou perfis de vídeo do Dynamic Media
description: '"Dicas e práticas recomendadas para nomear, organizar e gerenciar arquivos de imagem e de ativos de vídeo da Dynamic Media."'
contentOwner: Rick Brough
feature: Gerenciamento de ativos, Perfis de imagem, Perfis de vídeo
role: Admin,User
exl-id: 82ab5432-088c-4442-a9db-9f4e0184febf
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Práticas recomendadas para organizar ativos digitais para usar perfis de imagem ou perfis de vídeo{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Um conceito importante relacionado ao uso de perfis de imagem ou perfis de vídeo do Dynamic Media é que eles são atribuídos a pastas. Dentro de um perfil estão as configurações de uma imagem ou vídeo. Essas configurações processam o conteúdo de uma pasta junto com qualquer uma de suas subpastas. Portanto, nomear arquivos e pastas, organizar subpastas e manipular os arquivos nessas pastas afeta como esses ativos são processados pelo perfil.

Ao usar estratégias consistentes e apropriadas de nomeação de arquivos e pastas, juntamente com uma boa prática de metadados, você aproveita ao máximo sua coleção de ativos digitais e garante que os arquivos corretos sejam processados pelo perfil correto.

Consulte [Sobre Perfil de imagem do Dynamic Media e Perfis de vídeo](about-image-video-profiles.md).

A seguir estão dicas de práticas recomendadas para organizar seus arquivos de ativos digitais.

* Organize seus arquivos com base nos metadados que você adicionou a eles em vez de nas pastas em que eles residem. Você pode realizar essa prática adicionando perfis de metadados.

   * Consulte [Perfis de metadados](/help/assets/metadata-profiles.md).
   * Consulte [Metadados para Gerenciamento de ativos digitais](/help/assets/manage-metadata.md).

* Geralmente, sua coleção de ativos digitais está sempre crescendo. Portanto, é importante - anteriormente - formalizar o uso de metadados, a estrutura de pastas e a nomenclatura de arquivos entre todos os ativos carregados. Padronizar essas coisas garante que, à medida que o conjunto de ativos digitais cresce, você possa aplicar perfis de processamento a pastas com maior precisão e consistência.
* Use pastas somente para impor uma estrutura de armazenamento consistente para seus ativos digitais. Por exemplo, as estruturas de pastas que podem ajudar você a refinar quais perfis atribuir podem incluir o seguinte:

   * **Pastas de desenvolvimento**  - contém ativos digitais em que você está trabalhando no momento.
   * **Pastas do cliente**  - contém ativos digitais com base em clientes ou nomes de projeto.
   * **Pastas de origem primária**  - contém ativos digitais de origem originais.
   * **Pastas de representação**  - contém representações e cópias dos ativos digitais de origem original.
   * **Pastas de tamanho de arquivo**  - contém ativos digitais com base em tamanhos de arquivo pequenos, médios ou grandes.
   * **Pastas de preparo**  - contém ativos digitais que estão prontos para publicar ao vivo em seu site.
   * **Pastas do tipo MIME**  - contém ativos digitais específicos para tipos MIME, como imagens, documentos e multimídia.
   * **Pastas de arquivamento**  - contém ativos digitais descontinuados.
   * **Pastas baseadas em data**  - contém ativos digitais com base em uma data de criação ou em uma data da última modificação.

* Crie um diretório de pastas que provavelmente não será alterado para que os perfis atribuídos não sejam interrompidos.
* Suponha que um ativo já tenha sido publicado, então use o Adobe Experience Manager para movê-lo para outra pasta e republicar de seu novo local. O local do ativo publicado original ainda está disponível, juntamente com o ativo republicado recentemente. O ativo publicado original, no entanto, é &quot;perdido&quot; para o Experience Manager e não pode ter a publicação cancelada. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.
