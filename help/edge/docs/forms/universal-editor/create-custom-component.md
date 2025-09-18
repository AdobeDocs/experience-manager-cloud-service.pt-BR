---
title: Criar componentes personalizados para um formulário EDS
description: Criar componentes personalizados para um formulário EDS
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9664495d17ad8a8101c886408bee1584b3d48f1e
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---


# Criação de componente de formulário personalizado no bloco de formulário adaptável

O Edge Delivery Services Forms oferece personalização, permitindo que desenvolvedores de front-end criem componentes de formulário personalizados. Esses componentes personalizados se integram perfeitamente à experiência de criação do WYSIWYG, permitindo que os autores de formulários os adicionem, configurem e gerenciem facilmente no editor de formulários. Com componentes personalizados, os autores podem aprimorar a funcionalidade e, ao mesmo tempo, garantir um processo de criação simples e intuitivo.

Este documento descreve as etapas para criar componentes personalizados estilizando os componentes de formulário nativos do HTML para melhorar a experiência do usuário e aumentar o apelo visual do formulário.

## Visão geral da arquitetura

O componente personalizado para o Bloco Forms segue um padrão de arquitetura **MVC (Model-View-Controller)**:

### Modelo

- Definido pelo esquema JSON para cada `field/component`.

- As propriedades autoráveis são especificadas no arquivo JSON correspondente (consulte blocos/formulário/modelos/formulário-componentes).

- Essas propriedades estão disponíveis para autores no construtor de formulários e são passadas para o componente como parte da definição de campo (fd).

### Exibir

- A estrutura do HTML para cada tipo de campo é descrita em tipos de campo de formulário.

- Essa é a estrutura básica do seu componente que pode ser estendida ou modificada.

- A estrutura básica do HTML para cada componente OOTB é documentada em tipos de campo de formulário.

### Lógica do controlador/componente

- Implementado no JavaScript, como componentes prontos para uso ou personalizados.  - Localizado em `blocks/form/components` para componentes personalizados.

## Componentes OOTB

**Os componentes prontos para uso** fornecem a base para o desenvolvimento personalizado:

- Os componentes OOTB estão localizados em `blocks/form/models/form-components`.

- Cada componente OOTB tem um arquivo JSON que define suas propriedades que podem ser criadas (por exemplo, ` _text-input.json`,`_drop-down.json`).

- Essas propriedades estão disponíveis para autores no construtor de formulários e são passadas para o componente como parte da definição de campo (fd).

- A estrutura básica do HTML para cada componente OOTB é documentada em tipos de campo de formulário.

A extensão de um componente OOTB existente permite reutilizar sua estrutura básica, comportamento e propriedades, enquanto o personaliza para atender às suas necessidades.

- Os componentes personalizados devem se estender de um conjunto predefinido de componentes OOTB.

- O sistema identifica qual componente OOTB deve ser estendido com base na propriedade `viewType` no JSON do campo.

- O sistema mantém um registro das variantes de componente personalizadas permitidas. Somente as variantes listadas neste registro podem ser usadas, por exemplo, `customComponents[]` em `mappings.js`.

- Ao renderizar um formulário, o sistema verifica a propriedade de variante ou `:type/fd:viewType` e, se ele corresponder a um componente personalizado registrado, carrega os arquivos JS e CSS correspondentes da pasta `blocks/form/components`.

- O componente personalizado é aplicado à estrutura básica do HTML do componente OOTB, permitindo melhorar ou substituir seu comportamento e aparência.

## Estrutura do componente personalizado

Para criar componentes personalizados, você pode usar a **CLI de Scaffolder** para configurar os arquivos e pastas necessários para o seu componente e, em seguida, adicionar o código do componente personalizado.

- Os componentes personalizados residem na pasta `blocks/form/components`.

- Cada componente personalizado deve ser colocado em sua própria pasta, nomeada em homenagem ao componente, por exemplo, cartões. Dentro da pasta, os seguintes arquivos devem ser:

   - **_cards.json** - Arquivo JSON que estende a definição de componente de um componente OOTB, define suas propriedades que podem ser criadas (modelos[]) e estrutura de conteúdo na carga (definições[]).
   - **cards.js** - O arquivo JavaScript que inclui a lógica principal.
   - **cards.css** - opcional, para estilos.

- O nome da pasta e os arquivos JS/CSS devem corresponder.

### Reutilizar e estender campos em componentes personalizados

Ao definir campos no JSON do componente personalizado (para qualquer grupo de campos, básico, validação, ajuda etc.), siga estas práticas recomendadas para manutenção e consistência:

- Reutilizar campos padrão/compartilhados referenciando contêineres ou definições de campo compartilhados existentes (por exemplo, `../form-common/_basic-input-placeholder-fields.json#/fields`, `../form-common/_basic- validation-fields.json#/fields`). Isso garante que você herde todas as opções padrão sem duplicá-las.

- Adicione apenas campos novos ou personalizados explicitamente no container. Isso mantém seu esquema seco e focado.

- Remova ou evite duplicar campos que já estão incluídos por meio de referências. Defina somente os campos que são exclusivos à lógica do componente.

- Consulte contêineres de ajuda e outro conteúdo compartilhado (por exemplo, `../form-common/_help-container.json`) conforme necessário para fins de consistência e manutenção.

>[!TIP]
>
> - Esse padrão facilita a atualização ou a extensão da lógica no futuro e garante que seus componentes personalizados permaneçam consistentes com o restante do sistema de formulários.
> - Sempre verifique se há contêineres compartilhados ou definições de campo existentes antes de adicionar novos.

### Definição de novas propriedades para componentes personalizados

- Se você precisar capturar novas propriedades para o componente personalizado de autores, isso pode ser feito definindo um campo na matriz `fields[]` do componente no JSON do componente.

- O componente personalizado é identificado usando a propriedade :type, que pode ser definida como `fd:viewType` no arquivo JSON (por exemplo, `fd:viewType: cards`). Isso permite que o sistema reconheça e carregue o componente personalizado correto e, portanto, isso é obrigatório para componentes personalizados

- Quaisquer novas propriedades adicionadas na definição JSON estarão disponíveis na definição do campo como propriedades. `<propertyName>` na lógica JS do seu componente

## API JavaScript do componente personalizado

A API JavaScript do componente personalizado define como controlar o comportamento, a aparência e a reatividade do componente de formulário personalizado.

### Função Decorate

A função **decorar** é o ponto de entrada para o componente personalizado. Ele inicializa o componente, vincula-o à definição JSON e permite manipular a estrutura e o comportamento do HTML.

>[!NOTE]
>
> O arquivo JavaScript do componente personalizado deve exportar uma função padrão como decorar:

#### Assinatura da Função:

```javascript
export default function decorate(element, fieldJson, container, formId) 
{
  // element: The HTML structure of the OOTB component you are extending
  // fieldJson: The JSON field definition (all authorable properties)
  // container: The parent element (fieldset or form)
  // formId: The id of the form

  // ... your logic here ...
}
```

Ele pode:

- **Modifique o elemento**: adicione ouvintes de eventos, atualize atributos ou insira marcação adicional.

- **Acessar propriedades JSON**: use `fd.properties.<propertyName>` para ler valores definidos no esquema JSON e aplicá-los na lógica do componente.

## Função Subscribe

A função **assinar** permite que seu componente reaja a alterações nos valores de campo ou eventos personalizados. Isso garante que o componente permaneça sincronizado com o modelo de dados do formulário e possa atualizar dinamicamente sua interface.

### Assinatura da Função:

```javascript
import { subscribe } from '../../rules/index.js';
export default function decorate(fieldDiv, fieldJson, container, formId) {
  // Access custom properties defined in the JSON
  const { initialText, finalText, time } = fieldJson?.properties;

  // ... setup logic ...

  subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => {
    fieldModel.subscribe(() => {
      // React to custom event (e.g., resetCardOption)
      // ... logic ...
    }, 'resetCardOption');
  });
}
```

Ele pode:

- **Registrar um retorno de chamada**: Chamar **subscribe(element, formId, callback)** registra seu retorno de chamada para ser executado sempre que os dados do campo forem alterados. Use dois parâmetros de retorno de chamada:
   - **element**: o elemento HTML que representa o campo.
   - **fieldModel**: o objeto que representa o estado do campo e as APIs de evento.

- **Ouvir alterações ou eventos**: use `fieldModel.subscribe((event) => { ... }, 'eventName')` para executar a lógica sempre que um valor for alterado ou um evento personalizado for acionado. O objeto de evento contém detalhes sobre o que foi alterado.

## Criação de um componente personalizado

Nesta seção, você aprenderá o processo de criação de um **componente personalizado de cartões** estendendo o componente de botão de opção OOTB.

![Componente personalizado do cartão](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. Configuração do código

#### 1.1 Arquivos e pastas

A primeira etapa é configurar os arquivos necessários do componente personalizado e conectá-lo ao código no repositório. Este processo é executado automaticamente pela **CLI do AEM Forms Scaffolder**, o que torna mais rápido o scaffold e a conexão dos arquivos necessários.

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. Abra o terminal e navegue até a raiz do projeto de formulário.
2. Execute os seguintes comandos:

```bash
npm install
npm run create:custom-component
```

![CLI de Scaffolder](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

Ele irá:

- **Solicitar que você nomeie** seu novo componente. Por exemplo, nesse caso, use cartões.
- **Pedir que você escolha** um componente básico (selecionar grupo de opções)

Isso cria todas as pastas e arquivos necessários, incluindo:

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

E a conecta com o restante do código no repositório, conforme mostrado na saída da CLI.
Ele executa as funcionalidades abaixo automaticamente:

- Adiciona cartões aos filtros para permitir a adição no Bloco de formulário adaptável.
- Atualiza a inclui na lista de permissões de `mappings.js` para incluir o novo componente de cartões.
- Registra a definição do componente de cartões na listagem **Componentes personalizados** no Universal Editor.

>[!NOTE]
>
> Você também pode criar um componente personalizado usando o método manual (herdado). Consulte o [Método Manual ou Herdado](#manual-or-legacy-method-to-create-custom-component) para criar a seção de componente personalizado para obter detalhes.

#### 1.2 Uso do componente no editor universal

1. **Atualizar o Editor Universal**: abra o formulário no Editor Universal e atualize a página para garantir que ele carregue o código mais recente do repositório.

2. **Adicionar o componente personalizado**

   1. Clique no botão **Adicionar (+)** na tela de formulário.
   2. Role até a seção Componentes personalizados.
   3. Selecione o **componente de Cartões** recém-criado para inseri-lo em seu formulário.

      ![Selecionar componente personalizado](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

Como nenhum código está presente em `cards.js`, o componente personalizado é renderizado como um grupo de opções.

#### 1.3 Pré-visualizar e testar localmente

Agora que o formulário contém o componente personalizado, é possível intermediar o formulário por proxy e fazer alterações nele localmente e ver as alterações:

1. Vá para o terminal e execute o `aem up`.

2. Abrir o servidor proxy iniciado em `http://localhost:3000/{path-to-your-form}` (exemplo de caminho: `/content/forms/af/custom-component-form`)


### &#x200B;2. Implementação de comportamento personalizado para seu componente personalizado

#### 2.1 Criação do estilo do componente personalizado

Vamos adicionar um **cartão** de classe ao componente para estilo e adicionar uma imagem para cada rádio. Use o código abaixo para isso.

**Estilo do componente usando card.js**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => {
    const image = createOptimizedPicture(
      'https://main--afb--jalagari.hlx.live/lab/images/card.png',
      'card-image'
    );
    radioWrapper.appendChild(image);
  });

  return element;
}
```

**Adicionar Comportamento de Tempo de Execução usando cards.css**

```javascript
.card .radio-wrapper {
  min-width: 320px; /* or whatever width fits your design */
  max-width: 340px;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  flex: 0 0 auto;
  scroll-snap-align: start;
  padding: 24px 16px;
  margin-bottom: 0;
  position: relative;
  transition: box-shadow 0.2s;
  display: flex;
  align-items: flex-start;
  gap: 12px;
}
```

Agora, o componente de cartões é exibido assim:

![adicionar cartão css e js](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 Adição de Comportamento Dinâmico usando a Função Subscribe

Quando a lista suspensa é alterada, as placas são buscadas e definidas na enumeração do grupo de opções. Mas atualmente a visualização não lida com isso. Assim, ele é renderizado conforme mostrado abaixo:

![função de assinatura](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

Quando a API é chamada, ela define o modelo do campo e deve acompanhar as alterações e renderizar a exibição de acordo. Isso é feito usando a **função de assinatura**.

Vamos converter o código de exibição da etapa anterior em uma função e chamá-lo dentro da função de inscrição em `cards.js` conforme mostrado abaixo:

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';
import { subscribe } from '../../rules/index.js';

function createCard(element, enums) {
  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {
    if (enums[index]?.name) {
      let label = radioWrapper.querySelector('label');

      if (!label) {
        label = document.createElement('label');
        radioWrapper.appendChild(label);
      }

      label.textContent = enums[index]?.name;
    }

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

    radioWrapper.appendChild(image);
  });
}

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');
  createCard(element, fieldJson.enum);

  subscribe(element, formId, (fieldDiv, fieldModel) => {
    fieldModel.subscribe((e) => {
      const { payload } = e;

      payload?.changes?.forEach((change) => {
        if (change?.propertyName === 'enum') {
          createCard(element, change.currentValue);
        }
      });
    });
  });

  return element;
}
```

**Usar a função de assinatura para escutar as alterações do evento em cards.js**

Agora, ao alterar a lista suspensa, os cartões são preenchidos conforme mostrado abaixo:

![função de assinatura](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 Sincronização de atualizações de exibição com o modelo de campo

Para sincronizar as alterações de exibição com o Modelo de campo, você deve definir o valor do cartão selecionado. Portanto, adicione o seguinte ouvinte de eventos de alteração no cards.js, como mostrado abaixo:

**Usando a API do modelo de campo em cards.js**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';
import { subscribe } from '../../rules/index.js';

function createCard(element, enums) {
  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {
    if (enums[index]?.name) {
      let label = radioWrapper.querySelector('label');

      if (!label) {
        label = document.createElement('label');
        radioWrapper.appendChild(label);
      }

      label.textContent = enums[index]?.name;
    }

    // Attach index to input element for later reference
    radioWrapper.querySelector('input').dataset.index = index;

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

    radioWrapper.appendChild(image);
  });
}

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');
  createCard(element, fieldJson.enum);

  subscribe(element, formId, (fieldDiv, fieldModel) => {
    fieldModel.subscribe((e) => {
      const { payload } = e;

      payload?.changes?.forEach((change) => {
        if (change?.propertyName === 'enum') {
          createCard(element, change.currentValue);
        }
      });
    });

    element.addEventListener('change', (e) => {
      e.stopPropagation();
      const value = fieldModel.enum?.[parseInt(e.target.dataset.index, 10)];
      fieldModel.value = value.name;
    });
  });

  return element;
}
```

Agora, o componente de cartão personalizado aparece, como mostrado abaixo:

![Componente personalizado do cartão](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;3. Confirmar e enviar alterações

Depois de implementar o JavaScript e o CSS para o componente personalizado e verificá-los localmente, confirme e envie as alterações para o repositório Git.

```bash
git add . && git commit -m "Add card custom component" && git push
```

Você criou com sucesso um componente complexo de seleção de cartão personalizado em algumas etapas simples.

+++ **Método Manual ou Herdado para Criar Componente Personalizado**

A maneira herdada de fazer isso é seguir manualmente as etapas descritas abaixo:

1. **Escolha um componente OOTB** para estender (por exemplo, botão, lista suspensa, entrada de texto etc.). Nesse caso, estenda o componente de rádio.

2. **Crie uma pasta** em `blocks/form/components` com o nome do seu componente (cartões, neste caso).

3. **Adicionar um arquivo JS** com o mesmo nome:
   - `blocks/form/components/cards/cards.js`.

4. (Opcional) **Adicionar um arquivo CSS** para estilos personalizados:
   - `blocks/form/components/cards/cards.css.`

5. **Defina um novo arquivo JSON** (por exemplo,` _cards.json`) na mesma pasta que seu **arquivo JS componente** (`blocks/form/components/cards/_cards.json`). Este JSON deve estender um componente existente e, em suas definições, definir `fd:viewType` como o nome do seu componente (cartões, neste caso):

   - Para todos os grupos de campos (básico, validação, ajuda etc.), adicione seus campos personalizados explicitamente.

6. **Implemente a lógica JS e CSS:**
   - Exporte uma função padrão conforme descrito acima.
   - Use o parâmetro **element** para modificar a estrutura base do HTML.
   - Use o parâmetro **fieldJson** se necessário para dados de campo padrão.
   - Use a função **assinar** para ouvir alterações de campo ou eventos personalizados, se necessário.

     >[!NOTE]
     >
     >Implemente a lógica JS e CSS para seu componente personalizado, conforme explicado acima.

7. Registre seu componente como uma variante no construtor de formulários e defina a propriedade de variante ou
   `fd:viewType/:type` no JSON para o nome do seu componente, por exemplo, adicione o valor `fd:viewType` de `definitions[]` como cartões à matriz de componentes do objeto com `id="form`.

   ```
       {
     "definitions": [
       {
         "title": "Cards",
         "id": "cards",
         "plugins": {
           "xwalk": {
             "page": {
               "resourceType": "core/fd/components/form/radiobutton/v1/radiobutton",
               "template": {
                 "jcr:title": "Cards",
                 "fieldType": "radio-button",
                 "fd:viewType": "cards",
                 "enabled": true,
                 "visible": true
               }
             }
           }
         }
       }
     ]
   }
   ```

8. **Atualizar mappings.js**: adicione o nome do seu componente à lista **OOTBComponentDecorators** (para componentes de estilo OOTB) ou **customComponents** para que ele seja reconhecido e carregado pelo sistema.

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **Atualizar _form.json**: adicione o nome de seu componente à matriz `filters.components` para que ele possa ser descartado na interface de criação.

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **Atualizar _component-definition.json**: em `models/_component-definition.json`, atualize a matriz no grupo com `id custom-components` com um objeto da seguinte maneira:

    ```javascript
    {
    "...":"../blocks/form/components/cards/_cards.json#/definitions"
    }
    ```

    Isso fornece a referência para o novo componente de placas a ser construído com o restante dos componentes

11. **Execute o script de compilação:json**: Execute `npm run build:json` para compilar e mesclar todas as definições de JSON de componente em um único arquivo a ser fornecido pelo servidor. Isso garante que o esquema do novo componente seja incluído na saída mesclada.

12. Confirme e envie as alterações para o repositório Git.

Agora, você pode adicionar o componente personalizado ao formulário.

+++

## Criar um componente composto

Um componente composto é criado ao combinar vários componentes.
Por exemplo, um componente composto dos Termos e condições consiste em um painel principal que contém:

- Um campo de texto simples para exibir os termos

- Uma caixa de seleção para capturar o contrato do usuário

Essa estrutura de composição é definida como um modelo dentro do arquivo JSON do respectivo componente. O exemplo a seguir mostra como definir um modelo para um componente dos Termos e Condições:

```javascript
{
  "definitions": [
    {
      "title": "Terms and conditions",
      "id": "tnc",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/termsandconditions/v1/termsandconditions",
            "template": {
              "jcr:title": "Terms and conditions",
              "fieldType": "panel",
              "fd:viewType": "tnc",
              "text": {
                "value": "Text related to the terms and conditions come here.",
                "sling:resourceType": "core/fd/components/form/text/v1/text",
                "fieldType": "plain-text",
                "textIsRich": true
              },
              "approvalcheckbox": {
                "name": "approvalcheckbox",
                "jcr:title": "I agree to the terms & conditions.",
                "sling:resourceType": "core/fd/components/form/checkbox/v1/checkbox",
                "fieldType": "checkbox",
                "required": true,
                "type": "string",
                "enum": [
                  "true"
                ]
              }
            }
          }
        }
      }
    }
  ],
  ...
}
```

## Práticas recomendadas

Lembre-se dos pontos abaixo antes de criar seu próprio componente personalizado:

- **Mantenha a lógica do componente focada**: adicione/substitua somente o que é necessário para o seu comportamento personalizado

- **Aproveite a estrutura base**: use o HTML OOTB como ponto de partida

- **Usar propriedades que podem ser criadas:** Exponha as opções configuráveis por meio do esquema JSON

- **Namespace do CSS**: evite colisões de estilos usando nomes de classe exclusivos

## Referências

- [tipos de campo de formulário](/help/edge/docs/forms/eds-form-field-properties.md): estruturas e propriedades de base do HTML para todos os tipos de campo.

- **blocos/formulário/modelos/formulário-components**: OOTB e definições de propriedades de componentes personalizados.

- **blocos/formulário/componentes**: coloque seus componentes personalizados. Por exemplo: `blocks/form/components/countdown-timer/_countdown-timer.json` mostra como estender um componente base e adicionar novas propriedades.
