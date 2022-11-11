---
title: Introdução à criação do Adaptive Forms
seo-title: Introduction to authoring Adaptive Forms
description: O AEM Forms fornece uma interface fácil de usar, mas eficiente, para a criação do Adaptive Forms. Ele fornece vários componentes e ferramentas que podem ser usadas para criar formulários.
seo-description: AEM Forms provide easy-to-use yet powerful interface for authoring Adaptive Forms. It provides a host of components and tools that you can use to build forms.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
topic-tags: author, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
source-git-commit: 434071de17d6ff56ede561735f7214d96f98cfa0
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 4%

---


# Editor adaptável Forms {#introduction-to-authoring-adaptive-forms}

## Visão geral {#overview}

O Adaptive Forms permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. [!DNL AEM Forms] O oferece uma interface de usuário intuitiva e componentes prontos para uso para criar e trabalhar com o Adaptive Forms. É possível optar por criar um formulário adaptável com base em um modelo ou esquema de formulário ou sem um modelo de formulário. É importante escolher cuidadosamente o modelo de formulário que atende não apenas às suas necessidades, mas estende os investimentos e ativos existentes em infraestrutura. Você pode escolher entre as seguintes opções para criar um formulário adaptável:

* **Uso de um modelo de dados de formulário**
   [Integração de dados](data-integration.md) O permite integrar entidades e serviços de diferentes fontes de dados em um Modelo de dados de formulário que pode ser usado para criar o Adaptive Forms. Escolha Modelo de dados de formulário se o Formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.

* **Uso de um modelo de formulário XDP**
É um modelo de formulário ideal se você tiver investimentos em formulários XFA ou XDP. Ele fornece uma maneira direta de converter formulários baseados em XFA em Adaptive Forms. Quaisquer regras XFA existentes são retidas no Adaptive Forms associado. O Adaptive Forms resultante oferece suporte a construções XFA, como validações, eventos, propriedades e padrões.

* **Usando uma Definição de Esquema XML (XSD) ou um Esquema JSON**
Os esquemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na organização. Você pode associar o esquema a um Formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao Formulário adaptável. Os elementos do esquema estarão disponíveis para uso na guia Objetos do modelo de dados do navegador Conteúdo ao criar o Adaptive Forms.

* **Uso de um modelo de formulário nenhum ou sem**
O Adaptive Forms criado com essa opção não usa nenhum modelo de formulário. O XML de dados gerado desses formulários tem uma estrutura simples com campos e valores correspondentes.

   >[!NOTE]
   >
   > É possível modificar as propriedades do modelo de formulário no editor de formulário adaptável ou no editor de modelo de formulário adaptável. Para obter mais informações, consulte [Editar as propriedades do Modelo de formulário de um formulário adaptável](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model).

Para criar um formulário adaptável, consulte [Criação de um formulário adaptável](creating-adaptive-form.md).

## Interface do usuário de criação de formulário adaptável {#adaptive-form-authoring-ui}

A interface otimizada para toque para a criação do Adaptive Forms é intuitiva e oferece:

* Funcionalidade de arrastar e soltar
* Componentes de formulário padrão
* Repositório integrado de ativos

Ao criar um formulário adaptável novo ou editar um formulário existente, você usa os seguintes elementos da interface do usuário:

* [Barra lateral](#sidebar)
* [Barra de ferramentas da página](#page-toolbar)
* [Barra de ferramentas Componente](#component-toolbar)
* [Página de formulário adaptável](#af-page)

<!-- ![Adaptive Form authoring UI](assets/formeditor.png)

**A.** Sidebar **B.** Page toolbar **C.** Adaptive Form page -->

### Barra lateral {#sidebar}

A barra lateral permite

* Pesquise, visualize e use ativos no repositório do Gerenciamento de ativos digitais do AEM (DAM).
* Consulte o conteúdo do formulário, como painéis, componentes, campos e layout.
* Adicione componentes ao formulário.
* Editar propriedades de componentes.

![Barra lateral](assets/sidebar-comps.png)

**A.** Navegador de conteúdo **B.** Navegador de propriedades **C.** Navegador de ativos **D.** Navegador de componentes

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

A barra lateral inclui os seguintes navegadores:

* **Navegador de conteúdo**
No navegador de conteúdo, é possível ver:

   * **Objetos de formulário**
Mostra a hierarquia de objetos do Formulário. O autor pode navegar até um componente de formulário específico tocando nesse elemento na Árvore de objetos de formulário. O autor pode pesquisar objetos e reorganizá-los a partir dessa árvore.

   * **Objetos do modelo de dados**
Permite ver a hierarquia do modelo de formulário.
Ela permite arrastar e soltar elementos do modelo de formulário no Formulário adaptável. Os elementos adicionados são convertidos automaticamente em componentes de formulário, mantendo suas propriedades originais. É possível ver objetos de modelo de dados quando o formulário usa esquema XML, esquema JSON ou modelo XDP.

* **Navegador de propriedades**

   Permite editar as propriedades de um componente. As propriedades mudam de acordo com um componente. Para ver as propriedades do contêiner do Formulário adaptável:

   Selecione um componente e toque em ![nível de campo](assets/Smock_SelectContainer_18_N.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e toque em ![propriedades](assets/Smock_Wrench_18_N.svg).

* **Navegador de ativos**

   Segmenta diferentes tipos de conteúdo, como imagens, documentos, páginas, filmes e assim por diante.

* **Navegador de componentes**

   Inclui componentes que podem ser usados para criar um formulário adaptável. Você pode arrastar os componentes do para o Formulário adaptável para adicionar elementos de formulário e configurar o elemento adicionado de acordo com os requisitos. A tabela a seguir descreve os componentes listados no navegador de componentes.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funcionalidade</strong></th>
  </tr>
  <tr>
   <td>Bloco do Adobe Sign</td>
   <td>Adiciona um bloco de texto com espaços reservados para os campos a serem preenchidos ao assinar usando o Adobe Sign.</td>
  </tr>
  <tr>
   <td>Botão</td>
   <td>Adiciona um botão, que pode ser configurado para executar ações, como salvar, redefinir, seguir, anterior e assim por diante.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Adiciona a validação CAPTCHA usando o serviço Google reCAPTCHA.</td>
  </tr>
  <tr>
   <td>Gráfico</td>
   <td>Adiciona um gráfico que pode ser usado no Adaptive Forms e em documentos para representação visual de dados bidimensionais em painéis repetitivos e linhas de tabela.</td>
  </tr>
  <tr>
   <td>Caixa de seleção</td>
   <td>Adiciona uma caixa de seleção.</td>
  </tr>
  <tr>
   <td>Campo de Entrada de Data</td>
   <td>Use o componente Campo de entrada de data em seu formulário, para permitir que os clientes preencham dia, mês e ano separadamente em três caixas. Você pode personalizar a aparência do componente e alterar o formato de data. Por exemplo, você pode permitir que seus clientes insiram datas no formato MM/DD/AAAA ou DD/MM/AAAA.</td>
  </tr>
  <tr>
   <td>Seletor de data</td>
   <td>Adiciona um campo de calendário para selecionar uma data.</td>
  </tr>
  <tr>
   <td>Fragmento do documento</td>
   <td>Permite adicionar componentes reutilizáveis de uma correspondência.</td>
  </tr>
  <tr>
   <td>Grupo de fragmento de documento</td>
   <td>Permite adicionar um grupo de fragmentos de documento relacionados que você pode usar em um modelo de carta como uma única unidade.</td>
  </tr>
  <tr>
   <td>Lista suspensa</td>
   <td>Adiciona uma lista suspensa - seleção única ou múltipla</td>
  </tr>
  <tr>
   <td>Email</td>
   <td><p>Adiciona um campo para capturar o endereço de email. O componente Email, por padrão, valida endereços de email usando a seguinte expressão regular.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Anexo de arquivo</td>
   <td><p>Adiciona um botão que permite aos usuários navegar e anexar documentos de suporte a um formulário.</p> <p><strong>Observação: </strong>O componente de anexo de arquivo oferece suporte a um conjunto predefinido de formatos de arquivo no Adaptive Forms habilitado para Adobe Sign. Para obter mais informações, consulte <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formatos de arquivo compatíveis</a>.</p> </td>
  </tr>
  <tr>
   <td>Lista de anexos de arquivo</td>
   <td>Adiciona um campo que lista todos os anexos carregados usando o componente Anexo de arquivo.</td>
  </tr>
  <tr>
   <td>Rodapé<br /> </td>
   <td>Adiciona o cabeçalho da página que normalmente inclui o logotipo de uma corporação, o título do formulário e o resumo.<br /> </td>
  </tr>
  <tr>
   <td>Cabeçalho</td>
   <td>Adiciona o rodapé da página que normalmente inclui informações de direitos autorais e links para outras páginas. </td>
  </tr>
  <tr>
   <td>Imagem</td>
   <td>Permite inserir uma imagem.</td>
  </tr>
  <tr>
   <td>Opção de Imagem</td>
   <td>Permite que seus clientes selecionem uma imagem para fornecer informações. Você pode usar as informações para fornecer serviços personalizados aos clientes.</td>
  </tr>
  <tr>
   <td>Próximo botão</td>
   <td>Adiciona um botão para navegar até o próximo painel em um formulário.</td>
  </tr>
  <tr>
   <td>Caixa numérica</td>
   <td>Adiciona um campo para capturar valores numéricos</td>
  </tr>
  <tr>
   <td>Escalonador Numérico</td>
   <td>Use o Numeric Stepper em seu formulário para permitir que seus clientes insiram um valor numérico, que pode aumentar ou diminuir com base em uma etapa predefinida.</td>
  </tr>
  <tr>
   <td>Painel</td>
   <td><p>Adiciona um painel ou subpainel.</p> <p>Você também pode adicionar um componente de painel na barra de ferramentas do painel principal usando o <span class="uicontrol">Adicionar painel filho</code> botão. Da mesma forma, é possível adicionar uma barra de ferramentas específica do painel usando o <span class="uicontrol">Adicionar barra de ferramentas do painel</code> botão. É possível configurar a posição da barra de ferramentas do painel usando a caixa de diálogo Editar painel .</code></code></p> </td>
  </tr>
  <tr>
   <td>Caixa de senha</td>
   <td>Adiciona um campo para capturar uma senha.</td>
  </tr>
  <tr>
   <td>Botão Anterior</td>
   <td>Adiciona um botão que os usuários precisam para retornar à página ou ao painel anterior.</td>
  </tr>
  <tr>
   <td>Botão de opção</td>
   <td>Adiciona botões de opção.</td>
  </tr>
  <tr>
   <td>Botão de redefinição</td>
   <td>Adiciona um botão para redefinir campos de formulário.</td>
  </tr>
  <tr>
   <td>Botão salvar</td>
   <td>Adiciona um botão para salvar os dados do formulário.</td>
  </tr>
  <tr>
   <td>Assinatura</td>
   <td>Adiciona um campo para capturar assinaturas do rabisco.</td>
  </tr>
  <tr>
   <td>Separador</td>
   <td>Permite a segregação visual de painéis em seu formulário.</td>
  </tr>
  <tr>
   <td>Etapa de assinatura</td>
   <td>Exibe as informações fornecidas no formulário e os campos de assinatura para o usuário verificar e assinar o formulário.</td>
  </tr>
  <tr>
   <td>Texto</td>
   <td>Permite que você especifique texto estático.</td>
  </tr>
  <tr>
   <td>Botão enviar</td>
   <td>Adiciona um botão Enviar para enviar o formulário para a Ação de envio configurada.</td>
  </tr>
  <tr>
   <td>Etapa de resumo</td>
   <td>Envia o formulário e exibe o texto resumido que os autores especificam após o envio do formulário. </td>
  </tr>
  <tr>
   <td>Alternar</td>
   <td>Adiciona um switch que executa uma ação de alternância ou ativação/desativação. Não é possível adicionar mais de duas opções no componente Switch. Como um switch pode ter apenas dois valores: Ligado ou desligado, não é obrigatório. Pelo menos um valor é salvo independentemente da entrada do usuário. <br /> </td>
  </tr>
  <tr>
   <td>Tabela</td>
   <td>Adiciona uma tabela que permite organizar dados em linhas e colunas. </td>
  </tr>
  <tr>
   <td>Telefone</td>
   <td><p>Adiciona um campo para capturar o número de telefone. O componente Telefone permite que os autores configurem um dos seguintes tipos de número de telefone. Cada tipo está associado a uma expressão regular padrão para validação.</p>
    <ul>
     <li>O Tipo Internacional é validado por <code>^[+][0-9]{0,14}$</code>.</li>
     <li>Tipo USPhoneNumber é validado por <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>O tipo UKPhoneNumber é validado por <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Tipo Personalizado não fornece um padrão de validação padrão. Obtém o valor do último tipo de número de telefone selecionado. Você também pode especificar seu próprio padrão de validação personalizado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Termos e condições<br /> </td>
   <td>Adiciona um campo que os autores podem usar para especificar os termos e condições que os usuários devem revisar antes de preencher o formulário.</td>
  </tr>
  <tr>
   <td>Caixa de texto </td>
   <td><p>Adiciona uma caixa de texto na qual o usuário pode especificar as informações necessárias. </p> <p>Por padrão, o componente Caixa de texto aceita apenas texto sem formatação. Você pode ativar um componente Caixa de texto para aceitar Rich Text. Um componente de texto Rich Text habilitado fornece opções para adicionar cabeçalhos, alterar estilos de caracteres (negrito, itálico, sublinhar os caracteres), criar listas ordenadas e não ordenadas, alterar o plano de fundo do texto e a cor do texto e adicionar hiperlinks. Para ativar o rich text de uma caixa de texto, ative a<strong> Permitir Rich Text</strong> nas propriedades do componente.</p> </td>
  </tr>
  <tr>
   <td>Título</td>
   <td>Especifica um título para o Formulário adaptável.</td>
  </tr>
  <tr>
   <td>Etapa de verificação</td>
   <td><p>Adiciona um espaço reservado para exibir o formulário preenchido para verificação por usuário.</p> <p><strong>Observação</strong>: O formulário adaptável que contém o componente Verificar não suporta usuários anônimos. Além disso, não é recomendado usar o componente Verificar em um Fragmento de formulário adaptável.</p> </td>
  </tr>
 </tbody>
</table>

### Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas da página na parte superior fornece opções que permitem visualizar o formulário, alterar as propriedades do formulário e editar o layout do formulário. É possível visualizar o formulário ao criá-lo e fazer alterações de acordo. Na barra de ferramentas da página, você vê:

* **Alternar painel lateral** ![painel lateral de alternância](assets/Smock_RailLeft_18_N.svg): Permite mostrar ou ocultar a Barra Lateral.

* **Informações da página** ![theme-options](assets/Smock_Properties_18_N.svg): Permite exibir as propriedades da página, publicar/desfazer a publicação de um formulário, iniciar um fluxo de trabalho de formulário e abrir o formulário na interface clássica.

* **Emulador** ![régua](assets/Smock_Devices_18_N.svg): Permite que você emule a aparência de seu formulário para diferentes tamanhos de exibição, como tablets e telefones.

* **Editar**: Permite selecionar outros modos, como: **[!UICONTROL Editar]**, **[!UICONTROL Estilo]**, **[!UICONTROL Desenvolvedor]** e **[!UICONTROL Design]**.

   * **Editar**: Permite editar as propriedades do formulário e seus componentes. Por exemplo, adicionar um componente, soltar uma imagem e especificar campos obrigatórios.
   * **Estilo**: Permite estilizar a aparência dos componentes do formulário. Por exemplo, no modo de estilo, é possível selecionar um painel e especificar a cor do plano de fundo.

   * **Desenvolvedor**: Permite que um desenvolvedor:

      * Descubra de quais formulários são compostos.
      * Depurar o que está acontecendo onde e quando, o que, por sua vez, ajuda a resolver problemas.

      * **Design**. Permite ativar ou desativar componentes personalizados ou componentes prontos para uso que não estejam listados na Barra lateral.

* **Visualizar**: Permite que você visualize a aparência do formulário ao publicá-lo.

### Barra de ferramentas Componente {#component-toolbar}

![Barra de ferramentas do componente na interface de toque](assets/component-toolbar.png)

Ao selecionar um componente, você verá uma barra de ferramentas que permite trabalhar nele. Você tem opções para recortar, colar, mover e especificar as propriedades dos componentes. Suas opções são:

A.**Configurar**: Ao tocar **[!UICONTROL Configurar]**, as propriedades do componente são visíveis na barra lateral. A configuração dessas propriedades permite personalizar a experiência de captura de dados. Você pode alterar o nome do elemento do componente, especificar o texto do rótulo no campo Título do componente. O nome do elemento permite capturar valores inseridos pelos usuários usando o componente. Nas propriedades do componente, especifique o comportamento do componente e gerencie a entrada do usuário. Configure as propriedades na barra lateral para capturar os dados do usuário e usá-los para processamento adicional. As propriedades do contêiner de Formulário adaptável permitem especificar as bibliotecas do cliente, os Layouts, os Temas, as configurações de Documento de registro, salvar configurações, as configurações de envio e as configurações de metadados.

B.**Copiar**: Você pode usar a opção de copiar para copiar um componente e colá-lo em outros lugares do formulário. Quando você cola um componente, o componente colado obtém um novo nome de elemento, mas retém as propriedades do componente copiado.

C.**Recortar**: Você pode usar a opção de recorte para mover um componente de um local para outro no Formulário adaptável.

D. **Excluir**: Permite excluir o componente do formulário.

E. **Inserir**: Permite inserir um componente acima do componente selecionado.

F. **Colar**: Permite colar o componente cortado ou copiado usando as opções descritas acima.

G. **Editar regras**: Permite abrir o editor de regras. Para obter mais informações, <!-- see [Rule Editor](rule-editor.md). -->

H. **Grupo**: Permite selecionar vários componentes se você deseja cortar, copiar ou colar mais de um componente.

I. **Pai**: Permite selecionar o pai de um componente. Por exemplo, um campo de texto está em uma subseção, que fica em uma seção. A seção encontra-se no painel raiz do guia e o contêiner de Formulário adaptável é o pai de um painel raiz do guia. Para um componente, você pode ver todas as opções com a hierarquia inferior classificada.

Por exemplo, se você tocar em **[!UICONTROL Pai]** para uma caixa de texto, é possível ver:

* Subseção
* Seção
* guideRootPanel
* Contêiner de formulário adaptável

J. **Outros**: Fornece mais opções para trabalhar com o componente selecionado.

* Exibir expressão SOM
* Salvar um painel como fragmento (somente para painéis)
* Adicionar painel filho (somente para painéis)
* Adicionar barra de ferramentas do painel (somente para painéis)
* Substituir (não para painéis)

### Página de formulário adaptável {#af-page}

A página Formulário adaptável é o formulário real. É como qualquer outra página WCM modelada como o WCM `cq:Page` componente. A imagem a seguir mostra a estrutura de conteúdo de um formulário adaptável típico.

![Estrutura de conteúdo de uma página WCM de formulário adaptável](assets/afstructure.png)

A estrutura de conteúdo normalmente contém os seguintes componentes principais:

* **guideContainer**: A raiz de um formulário adaptável, que é marcado como **[!UICONTROL Início do formulário adaptável]** na interface do usuário do formulário adaptável. Nesse componente, você pode especificar:

   * *Layout móvel do formulário adaptável*: Define a aparência do formulário em dispositivos móveis.
   * *Página de agradecimento*: Define a página para a qual o usuário é redirecionado após enviar o formulário.
   * *Enviar ação*: Define como o formulário é processado no servidor depois que o usuário envia o formulário.
   * *Estilo*: Especifica o caminho para o arquivo CSS usado para personalizar a aparência do formulário.

* **rootPanel:** O painel raiz de um formulário adaptável. Ele pode conter subpainéis sob o nó items . Cada painel, incluindo o painel raiz, pode ter um layout associado a ele. O layout do painel determina como o formulário é posicionado. Por exemplo, no layout Acordeão, seus itens são apresentados como Etapas de acordeão.

* **barra de ferramentas:** Um contêiner de Formulário adaptável tem uma barra de ferramentas global associada, que é global ao formulário. Essa barra de ferramentas pode ser adicionada usando o **[!UICONTROL Adicionar barra de ferramentas]** na barra de edição, que permite que os autores adicionem ações, como Enviar, Salvar, Redefinir e assim por diante.

* **ativos:** Esse nó contém informações adicionais usadas para a criação de formulários. Por exemplo, detalhes do modelo de formulário, detalhes de localização e assim por diante.
