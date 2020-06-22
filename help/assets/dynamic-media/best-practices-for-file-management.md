---
title: Práticas recomendadas para organizar ativos digitais para usar Perfis de imagem Dynamic Media ou Perfis de vídeo
description: Dicas e práticas recomendadas para nomear, organizar e gerenciar arquivos de ativos de imagem e vídeo da Dynamic Media.
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Práticas recomendadas para organizar ativos digitais para uso de perfis de imagem ou perfis de vídeo{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Um conceito importante em relação ao uso de Perfis de imagem Dynamic Media ou Perfis de vídeo é que eles são atribuídos a pastas. Dentro de um perfil estão as configurações de uma imagem ou vídeo. Essas configurações processam o conteúdo de uma pasta junto com qualquer uma de suas subpastas. Portanto, a forma como você nomeia arquivos e pastas, como você organiza as subpastas e como manipula os arquivos dessas pastas tem um impacto significativo na forma como esses ativos são processados pelo perfil.

Usando estratégias de nomenclatura de arquivos e pastas consistentes e apropriadas, juntamente com boas práticas de metadados, você pode aproveitar ao máximo sua coleção de ativos digitais e garantir que os arquivos corretos sejam processados pelo perfil certo.

Consulte [Sobre o Perfil de imagem Dynamic Media e Perfis](about-image-video-profiles.md)de vídeo.

Veja a seguir dicas de práticas recomendadas para organizar seus arquivos de ativos digitais.

* Organize seus arquivos com base nos metadados que você adicionou a eles em vez de nas pastas em que eles residem. É possível fazer isso adicionando perfis de metadados.

   * Consulte Perfis [de metadados.](/help/assets/metadata-profiles.md)
   * Consulte [Metadados para gerenciamento](/help/assets/manage-metadata.md)de ativos digitais.

* Na maioria dos casos, sua coleção de ativos digitais está sempre crescendo. Portanto, é importante, mais cedo, formalizar o uso de metadados, a estrutura de pastas e a nomenclatura de arquivos entre todos os ativos carregados. Padronizar com base nesses itens garante que, à medida que o seu pool de ativos digitais cresce, você possa aplicar perfis de processamento a pastas com maior precisão e consistência.
* Use pastas somente para impor uma estrutura de armazenamento consistente para seus ativos digitais. Por exemplo, as estruturas de pastas que podem ajudá-lo a refinar quais perfis atribuir podem incluir o seguinte:

   * **Pastas** de desenvolvimento - contém ativos digitais em que você está trabalhando no momento.
   * **Pastas** do cliente - contém ativos digitais com base em clientes ou nomes de projetos.
   * **Pastas** de origem primária - contém ativos digitais de origem original.
   * **Pastas** de execução - contém execuções e cópias dos ativos digitais originais de origem.
   * **Pastas** de tamanho de arquivo - contém ativos digitais com base em arquivos de tamanho pequeno, médio ou grande.
   * **Pastas** de preparo - contém ativos digitais que estão prontos para publicar ao vivo em seu site.
   * **Pastas** do tipo MIME - contém ativos digitais específicos para tipos MIME, como imagens, documentos e multimídia.
   * **Arquivar pastas** - contém ativos digitais desativados.
   * **Pastas** baseadas em datas - contém ativos digitais com base em uma data de criação ou em uma data de última modificação.

* Crie um diretório de pastas que provavelmente não serão alteradas para que qualquer perfil atribuído não seja quebrado.
* Se um ativo já tiver sido publicado, você usará o AEM para mover o ativo para outra pasta e republicar de seu novo local, o local original do ativo publicado ainda estará disponível, juntamente com o ativo recém-publicado. O ativo publicado original, no entanto, é &quot;perdido&quot; para o AEM e não pode ser despublicado. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

