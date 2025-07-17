---
title: Criar aparências personalizadas em formulários HTML5
description: Você pode conectar widgets personalizados a um Forms móvel. Você pode estender widgets jQuery existentes ou desenvolver seus próprios widgets personalizados.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Criar aparências personalizadas em formulários HTML5{#create-custom-appearances-in-html-forms}

<span class="preview"> O recurso HTML5 Forms é oferecido como parte do Programa de acesso antecipado. Para solicitar acesso, envie um email de sua ID de email oficial (comercial) para aem-forms-ea@adobe.com.
</span>

Você pode conectar widgets personalizados a um Forms móvel. Você pode estender widgets jQuery existentes ou desenvolver seus próprios widgets personalizados usando a estrutura de aparências. O mecanismo XFA usa vários widgets, consulte [Estrutura de aparência para formulários adaptáveis e HTML5](/help/forms/custom-widgets.md) para obter informações detalhadas.

![Um exemplo de widget padrão e personalizado](assets/custom-widgets.jpg)

Um exemplo de widget padrão e personalizado

## Integração de widgets personalizados com formulários HTML5 {#integrating-custom-widgets-with-html-forms}

### Criar um perfil  {#create-a-profile-nbsp}

Você pode criar um perfil ou escolher um perfil existente para adicionar um widget personalizado. Para obter mais informações sobre como criar perfis, consulte [Criando um perfil personalizado](/help/forms/custom-profile.md).

### Criar um dispositivo {#create-a-widget}

Os formulários HTML5 fornecem uma implementação da estrutura de widgets que pode ser estendida para criar novos widgets. A implementação é um widget jQuery *abstractWidget* que pode ser estendido para gravar um novo widget. O novo widget pode se tornar funcional somente estendendo/substituindo as funções mencionadas abaixo.

<table>
 <tbody>
  <tr>
   <td>Função/Classe</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td>renderizar</td>
   <td>A função de renderização retorna o objeto jQuery para o elemento HTML padrão do widget. O elemento HTML padrão deve ser do tipo focalizável. Por exemplo, &lt;a&gt;, &lt;input&gt; e &lt;li&gt;. O elemento retornado é usado como $userControl. Se o $userControl especificar a restrição acima, então as funções da classe AbstractWidget funcionam como esperado, caso contrário algumas das APIs comuns (foco, clique) exigem alterações. </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>Retorna um mapa para converter eventos HTML em eventos XFA. <br /> {<br /> desfoque: XFA_EXIT_EVENT,<br /> }<br /> Este exemplo mostra que o desfoque é um evento HTML e XFA_EXIT_EVENT é um evento XFA correspondente. </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>Retorna um mapa que fornece detalhes sobre qual ação executar ao alterar uma opção. As teclas são as opções fornecidas ao widget e os valores são as funções que são chamadas sempre que uma alteração nessa opção é detectada. O widget fornece manipuladores para todas as opções comuns (exceto value e displayValue)</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>A estrutura Widget carrega a função sempre que o valor do widget é salvo no XFAModel (por exemplo, no evento de saída de um textField). A implementação deve retornar o valor salvo no widget. O manipulador recebe o novo valor da opção.</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>Por padrão, no XFA, em inserir evento, o rawValue do campo é exibido. Esta função é chamada para mostrar rawValue para o usuário. </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>Por padrão, no XFA no evento de saída, o valor formatado do campo é exibido. Esta função é chamada para mostrar o formattedValue para o usuário. </td>
  </tr>
 </tbody>
</table>

Para criar seu próprio widget, no perfil criado acima, inclua referências do arquivo JavaScript que contém funções substituídas e funções recém-adicionadas. Por exemplo, o *sliderNumericFieldWidget* é um widget para Campos numéricos. Para usar o widget em seu perfil na seção de cabeçalho, inclua a seguinte linha:

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### Registrar widget personalizado com o mecanismo de script XFA  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

Quando o código de widget personalizado estiver pronto, registre o widget com o mecanismo de script usando a `registerConfig`API para o [Form Bridge](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/developer-reference/form-bridge-apis). É necessário widgetConfigObject como entrada.

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

A configuração do widget é fornecida como um objeto JSON (uma coleção de pares de valores chave), em que a chave identifica os campos e o valor representa o widget a ser usado com esses campos. Um exemplo de configuração é semelhante a:

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

onde &quot;identifier&quot; é um seletor CSS jQuery que representa um campo específico, um conjunto de campos de um tipo específico ou todos os campos. Veja a seguir o valor do identificador em casos diferentes:

| Tipo de identificador | Identificador | Descrição |
|---|---|---|
| Campo específico com nome nome do campo | Identificador:&quot;div.fieldname&quot; | Todos os campos com o nome ‘fieldname’ são renderizados usando o widget. |
| Todos os campos do tipo &quot;type&quot;(onde type é NumericField, DateField, e assim por diante).: | Identificador: &quot;div.type&quot; | Para Timefield e DateTimeField, o tipo é textfield, pois esses campos não são compatíveis. |
| Todos os campos | Identificador: &quot;div.field&quot; |  |
