---
title: Como melhorar o desempenho de formulários grandes com carregamento lento?
description: Saiba mais sobre como melhorar o desempenho de formulários grandes com carregamento lento. O carregamento lento melhora significativamente o desempenho do Adaptive Forms grande e complexo, adiando a inicialização e o carregamento de fragmentos de formulário até que fiquem visíveis.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 0cd38edb-2201-4ca6-8b84-6b5b7f76bd90
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# Melhore o desempenho de formulários grandes com carregamento lento{#improve-performance-of-large-forms-with-lazy-loading}

## Introdução ao carregamento lento {#introduction-to-lazy-loading}

Quando o formulário se torna grande e complexo com centenas e milhares de campos, os usuários finais experimentam um longo tempo de resposta ao renderizar formulários no tempo de execução. Para minimizar o tempo de resposta, o Adaptive Forms permite quebrar formulários em fragmentos lógicos e configurar para adiar a inicialização ou o carregamento de fragmentos até que o fragmento precise estar visível. É chamado de carregamento lento. Além disso, os fragmentos configurados para carregamento lento são descarregados depois que o usuário navega para outras seções no formulário e os fragmentos não estão mais visíveis.

Vamos primeiro entender os requisitos e as etapas preparatórias antes de configurar o carregamento lento.

## Preparação para configurar o carregamento lento {#preparing-to-configure-lazy-loading}

Antes de configurar o carregamento lento de fragmentos em seu Formulário adaptativo, é importante definir estratégias para criar fragmentos, identificar valores que são usados em scripts ou referenciados em outros fragmentos e definir regras para controlar a visibilidade dos campos em fragmentos carregados lentamente.

* **Identificar e criar fragmentos**
Você pode configurar somente os Fragmentos de formulário adaptáveis para o carregamento lento. Um fragmento é um segmento independente que fica fora de um formulário adaptável e pode ser reutilizado em formulários. Assim, o primeiro passo para implementar o carregamento lento é identificar seções lógicas em um formulário e convertê-las em fragmentos. É possível criar um fragmento do zero ou salvar um painel de formulário existente como fragmento.

   <!--For more information about creating fragments, see [Adaptive Form Fragments](adaptive-form-fragments.md).-->

* **Identificar e marcar valores globais**
As transações baseadas em Forms envolvem elementos dinâmicos para capturar dados relevantes dos usuários e processá-los para simplificar a experiência de preenchimento de formulários. Por exemplo, seu formulário tem o campo A no fragmento X cujo valor determina a validade do campo B em outro fragmento. Nesse caso, se o fragmento X estiver marcado para carregamento lento, o valor do campo A deverá estar disponível para validar o campo B mesmo quando o fragmento X não estiver carregado. Para isso, é possível marcar o campo A como global, o que garante que seu valor esteja disponível para a validação do campo B quando o fragmento X não estiver carregado.

   Para obter informações sobre como tornar um valor de campo global, consulte [Configuração do carregamento lento](lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Gravar regras para controlar a visibilidade dos campos**
O Forms inclui alguns campos e seções que não se aplicam a todos os usuários e em todas as condições. Os autores e desenvolvedores do Forms usam regras de visibilidade ou mostrar para controlar sua visibilidade com base nas entradas do usuário. Por exemplo, o campo Endereço do escritório não é exibido para os usuários que escolhem Desempregado no campo Status do Emprego em um formulário. Para obter mais informações sobre regras de gravação, consulte [Uso do editor de regras](rule-editor.md).

   Você pode usar regras de visibilidade nos fragmentos carregados de preguiça para que campos condicionais sejam mostrados somente quando necessário. Além disso, marque o campo condicional global para referenciá-lo na expressão de visibilidade do fragmento carregado lentamente.

## Configuração do carregamento lento {#configuring-lazy-loading}

Execute as seguintes etapas para ativar o carregamento lento em um Fragmento de formulário adaptável:

1. Abra o Formulário adaptável no modo de criação que contém o fragmento que deseja ativar para carregamento lento.
1. Selecione o Fragmento do formulário adaptável e toque em ![configure](assets/configure-icon.svg).
1. Na barra lateral, ative **[!UICONTROL Carregar fragmento lentamente]** e tocar **Concluído**.

   ![Habilitar carregamento lento para o Fragmento do formulário adaptável](assets/lazy-loading-fragment.png)

   O fragmento agora está ativado para carregamento lento.

É possível marcar os valores dos objetos no fragmento carregado lentamente como global para que eles estejam disponíveis para uso em scripts quando o fragmento contido não estiver carregado. Faça o seguinte:

1. Abra o Fragmento do formulário adaptável no modo de criação.
1. Toque no campo cujo valor você deseja marcar como global e toque em ![configure](assets/configure-icon.svg).
1. Na barra lateral, ative **[!UICONTROL Usar valor durante o carregamento lento]**.

   ![Campo de carregamento lento na barra lateral](assets/enable-lazy-loading.png)

   O valor agora é marcado como global e está disponível para uso em scripts, mesmo quando o fragmento que contém é descarregado.

## Considerações e práticas recomendadas para configurar o carregamento lento {#considerations-and-best-practices-for-configuring-lazy-loading}

Algumas limitações, recomendações e pontos importantes a serem considerados ao trabalhar com o carregamento lento são as seguintes:

* É recomendável usar o Adaptive Forms baseado em esquema XSD no Forms adaptável baseado em XFA para configurar o carregamento lento em formulários grandes. O ganho de desempenho devido à implementação de carregamento lento no Forms adaptável baseado em XFA é relativamente menor do que o ganho no Forms adaptável baseado em XSD.
* Não configure o carregamento lento em fragmentos em um formulário adaptável que use **[!UICONTROL Responsivo - tudo em uma página sem navegação]** layout para o painel raiz. Como resultado da configuração do layout responsivo, todos os fragmentos são carregados simultaneamente em um formulário adaptável. Também pode resultar em desempenho degradado.
* É recomendável não configurar o carregamento lento em fragmentos no primeiro painel que é renderizado ao carregar o formulário adaptável.
* O carregamento lento é compatível com até dois níveis na hierarquia de fragmentos.
* Certifique-se de que os campos marcados como globais sejam exclusivos em um Formulário adaptável.
* Considere escrever regras de visibilidade para fragmentos que devem mostrar ou ocultar com base em uma condição. Por exemplo, você pode mostrar ou ocultar o fragmento Detalhes do Cônjuge com base no status civil especificado por um usuário.
* O anexo de arquivo e os componentes Termos e condições não são suportados em fragmentos carregados de forma preguiçosa.

### Práticas recomendadas de script para configurar o carregamento lento {#scripting-best-practices-for-configuring-lazy-loading}

Pontos importantes a serem considerados ao desenvolver scripts para painéis de carregamento lento são os seguintes:

* Certifique-se de que os scripts de inicialização e cálculo usados nos campos de um fragmento carregado lento sejam despotentes na natureza. Os scripts Idempotentes são aqueles que têm o mesmo efeito mesmo após várias execuções.
* Use a propriedade de campos globalmente disponível para disponibilizar o valor dos campos localizados em um painel de carregamento lento para todos os outros painéis de um formulário.
* Não encaminhe o valor de referência de um campo dentro de um painel lento, independentemente de o campo estar sendo marcado globalmente em fragmentos ou não.
* Use o recurso de redefinição do painel para redefinir tudo o que está visível no painel, usando a seguinte expressão de clique.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;}).resetData()
