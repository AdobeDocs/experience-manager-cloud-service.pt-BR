---
title: Alteração de estilos padrão de formulários HTML5
description: O estilo dos formulários HTML5 é baseado em CSS. É possível alterar os estilos padrão do formulário.
content-type: reference
topic-tags: hTML5_forms
feature: HTML5 Forms,Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1496d7517d586c99c5f1001fff13d88275e91d09
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Alteração de estilos padrão de formulários HTML5{#changing-default-styles-of-html-forms}

<span class="preview"> O recurso HTML5 Forms é oferecido como parte do Programa de acesso antecipado. Para solicitar acesso, envie um email de sua ID de email oficial (comercial) para aem-forms-ea@adobe.com.
</span>

Os formulários HTML5 são renderizados usando os recursos do HTML5 e o estilo do formulário renderizado é feito usando CSS. A aparência padrão de um formulário HTML5 é semelhante à sua representação do PDF. Os desenvolvedores podem usar o CSS personalizado para alterar a aparência padrão dos formulários HTML5.

Este artigo fornece informações passo a passo para alterar o estilo de um formulário HTML5 e o artigo [Introdução aos Estilos](/help/forms/css-styles.md) contém informações detalhadas sobre vários aspectos de estilo dos formulários HTML5. Certifique-se de ler o artigo Introdução aos estilos antes de executar as etapas mencionadas neste artigo.

As duas imagens a seguir mostram a diferença entre os estilos padrão e personalizados.

![imagens-002-pequenas](assets/pictures-002-small.png)

## Estilizar seus formulários {#style-your-forms}

1. **Escolha um perfil para adicionar estilos personalizados**

   Acesse a interface CRX DE na URL: **https://&lt;server>:&lt;port>/crx/de** e crie um perfil ou escolha um perfil existente. Para saber como criar um perfil, consulte [Criando um Perfil](/help/forms/custom-profile.md)

1. **Criar uma folha de estilos CSS para estilizar os formulários HTML5**

   Navegue até a pasta em que você criou o renderizador de perfil e crie um arquivo de folha de estilos CSS. As etapas a seguir são

   1. Clique com o botão direito do mouse na pasta e selecione **criar** > **criar Arquivo** no menu

   1. Na caixa de diálogo Criar arquivo, digite o nome da folha de estilos. Use a extensão .css (por exemplo, stylesheet.css)
   1. No painel de navegação, abra o arquivo CSS criado.
   1. Defina as classes CSS dos componentes que deseja estilizar e adicione estilos a essas classes.

   Para saber quais classes CSS criar para um componente específico nos formulários HTML5, consulte [Introdução aos estilos](/help/forms/css-styles.md).

1. **Incluir a folha de estilos no Renderizador de Perfil**

   Abra a página Renderizador de perfil (arquivo jsp) no CRX DE e inclua o arquivo CSS na página logo abaixo da biblioteca de cliente XFA. Execute essas etapas para incluir o arquivo CSS no perfil.

   1. Pesquise na página do renderizador a seguinte linha:

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. Insira o seguinte abaixo da linha acima para incluir a folha de estilos:

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. Salve o arquivo.
