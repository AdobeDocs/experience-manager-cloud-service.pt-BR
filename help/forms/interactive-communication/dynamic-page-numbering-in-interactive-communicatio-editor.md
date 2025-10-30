---
title: Numeração dinâmica de páginas no Editor de comunicação interativa
description: A Numeração dinâmica de páginas no Editor de comunicação interativa permite que os autores exibam automaticamente números de página em sua saída do PDF.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: dae482e1f57a3504bf08926b57b89ca9266bd36a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Numeração dinâmica de páginas no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## Introdução

O recurso de Numeração dinâmica de páginas na Comunicação interativa (IC) permite que os autores exibam automaticamente números de página na saída do PDF. A numeração de páginas pode ser ativada no nível da página principal, garantindo uma numeração consistente em todas as páginas de design associadas. Isso ajuda a manter um rastreamento de página claro e um layout profissional em comunicações de várias páginas.

## Principais recursos

- **Configuração da Página Mestra:**
A numeração de páginas pode ser ativada no nível da página-mestre. O componente pode ser colocado em qualquer lugar na tela depois de ter sido solto e personalizado livremente, pois suporta todas as propriedades disponíveis no componente de texto.

- **Posicionamento Automático:**
Um componente de numeração de página é exibido no centro inferior de cada página com o formato:
&quot;**Página nº de ##**&quot;

   - O primeiro **#** representa o número de página atual.

   - O segundo **##** representa o número total de páginas na comunicação.

- **Exibição Dinâmica na Visualização do PDF:**
Os números de página são renderizados dinamicamente durante a pré-visualização do PDF, exibindo uma numeração de página precisa na saída final.

### Exemplo

Ao visualizar uma Comunicação interativa de 5 páginas, cada página exibirá:

Página 1 de 5

Página 2 de 5

... e assim por diante, atualização dinâmica durante a geração do PDF.

## Principais benefícios

- Aprimora a legibilidade e o profissionalismo dos documentos.

- Automatiza a numeração de páginas sem intervenção manual.

- Mantém a consistência em todas as páginas vinculadas a uma página mestra.
