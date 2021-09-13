---
title: Gerenciador de vários sites e tradução
description: Saiba como reutilizar seu conteúdo em seu projeto e gerenciar sites multilíngues no AEM.
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# Gerenciador de vários sites e tradução {#msm-and-translation}

O Adobe Experience Manager integrado Multi Site Manager e as ferramentas de tradução simplificam a localização do conteúdo.

* O Multi Site Manager (MSM) e seus recursos de Live Copy permitem usar o mesmo conteúdo de site em vários locais, permitindo variações:
   * [Reutilizar conteúdo: gerenciador de vários sites e Live Copy](msm/overview.md)
* A tradução permite automatizar a tradução do conteúdo da página para criar e manter sites multilíngues:
   * [Tradução de conteúdo para sites multilíngues](translation/overview.md)

Esses dois recursos podem ser combinados para atender a sites que são [multinacionais e multilíngues](#multinational-and-multilingual-sites).

>[!TIP]
>
>Se você não estiver familiarizado com a tradução de conteúdo, consulte nossa [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é o caminho orientado pela tradução do conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideal para aqueles sem AEM ou experiência de tradução.

## Sites multinacionais e multilíngues {#multinational-and-multilingual-sites}

Você pode criar conteúdo com eficiência para sites multinacionais e multilíngues usando o Gerenciador de vários sites e o fluxo de trabalho de tradução.

Normalmente, você cria um site principal em um idioma e para um país específico, em seguida, usa esse conteúdo como base para os outros sites, usando tradução quando necessário.

1. [](translation/overview.md) Traduza o site principal em diferentes idiomas.
1. Use [Gerenciador de vários sites](msm/overview.md) para:
   1. Reutilize o conteúdo do site principal e suas traduções para criar sites para outros países e culturas.
   1. Quando necessário, desanexe elementos das Live Copies para adicionar detalhes de localização.

>[!TIP]
>
>Limite o uso do Multi Site Manager para conteúdo em um idioma.
>
>Por exemplo, use o principal inglês para criar a versão em inglês das páginas para os EUA, Canadá, Reino Unido etc. e usar o principal francês para criar a versão em francês das páginas para França, Suíça, Canadá etc.

O diagrama a seguir ilustra como os principais conceitos se cruzam (mas não mostra todos os níveis/elementos envolvidos):

![Visão geral da localização](assets/localization-overview.png)

Neste cenário, e em situações comparáveis, o MSM não gerencia as diferentes versões de idioma como tal.

* [](msm/overview.md) O MSMgerencia a implantação de conteúdo traduzido de um blueprint (ou seja, um principal global) para as Live Copies (ou seja, os sites locais), dentro dos limites de um idioma.
* Os recursos de integração [translation](translation/overview.md) do AEM, juntamente com serviços de gerenciamento de tradução de terceiros, gerenciam os idiomas e traduzem o conteúdo nesses diferentes idiomas.

Para casos de uso mais avançados, o MSM também pode ser usado em mestres de idiomas.

>[!TIP]
>
>Em todos os casos de uso, é recomendável ler as seguintes práticas recomendadas:
>
>* [Práticas recomendadas para MSM](msm/best-practices.md)
>* [Práticas recomendadas para tradução](translation/best-practices.md)

