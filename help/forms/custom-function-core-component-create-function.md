---
title: Criar e adicionar funções personalizadas em um Formulário adaptável
description: O AEM Forms é compatível com funções personalizadas, que permitem aos usuários criar e usar suas próprias funções no editor de regras.
keywords: Adicionar uma função personalizada, usar uma função personalizada, criar uma função personalizada, usar a função personalizada no editor de regras.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: e7ab4233-2e91-45c6-9377-0c9204d03ee9
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Criar uma função personalizada para um formulário adaptável com base nos Componentes principais

O Forms adaptável baseado em Componentes principais oferece experiências dinâmicas de usuário, ajustando o conteúdo e o comportamento com base na entrada do usuário. As funções personalizadas permitem que os desenvolvedores estendam a funcionalidade, garantindo que os formulários possam atender a requisitos específicos. Ao integrar funções personalizadas, os desenvolvedores podem implementar lógica complexa, automatizar processos e introduzir interações exclusivas que se alinham a requisitos de negócios específicos ou expectativas do usuário. Garante que os formulários não só se adaptem a condições variáveis, mas também forneçam uma solução mais precisa e eficaz para casos de uso diversos.
Este artigo orienta você pelas etapas da criação de funções personalizadas para o Adaptive Forms usando componentes principais.

## Considerações

* O `parameter type` e o `return type` não dão suporte a `None`.

* As funções não suportadas na lista de funções personalizadas são:
   * Funções geradoras
   * Funções assíncronas/Await
   * Definições de método
   * Métodos de classe
   * Parâmetros padrão
   * Parâmetros rest

* Os recursos mais recentes do ECMAScript estão disponíveis como Acesso antecipado (EA), enquanto que até o ECMAScript 2019 é compatível com a disponibilidade geral.

## Pré-requisitos para criar uma função personalizada

Antes de começar a adicionar uma função personalizada ao Adaptive Forms, verifique se você tem o seguinte:

**Software:**

* **Editor de Texto sem Formatação (IDE)**: embora qualquer editor de texto sem formatação possa funcionar, um IDE (Ambiente de Desenvolvimento Integrado) como o Microsoft Visual Studio Code oferece recursos avançados para facilitar a edição.

* **Git:** este sistema de controle de versão é necessário para gerenciar alterações de código. Se não estiver instalado, baixe-o de https://git-scm.com.


## Criar uma função personalizada

Crie uma biblioteca do cliente para chamar funções personalizadas no editor de regras. Para obter mais informações, consulte [Usando bibliotecas do lado do cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=pt-BR#developing).

As etapas para criar funções personalizadas são:

1. [Criar uma biblioteca do cliente](#create-client-library)
1. [Adicionar a biblioteca do cliente a um Formulário adaptável](#use-custom-function)

### Criar uma biblioteca do cliente {#create-client-library}

É possível adicionar funções personalizadas adicionando uma biblioteca do cliente. Para criar uma biblioteca do cliente, execute as seguintes etapas:

**Clonar o Repositório**

Clonar seu [Repositório as a Cloud Service do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=pt-BR#accessing-git):

1. Abra a linha de comando ou a janela do terminal.

1. Navegue até o local desejado na máquina em que deseja armazenar o repositório.

1. Execute o seguinte comando para clonar o repositório:

   `git clone [Git Repository URL]`

Este comando faz o download do repositório e cria uma pasta local do repositório clonado no computador. Neste guia, nos referimos a essa pasta como o [diretório do projeto AEMaaCS].

**Adicionar uma pasta da biblioteca do cliente**

Para adicionar uma nova pasta da biblioteca do cliente ao [diretório do projeto AEMaaCS], siga estas etapas:

1. Abra o [diretório do projeto AEMaaCS] em um editor.

   ![estrutura de pasta de função personalizada](/help/forms/assets/custom-library-folder-structure.png)

1. Localizar `ui.apps`.
1. Adicionar nova pasta. Por exemplo, adicione uma pasta chamada `experience-league`.
1. Navegue até a pasta `/experience-league/` e adicione um `ClientLibraryFolder`. Por exemplo, crie uma pasta da biblioteca do cliente chamada `customclientlibs`.

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Adicionar arquivos e pastas à pasta da Biblioteca do Cliente**

Adicione o seguinte à pasta da biblioteca do cliente adicionada:

* arquivo .content.xml
* arquivo js.txt
* pasta js

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. Em `.content.xml`, adicione as seguintes linhas de código:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Você pode escolher qualquer nome para a propriedade `client library folder` e `categories`.

1. Em `js.txt`, adicione as seguintes linhas de código:

   ```javascript
         #base=js
       function.js
   ```

1. Na pasta `js`, adicione o arquivo javascript como `function.js`, o que inclui as funções personalizadas:

   ```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */
   
    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();
   
    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();
   
    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }
   
    return age;
    }
   ```

1. Salve os arquivos.

![estrutura de pasta de função personalizada](/help/forms/assets/custom-function-added-files.png)

**Incluir a nova pasta no filter.xml**:

1. Navegue até o arquivo `/ui.apps/src/main/content/META-INF/vault/filter.xml` no seu [diretório do projeto AEMaaCS].

2. Abra o arquivo e adicione a seguinte linha no final:

   `<filter root="/apps/experience-league" />`
3. Salve o arquivo.

![xml de filtro de função personalizada](/help/forms/assets/custom-function-filterxml.png)

**Implante a pasta da biblioteca do cliente recém-criada no seu ambiente AEM**

Implante o AEM as a Cloud Service, [diretório do projeto AEMaaCS], no seu ambiente Cloud Service. Para implantar no ambiente do Cloud Service:

1. Confirmar as alterações

   1. Adicione, confirme e envie as alterações no repositório usando os comandos abaixo:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Implante o código atualizado:

   1. Acione uma implantação do seu código por meio do pipeline de pilha completa existente. Isso cria e implanta automaticamente o código atualizado.

Se você ainda não tiver configurado um pipeline, consulte o manual sobre [como configurar um pipeline para o AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=pt-BR#setup-pipeline).

Depois que o pipeline for executado com êxito, a função personalizada adicionada à biblioteca do cliente ficará disponível em seu [editor de regras de Formulário adaptável](/help/forms/rule-editor-core-components.md).

### Adicionar a biblioteca do cliente a um Formulário adaptável{#use-custom-function}

Depois de implantar a biblioteca do cliente no ambiente do Forms CS, use os recursos dela no Formulário adaptável. Para adicionar a biblioteca do cliente no Formulário adaptável

1. Abra o formulário no modo de edição. Para abrir um formulário no modo de edição, selecione um formulário e selecione **[!UICONTROL Editar]**.
1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Básico]** e selecione o nome da **[!UICONTROL categoria da biblioteca do cliente]** na lista suspensa (neste caso, selecione `customfunctionscategory`).

   ![Adicionando a biblioteca cliente de função personalizada](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > É possível adicionar várias categorias especificando uma lista separada por vírgulas no campo **[!UICONTROL Categoria da biblioteca do cliente]**.

1. Clique em **[!UICONTROL Concluído]**.

Você pode usar a função personalizada no [editor de regras de um Formulário Adaptável](/help/forms/rule-editor-core-components.md) usando as [anotações do JavaScript](##js-annotations).

## Uso de uma função personalizada em um Formulário adaptável

Em um Formulário adaptável, você pode usar [funções personalizadas no editor de regras](/help/forms/rule-editor-core-components.md). Vamos adicionar o seguinte código ao arquivo JavaScript (arquivo `Function.js`) para calcular a idade com base na Data de Nascimento (AAAA-MM-DD). Crie uma função personalizada como `calculateAge()` que use a data de nascimento como entrada e retorne a idade:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

No exemplo acima, quando o usuário insere a data de nascimento no formato (AAAA-MM-DD), a função personalizada `calculateAge` é invocada e retorna a idade.

![Função personalizada Calcular Idade no Editor de Regras](/help/forms/assets/custom-function-calculate-age.png)

Vamos visualizar o formulário para observar como as funções personalizadas são implementadas por meio do editor de regras:

![Função personalizada Calcular Idade na Visualização de Formulário do Editor de Regras](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Você pode consultar a seguinte pasta [função personalizada](/help/forms/assets//customfunctions.zip). Baixe e instale esta pasta na instância do AEM usando o [Gerenciador de Pacotes](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

## Recursos de funções personalizadas

As funções personalizadas nos formulários do AEM oferecem uma solução robusta para estender e personalizar a funcionalidade de seus formulários. Você pode usar as funções personalizadas para atender às necessidades específicas da sua organização.

Essas funções oferecem suporte a várias funcionalidades, incluindo o trabalho com campos específicos, o uso de campos globais e operações assíncronas, além de incorporar mecanismos de armazenamento em cache. Essa flexibilidade garante que os formulários possam se adaptar a requisitos complexos e fornecer uma experiência do usuário eficiente e personalizada. Ao aproveitar esses recursos avançados, é possível aprimorar as interações de formulários e otimizar o desempenho, tornando os formulários do AEM mais funcionais e ágeis.

Vamos analisar os recursos de funções personalizadas.

### Suporte assíncrono em funções personalizadas {#support-of-async-functions}

Você pode implementar funções assíncronas no editor de regras usando funções personalizadas. Para obter orientação sobre como fazer isso, consulte o artigo [Uso de funções assíncronas em um Formulário adaptável](/help/forms/using-async-funct-in-rule-editor.md).

### Suporte a objetos de escopo de campo e global em funções personalizadas {#support-field-and-global-objects}

Os objetos Field referem-se aos componentes ou elementos individuais em um formulário, como campos de texto e caixas de seleção. O objeto Globals contém variáveis somente leitura, como instância de formulário, instância de campo de destino e métodos para fazer modificações de formulário em funções personalizadas.

>[!NOTE]
>
> O `param {scope} globals` deve ser o último parâmetro e não é exibido no editor de regras de um Formulário adaptável.

Para obter mais informações sobre objetos de escopo, consulte o artigo [Objetos de escopo em funções personalizadas](/help/forms/custom-function-core-component-scope-function.md).

### Suporte de cache na função personalizada

O Forms adaptável implementa o armazenamento em cache de funções personalizadas para melhorar o tempo de resposta ao recuperar a lista de funções personalizadas no editor de regras. Uma mensagem como `Fetched following custom functions list from cache` aparece no arquivo `error.log`.

![função personalizada com suporte a cache](/help/forms/assets/custom-function-cache-error.png)

Caso as funções personalizadas sejam modificadas, o armazenamento em cache é invalidado e é analisado.

## Resolução de problemas

* Se o arquivo JavaScript que contém o código para funções personalizadas tiver um erro, as funções personalizadas não serão listadas no editor de regras de um Formulário adaptável. Para verificar a lista de funções personalizadas, você pode navegar até o arquivo `error.log` para localizar o erro. No caso de um erro, a lista de funções personalizadas aparece vazia:

  ![arquivo de log de erros](/help/forms/assets/custom-function-list-error-file.png)

  Caso não haja erro, as funções personalizadas são buscadas e aparecem no arquivo `error.log`. Uma mensagem como `Fetched following custom functions list` aparece no arquivo `error.log`:

  ![arquivo de log de erros com a função personalizada adequada](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Próxima etapa

Vamos ver vários [exemplos de funções personalizadas para um Formulário adaptável com base nos Componentes principais](/help/forms/custom-function-core-components-use-cases.md).

## Consulte também

{{see-also-rule-editor}}
