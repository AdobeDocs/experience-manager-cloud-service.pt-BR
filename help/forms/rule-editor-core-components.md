---
title: Como usar o editor de regras para adicionar regras a campos de formulário para adicionar comportamento dinâmico e criar lógica complexa a um formulário adaptável com base em componentes principais?
description: O editor de regras Forms adaptável permite adicionar comportamento dinâmico e criar lógica complexa em formulários sem codificação ou script.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 1292f729-c6eb-4e1b-b84c-c66c89dc53ae
source-git-commit: 8585ec309b04e04b9a8dcaa43063369d1c9d5d24
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 4%

---


# Introdução ao Editor de regras para o Formulário adaptável com base nos Componentes principais

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service (Componentes principais) | Este artigo |
| AEM as a Cloud Service (Componentes de base) | [Clique aqui](/help/forms/rule-editor.md) |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html) |

Em um Formulário adaptável baseado em Componentes principais, o recurso do editor de regras permite que usuários empresariais e desenvolvedores gravem regras para objetos de Formulário adaptável. Essas regras definem as ações a serem acionadas nos objetos de formulário com base nas condições predefinidas, entradas do usuário e ações do usuário no formulário. Esse recurso ajuda a simplificar ainda mais a experiência de preenchimento de formulário, garantindo precisão e velocidade.

O editor de regras fornece uma interface de usuário intuitiva e simplificada para escrever regras. Ele oferece um editor visual que atende a todos os usuários, permitindo que eles criem e gerenciem regras sem precisar de extenso conhecimento técnico. Essa abordagem visual facilita a compreensão e a implementação da lógica desejada em seus formulários.

Algumas das ações principais que você pode executar em objetos do Formulário adaptável usando regras são:

* Mostrar ou ocultar um objeto
* Habilitar ou desabilitar um objeto
* Definir um valor para um objeto
* Validar o valor de um objeto
* Executar funções para calcular o valor de um objeto
* Chamar um serviço de modelo de dados de formulário (FDM) e executar uma operação
* Definir a propriedade de um objeto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Os usuários adicionados ao grupo `forms-power-users` podem criar scripts e editar os existentes. Os usuários do grupo [!DNL forms-users] podem usar os scripts, mas não podem criá-los ou editá-los.

Consulte o artigo [Diferença entre o Editor de Regras do Foundation e o Editor de Regras do Componente Principal](/help/forms/rule-editor-core-components-difference-tables.md) para obter uma comparação detalhada.

<!--
## Difference between Rule editor in Core Components and Rule Editor in Foundation Components

{{rule-editor-diff}}

>[!NOTE]
>
> To see how to create and use custom functions in detail, refer to [Custom functions in Adaptive Forms (Core Components)](/help/forms/create-and-use-custom-functions.md) article.

-->

## Noções básicas sobre uma regra {#understanding-a-rule}

Uma regra é uma combinação de ações e condições. No editor de regras, as ações incluem atividades como ocultar, mostrar, habilitar, desabilitar ou calcular o valor de um objeto em um formulário. As condições são expressões booleanas que são avaliadas executando verificações e operações no estado, valor ou propriedade de um objeto de formulário. As ações são executadas com base no valor ( `True` ou `False`) retornado pela avaliação de uma condição.

O editor de regras fornece um conjunto de tipos de regras predefinidos, como Quando, Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar, para ajudá-lo a escrever regras. Cada tipo de regra permite definir condições e ações em uma regra. O documento explica detalhadamente cada tipo de regra.

Uma regra normalmente segue uma das seguintes construções:

**Condition-Action** Nesta construção, uma regra primeiro define uma condição seguida por uma ação a ser acionada. A construção é comparável à instrução if-then em linguagens de programação.

No editor de regras, o tipo de regra **When** impõe a construção de condição-ação.

**Condição-ação** Nesta construção, uma regra primeiro define uma ação a ser acionada seguida por condições para avaliação. Outra variação dessa construção é ação-condição-ação alternativa, que também define uma ação alternativa a ser acionada se a condição retornar Falso.

Os tipos de regra Mostrar, Ocultar, Ativar, Desativar, Definir valor de e Validar no editor de regras impõem a construção de regra de condição de ação. Por padrão, a ação alternativa para Mostrar é Ocultar, e para Habilitar é Desabilitar e o oposto. Não é possível alterar a ação alternativa padrão.

>[!NOTE]
>
>Os tipos de regras disponíveis, incluindo condições e ações definidas no editor de regras, também dependem do tipo de objeto de formulário no qual você está criando uma regra. O editor de regras exibe somente tipos de regras válidos e opções para gravar instruções de condição e ação para um determinado tipo de objeto de formulário. Por exemplo, você não vê os tipos Validar e Definir valor de para um objeto de painel.

Para obter mais informações sobre tipos de regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Diretrizes para a escolha de uma construção de regra {#guidelines-for-choosing-a-rule-construct}

Embora seja possível obter a maioria dos casos de uso usando qualquer construção de regra, veja a seguir algumas diretrizes para escolher uma construção em vez de outra. Para obter mais informações sobre as regras disponíveis no editor de regras, consulte [Tipos de regras disponíveis no editor de regras](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* Uma regra prática comum ao criar uma regra é pensar nela no contexto do objeto no qual você está escrevendo uma regra. Considere que deseja ocultar ou mostrar o campo B com base no valor especificado por um usuário no campo A. Nesse caso, você está avaliando uma condição no campo A e, com base no valor retornado, aciona uma ação no campo B.

  Portanto, se estiver gravando uma regra no campo B (o objeto no qual você está avaliando uma condição), use a construção de condição-ação ou o tipo de regra When. Da mesma forma, use a construção action-condition ou o tipo de regra Mostrar ou Ocultar no campo A.

* Às vezes, você deve executar várias ações com base em uma condição. Nesses casos, é recomendável usar a construção condição-ação. Nesta construção, você pode avaliar uma condição uma vez e especificar várias instruções de ação.

  Por exemplo, para ocultar os campos B, C e D com base na condição que verifica o valor especificado por um usuário no campo A, grave uma regra com construção de condição-ação ou Quando tipo de regra no campo A e especifique ações para controlar a visibilidade dos campos B, C e D. Caso contrário, você precisará de três regras separadas nos campos B, C e D, em que cada regra verifica a condição e mostra ou oculta o respectivo campo. Neste exemplo, é mais eficiente escrever o tipo de regra Quando em um objeto do que o tipo de regra Mostrar ou Ocultar em três objetos.

* Para acionar uma ação com base em várias condições, é recomendável usar uma construção action-condition. Por exemplo, para mostrar e ocultar o campo A avaliando as condições nos campos B, C e D, use o tipo de regra Mostrar ou Ocultar no campo A.
* Use a construção de condição-ação ou condição de ação se a regra contiver uma ação para uma condição.
* Se uma regra verificar uma condição e executar uma ação imediatamente ao fornecer um valor em um campo ou ao sair de um campo, é recomendável gravar uma regra com uma construção de condição-ação ou o tipo de regra Quando no campo em que a condição é avaliada.
* A condição na regra Quando é avaliada quando um usuário altera o valor do objeto no qual a regra Quando é aplicada. No entanto, se você quiser que a ação seja acionada quando o valor for alterado no lado do servidor, como para preencher previamente o valor, é recomendável gravar uma regra When que aciona a ação quando o campo é inicializado.
* Ao escrever regras para objetos de menus suspensos, botões de opção ou caixas de seleção, as opções ou os valores desses objetos de formulário no formulário são preenchidos previamente no editor de regras.

Para entender como usar a interface de usuário para gravar e gerenciar regras em um Editor de regras, consulte o artigo [Interface de usuário do Editor de regras para o Forms adaptável com base nos Componentes principais](/help/forms/rule-editor-core-components-user-interface.md).

## Consulte também

{{see-also-rule-editor}}