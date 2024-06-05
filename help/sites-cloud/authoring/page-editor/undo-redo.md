---
title: Limitações de Desfazer e Refazer
description: Saiba mais sobre as limitações das opções desfazer e refazer no editor de páginas AEM.
exl-id: 87773f47-5116-4966-9ba4-5deedb7c4fa6
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 92%

---

# Limitações de Desfazer e Refazer {#undo-redo}

O AEM armazena um histórico de ações que você executa e a sequência na qual as executou, para que você possa desfazer várias ações na ordem em que as executou ou refazê-las pra reaplicar uma ou mais ações, se necessário.

Se um elemento na página de conteúdo estiver selecionado (po exemplo, como um componente de texto), o comando de desfazer e refazer será aplicado ao item selecionado.

O comportamento dos comandos desfazer e refazer é semelhante ao de outros softwares. Use os comandos para restaurar o estado recente da sua página da Web, conforme você decide sobre o conteúdo. Por exemplo, caso mova um parágrafo de texto para um local diferente na página, você pode usar o comando desfazer para mover o parágrafo de volta. Se você decidir que a posição anterior era melhor, use o comando Refazer para “desfazer a ação de desfazer”.

Por exemplo, você pode:

* Refazer ações desde que não tenha feito nenhuma edição da página desde que usou o comando desfazer.
* Desfazer no máximo 20 ações de edição (configuração padrão).
* Usar os [Atalhos de teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) para desfazer e refazer.

É possível desfazer ou refazer os seguintes tipos de alterações de página:

* Adição, edição, remoção e movimentação de parágrafos
* Edição no local do conteúdo do parágrafo
* Cópia, recorte e colagem de itens em uma página

>[!NOTE]
>
>* Permissões especiais são necessárias para desfazer e refazer as alterações nos arquivos e imagens.
>* O histórico de alterações em arquivos e imagens dura no mínimo dez horas. Além desse período, no entanto, a ação de desfazer as alterações não é garantida. Seu administrador pode alterar o tempo padrão de dez horas.
>* O administrador do sistema pode configurar vários aspectos dos recursos desfazer/refazer de acordo com os requisitos de sua ocorrência.
