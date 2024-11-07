---
title: Configurar a invalidação por push
description: Saiba mais sobre como configurar a invalidação de push para criar seu próprio CDN de produção.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
source-git-commit: 3941b7f97d434946a3cb796633f306b89e68c0a4
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 2%

---

# Configurar invalidação por push

A invalidação por push garante que as atualizações de conteúdo feitas por autores sejam removidas automaticamente da Rede de entrega de conteúdo (CDN) gerenciada quando publicada, para que somente o conteúdo mais recente seja distribuído.

O sistema limpa o conteúdo com base em URLs específicos e tags ou chaves de cache, garantindo que as versões desatualizadas sejam removidas.

Para ativar a invalidação por push, propriedades específicas devem ser adicionadas ao arquivo de configuração do projeto. Por exemplo, uma pasta de trabalho do Microsoft Excel chamada `.helix/config.xlsx` no SharePoint ou uma Planilha Google chamada `.helix/config` no Google Drive.

As seguintes propriedades de configuração definem o nome do host de produção e o tipo de gerenciamento CDN:

| key | valor | comentário |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | Nome do host do site de produção. Por exemplo, `www.example.com`. |
| `cdn.prod.type` | gerenciado |   |

Depois que as alterações forem feitas na folha de configuração, os usuários deverão visualizá-las e ativá-las usando a [ferramenta Sidekick](/help/edge/docs/sidekick.md) para aplicar as atualizações.
