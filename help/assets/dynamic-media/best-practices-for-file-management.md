---
title: Práticas recomendadas para organizar ativos digitais para usar Perfis de imagem Dynamic Media ou Perfis de vídeo
description: Dicas e práticas recomendadas para nomear, organizar e gerenciar arquivos de ativos de imagem e vídeo da Dynamic Media.
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: a64a7274f0037789be1a5e2f7427aba551f14ed7
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Práticas recomendadas para organizar ativos digitais para usar perfis de imagem ou perfis de vídeo{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Um conceito importante em relação ao uso de Perfis de imagem Dynamic Media ou Perfis de vídeo é que eles são atribuídos a pastas. Dentro de um perfil estão as configurações de uma imagem ou vídeo. Essas configurações processam o conteúdo de uma pasta junto com qualquer uma de suas subpastas. Portanto, a forma como você nomeia arquivos e pastas, organiza subpastas e lida com os arquivos dessas pastas afeta o modo como esses ativos são processados pelo perfil.

Usando estratégias de nomenclatura de arquivos e pastas consistentes e apropriadas, juntamente com boas práticas de metadados, você pode aproveitar ao máximo sua coleção de ativos digitais e garantir que os arquivos corretos sejam processados pelo perfil certo.

Consulte [Sobre o Perfil de imagem Dynamic Media e Perfis de vídeo](about-image-video-profiles.md).

Veja a seguir dicas de práticas recomendadas para organizar seus arquivos de ativos digitais.

* Organize seus arquivos com base nos metadados que você adicionou a eles em vez de nas pastas em que eles residem. É possível realizar essa prática adicionando perfis de metadados.

   * Consulte [Perfis de metadados.](/help/assets/metadata-profiles.md)
   * Consulte [Metadados para Gerenciamento de ativos digitais](/help/assets/manage-metadata.md).

* Geralmente, sua coleção de ativos digitais está sempre crescendo. Portanto, é importante, mais cedo, formalizar o uso de metadados, a estrutura de pastas e a nomenclatura de arquivos entre todos os ativos carregados. Padronizar com base nesses itens garante que, à medida que o seu pool de ativos digitais cresce, você possa aplicar perfis de processamento a pastas com maior precisão e consistência.
* Use pastas somente para impor uma estrutura de armazenamento consistente para seus ativos digitais. Por exemplo, as estruturas de pastas que podem ajudá-lo a refinar quais perfis atribuir podem incluir o seguinte:

   * **Pastas**  de desenvolvimento - contém ativos digitais em que você está trabalhando no momento.
   * **Pastas**  do cliente - contém ativos digitais com base em clientes ou nomes de projetos.
   * **Pastas**  de origem primária - contém ativos digitais de origem original.
   * **Pastas**  de execução - contém execuções e cópias dos ativos digitais originais de origem.
   * **Pastas**  de tamanho de arquivo - contém ativos digitais com base em arquivos de tamanho pequeno, médio ou grande.
   * **Pastas**  de preparo - contém ativos digitais que estão prontos para publicar ao vivo em seu site.
   * **Pastas**  do tipo MIME - contém ativos digitais específicos para tipos MIME, como imagens, documentos e multimídia.
   * **Arquivar pastas**  - contém ativos digitais desativados.
   * **Pastas**  baseadas em datas - contém ativos digitais com base em uma data de criação ou em uma data de última modificação.

* Crie um diretório de pastas que provavelmente não serão alteradas para que qualquer perfil atribuído não seja quebrado.
* Suponha que um ativo já tenha sido publicado, em seguida, use o Adobe Experience Manager para mover o ativo para outra pasta e publicar novamente a partir do novo local. A localização original do ativo publicado ainda está disponível, juntamente com o ativo recém-publicado. O ativo publicado original, no entanto, é &quot;perdido&quot; para a Experience Manager e não pode ser despublicado. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

