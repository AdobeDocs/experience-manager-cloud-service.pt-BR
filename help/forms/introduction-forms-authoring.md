---
title: Introdução à criação do Forms adaptável
description: O AEM Forms fornece uma interface fácil de usar, mas eficiente para a criação do Forms adaptável. Ele fornece vários componentes e ferramentas que podem ser usadas para criar formulários.
content-type: reference
topic-tags: author, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Adaptive Forms, Foundation Components
exl-id: 16f86dae-86fb-481b-8978-b8898705ed7e
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '2496'
ht-degree: 89%

---

# Construtor adaptável do Forms {#introduction-to-authoring-adaptive-forms}

>[!NOTE]
>
> A Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-forms-authoring.html) |
| AEM as a Cloud Service | Este artigo |

## Visão geral {#overview}

Formulários adaptáveis fornecem uma experiência envolvente, responsiva, dinâmica e adaptável. O [!DNL AEM Forms] oferece uma interface intuitiva e componentes prontos para uso para criar e trabalhar com formulários adaptáveis. É possível optar por criar um formulário adaptável com base em um modelo ou esquema de formulário ou sem um modelo de formulário. É importante escolher cuidadosamente o modelo de formulário que atenda não apenas às suas necessidades, mas que amplie seus investimentos de infraestrutura e ativos. Você pode escolher entre as seguintes opções ao criar um formulário adaptável:

* **Usando um modelo de dados de formulário (FDM)**
  A [integração de dados](data-integration.md) permite integrar entidades e serviços de diferentes fontes de dados em um Modelo de Dados de Formulário (FDM) que você pode usar para criar o Adaptive Forms. Escolha Modelo de dados de formulário (FDM) se o Formulário adaptável que você está criando envolver a busca e a gravação de dados de e para várias fontes de dados.

* **Usar um modelo de formulário XDP**
Esse é um modelo de formulário ideal se você tiver investido em formulários baseados em XFA ou XDP. Ele fornece uma maneira direta de converter formulários baseados em XFA em formulários adaptáveis. Quaisquer regras de XFA existentes são retidas nos formulários adaptáveis associados. O formulário adaptável resultante oferece suporte a construções em XFA, como validações, eventos, propriedades e padrões.

* **Usar uma definição de esquema XML (XSD) ou um esquema JSON**
Os esquemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na sua organização. Você pode associar o esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estarão disponíveis para uso na guia Objetos do modelo de dados do navegador de conteúdo ao criar formulários adaptáveis.

* **Não usar nenhum modelo de formulário**
Os formulários adaptáveis criados com essa opção não usam nenhum modelo de formulário. O XML de dados gerado desses formulários tem uma estrutura simples com campos e valores correspondentes.

  >[!NOTE]
  >
  > Você pode modificar as propriedades do modelo de formulário no Criador de formulários adaptáveis ou no Criador de modelos de formulários adaptáveis. Para obter mais informações, consulte [Editar as propriedades do modelo de formulário de um formulário adaptável](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model).

Para criar um formulário adaptável, consulte [Criação de um formulário adaptável](creating-adaptive-form.md).

## Interface de criação do formulário adaptável {#adaptive-form-authoring-ui}

A interface otimizada para toque da criação de formulários adaptáveis é intuitiva e oferece:

* Funcionalidade de arrastar e soltar
* Componentes de formulário padrão
* Repositório integrado de ativos

Ao criar ou editar um Formulário adaptável existente, você usa os seguintes elementos da interface do usuário:

* [Barra lateral](#sidebar)
* [Barra de ferramentas da página](#page-toolbar)
* [Barra de ferramentas Componente](#component-toolbar)
* [Página do formulário adaptável](#af-page)

<!-- ![Adaptive Form authoring UI](assets/formeditor.png)

**A.** Sidebar **B.** Page toolbar **C.** Adaptive Form page -->

### Barra lateral {#sidebar}

A barra lateral permite

* Pesquisar, visualizar e usar ativos no seu repositório de gerenciamento de ativos digitais (DAM) do AEM.
* Visualize o conteúdo do formulário, como painéis, componentes, campos e layout.
* Adicione componentes ao formulário.
* Edite propriedades de componentes.

![Barra lateral](assets/sidebar-comps.png)

**A.** Navegador de conteúdo **B.** Navegador de propriedades **C.** Navegador de ativos **D.** Navegador de componentes

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

A barra lateral inclui os seguintes navegadores:

* **Navegador de conteúdo**
No navegador de conteúdo, é possível ver:

   * **Objetos de formulário**
Mostra a hierarquia de objetos do formulário. O autor pode navegar até um componente de formulário específico selecionando esse elemento na Árvore de objetos de formulário. O autor pode pesquisar objetos e reorganizá-los a partir dessa árvore.

   * **Objetos do modelo de dados**
Permite ver a hierarquia do modelo de formulário.
Ela permite arrastar e soltar elementos do modelo de formulário no Formulário adaptável. Os elementos adicionados são convertidos automaticamente em componentes de formulário, mantendo suas propriedades originais. É possível ver objetos de modelo de dados quando o formulário usa esquema XML, esquema JSON ou modelo XDP.

* **Navegador de propriedades**

  Permite editar as propriedades de um componente. As propriedades mudam de acordo com um componente. Para ver as propriedades do container do Formulário adaptável:

  Selecione um componente e, em seguida, selecione ![nível do campo](assets/Smock_SelectContainer_18_N.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e selecione ![propriedades](assets/Smock_Wrench_18_N.svg).

* **Navegador de ativos**

  Segmenta diferentes tipos de conteúdo, como imagens, documentos, páginas, filmes e assim por diante.

* **Navegador de componentes**

  Inclui componentes que podem ser usados para criar um Formulário adaptável. Você pode arrastar os componentes para o Formulário adaptável para adicionar elementos de formulário e configurá-los de acordo com os requisitos. A tabela a seguir descreve os componentes listados no navegador de componentes.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funcionalidade</strong></th>
  </tr>
  <tr>
   <td>Bloco do Adobe Sign</td>
   <td>Adiciona um bloco de texto com espaços reservados para que os campos sejam preenchidos ao assinar usando o Adobe Sign.</td>
  </tr>
  <tr>
   <td>Botão</td>
   <td>Adiciona um botão, que pode ser configurado para executar ações, como salvar, redefinir, prosseguir, voltar e assim por diante.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Adiciona a validação CAPTCHA usando o serviço Google reCAPTCHA.</td>
  </tr>
  <tr>
   <td>Gráfico</td>
   <td>Adiciona um gráfico que pode ser usado nos Formulários adaptáveis e em documentos para representação visual de dados bidimensionais em painéis repetíveis e linhas de tabela.</td>
  </tr>
  <tr>
   <td>Caixa de seleção</td>
   <td>Adiciona uma caixa de seleção.</td>
  </tr>
  <tr>
   <td>Campo de entrada de data</td>
   <td>Use o componente Campo de entrada de data em seu formulário para permitir que os clientes preencham dia, mês e ano separadamente em três caixas. Você pode personalizar a aparência do componente e alterar o formato da data. Por exemplo, você pode permitir que seus clientes insiram as datas no formato MM/DD/AAAA ou DD/MM/AAAA.</td>
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
   <td><p>Adicione um campo para capturar o endereço de email. O componente Email, por padrão, valida endereços de email usando a seguinte expressão regular.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;'*+/=?^_&grave;{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Anexo de arquivo</td>
   <td><p>Adiciona um botão que permite aos usuários navegar e anexar documentos compatíveis a um formulário.</p> <p><strong>Observação: </strong>o componente de Anexo de arquivo é compatível com um conjunto predefinido de formatos de arquivo nos Formulários adaptáveis habilitado para o Adobe Sign. Para obter mais informações, consulte <a href="https://helpx.adobe.com/br/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formatos de arquivo compatíveis</a>.</p> </td>
  </tr>
  <tr>
   <td>Listagem de Anexo de arquivo</td>
   <td>Adiciona um campo que lista todos os anexos enviados usando o componente Anexo de arquivo.</td>
  </tr>
  <tr>
   <td>Rodapé<br /> </td>
   <td>Adiciona o cabeçalho da página que normalmente inclui o logotipo de uma corporação, o título do formulário e o resumo.<br /> </td>
  </tr>
  <tr>
   <td>Cabeçalho</td>
   <td>Adiciona o rodapé da página que normalmente inclui informações sobre direitos autorais e links para outras páginas. </td>
  </tr>
  <tr>
   <td>Imagem</td>
   <td>Permite inserir uma imagem.</td>
  </tr>
  <tr>
   <td>Opção de imagem</td>
   <td>Permite que seus clientes selecionem uma imagem para fornecer informações. Você pode usar as informações para fornecer serviços personalizados aos seus clientes.</td>
  </tr>
  <tr>
   <td>Próximo botão</td>
   <td>Adiciona um botão para navegar para o próximo painel em um formulário.</td>
  </tr>
  <tr>
   <td>Caixa numérica</td>
   <td>Adiciona um campo para capturar valores numéricos</td>
  </tr>
  <tr>
   <td>Escalonador numérico</td>
   <td>Use o Escalonador numérico em seu formulário para permitir que os clientes insiram um valor numérico, o qual eles podem aumentar ou diminuir com base em um passo predefinido.</td>
  </tr>
  <tr>
   <td>Painel</td>
   <td><p>Adiciona um painel ou subpainel.</p> <p>Você também pode adicionar um componente de painel da barra de ferramentas do painel pai usando o botão <span class="uicontrol">Adicionar painel filho</code> botão. Da mesma forma, é possível adicionar uma barra de ferramentas específica do painel usando o botão <span class="uicontrol">Adicionar barra de ferramentas do painel</code> botão. É possível configurar a posição da barra de ferramentas do painel usando a caixa de diálogo Editar painel.</p> </td>
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
   <td>Adiciona um botão para redefinir os campos do formulário.</td>
  </tr>
  <tr>
   <td>Botão Salvar</td>
   <td>Adiciona um botão para salvar os dados do formulário.</td>
  </tr>
  <tr>
   <td>Assinatura escrita</td>
   <td>Adiciona um campo para capturar assinaturas escritas.</td>
  </tr>
  <tr>
   <td>Separador</td>
   <td>Permite a separação visual de painéis em seu formulário.</td>
  </tr>
  <tr>
   <td>Etapa de assinatura</td>
   <td>Exibe as informações fornecidas no formulário e os campos de assinatura para o usuário verificar e assinar o formulário.</td>
  </tr>
  <tr>
   <td>Texto</td>
   <td>Permite especificar texto estático.</td>
  </tr>
  <tr>
   <td>Botão Enviar</td>
   <td>Adiciona um botão para enviar o formulário para a ação de envio configurada.</td>
  </tr>
  <tr>
   <td>Etapa de resumo</td>
   <td>Envia o formulário e exibe o texto resumido que os autores especificam após o envio do formulário. </td>
  </tr>
  <tr>
   <td>Alternar</td>
   <td>Adiciona um botão que executa um botão de alternância ou habilitação/desabilitação. Não é possível adicionar mais de duas opções no componente Alternar. Como um botão de alternância pode ter apenas dois valores: ligado ou desligado, não é possível torná-lo obrigatório. Pelo menos um valor é salvo independentemente da entrada do usuário. <br /> </td>
  </tr>
  <tr>
   <td>Tabela</td>
   <td>Adiciona uma tabela que permite organizar dados em linhas e colunas. </td>
  </tr>
  <tr>
   <td>Telefone</td>
   <td><p>Adicione um campo para capturar o número de telefone. O componente Telefone permite que os autores configurem um dos seguintes tipos de número de telefone. Cada tipo está associado a uma expressão regular padrão para validação.</p>
    <ul>
     <li>O tipo Internacional é validado por <code>^[+][0-9]{0,14}$</code>.</li>
     <li>O tipo USPhoneNumber é validado por <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>O tipo UKPhoneNumber é validado por <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Tipo Personalizado não fornece um padrão de validação modelo. Obtém o valor do último tipo de número de telefone selecionado. Você também pode especificar seu próprio padrão de validação personalizado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Termos e condições<br /> </td>
   <td>Adiciona um campo que os autores podem usar para especificar os termos e condições para que os usuários revisem antes de preencher o formulário.</td>
  </tr>
  <tr>
   <td>Caixa de texto </td>
   <td><p>Adiciona uma caixa de texto na qual o usuário pode especificar as informações necessárias. </p> <p>Por padrão, o componente Caixa de texto apenas aceita texto sem formatação. Você pode habilitar um componente Caixa de texto para aceitar rich text. Um componente de texto Rich text habilitado fornece opções para adicionar cabeçalhos, alterar estilos de caracteres (negrito, itálico, sublinhar os caracteres), criar listas ordenadas e não ordenadas, alterar o plano de fundo do texto e a cor do texto e adicionar hiperlinks. Para ativar o rich text de uma caixa de texto, ative a opção<strong> Permitir Rich text</strong> nas propriedades do componente.</p> </td>
  </tr>
  <tr>
   <td>Título</td>
   <td>Especifica um título para o Formulário adaptável.</td>
  </tr>
  <tr>
   <td>Etapa de verificação</td>
   <td><p>Adicione um espaço reservado para exibir o formulário preenchido para verificação por usuário.</p> <p><strong>Observação</strong>: o formulário adaptável que contém o componente Verificar não dá suporte a usuários anônimos. Além disso, não é recomendado usar o componente Verificar em um fragmento de Formulário adaptável.</p> </td>
  </tr>
 </tbody>
</table>

### Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas da página na parte superior fornece opções que permitem visualizar o formulário, alterar as propriedades do formulário e editar o layout do formulário. É possível visualizar o formulário ao criá-lo e fazer alterações de acordo. Na barra de ferramentas da página, você observa:

* **Alternar painel lateral** ![alternar-painel-lateral](assets/Smock_RailLeft_18_N.svg): Permite exibir ou ocultar a Barra Lateral.

* **Informações da página** ![opções-tema](assets/Smock_Properties_18_N.svg): permite exibir as propriedades da página, publicar/desfazer a publicação de um formulário, iniciar um fluxo de trabalho de formulário e abrir o formulário na interface clássica.

* **Emulador** ![régua](assets/Smock_Devices_18_N.svg): permite você emular a aparência de seu formulário para diferentes tamanhos de exibição, como tablets e telefones.

* **Editar**: permite selecionar outros modos, como: **[!UICONTROL Editar]**, **[!UICONTROL Estilo]**, **[!UICONTROL Desenvolvedor]** e **[!UICONTROL Design]**.

   * **Editar**: permite editar as propriedades do formulário e seus componentes. Por exemplo, adicionar um componente, soltar uma imagem e especificar campos obrigatórios.
   * **Estilo**: permite estilizar a aparência dos componentes do formulário. Por exemplo, no modo de estilo, é possível selecionar um painel e especificar a cor do plano de fundo.

   * **Desenvolvedor**: permite que um desenvolvedor:

      * Descubra que formulários são compostos.
      * Depure onde e quando está acontecendo, o que, por vezes, ajuda a resolver problemas.

      * **Design**. Permitir ativar ou desativar componentes personalizados ou componentes prontos para uso que não estejam listados na Barra lateral.

* **Visualizar**: permite que você visualize a aparência do formulário ao publicá-lo.

### Barra de ferramentas Componente {#component-toolbar}

![Barra de ferramentas Componente na interface de toque](assets/component-toolbar.png)

Ao selecionar um componente, você visualiza uma barra de ferramentas que permite trabalhar nele. Há opções para recortar, colar, mover e especificar as propriedades dos componentes. As opções são:

A.**Configurar**: ao selecionar **[!UICONTROL Configurar]**, as propriedades do componente ficam visíveis na barra lateral. A configuração dessas propriedades permite personalizar a experiência de captura de dados. Você pode alterar o nome do elemento do componente, especificar o texto do rótulo no campo Título do componente. O nome do elemento permite capturar valores inseridos pelos usuários usando o componente. Nas propriedades do componente, especifique o comportamento do componente e gerencie a entrada do usuário. Configure as propriedades na barra lateral para capturar os dados do usuário e usá-los para processamento adicional. As propriedades do container de Formulário adaptável permitem especificar as bibliotecas do cliente, os Layouts, os Temas, as configurações de Documento de registro, salvar configurações, as configurações de envio e as configurações de metadados.

B.**Copiar**: você pode usar a opção de copiar para copiar um componente e colá-lo em outros lugares do formulário. Quando você cola um componente, o componente colado obtém um novo nome de elemento, mas retém as propriedades do componente copiado.

C.**Recortar**: você pode usar a opção de recortar para mover um componente de um lugar para outro no Formulário adaptável.

D. **Excluir**: permite excluir o componente do formulário.

E. **Inserir**: permite inserir um componente acima do componente selecionado.

F. **Colar**: permite colar o componente cortado ou copiado usando as opções descritas acima.

G. **Editar regras**: permite abrir o editor de regras. Para obter mais informações, <!-- see [Rule Editor](rule-editor.md). -->

H. **Grupo**: permite selecionar vários componentes se você deseja cortar, copiar ou colar mais de um componente.

I. **Página principal**: permite selecionar a página principal de um componente. Por exemplo, um campo de texto está em uma subseção, que fica em uma seção. A seção encontra-se no guide root panel e o container de formulário adaptável é o principal de um guide root panel. Para um componente, você pode observar todas as opções com a hierarquia classificada de baixo para cima.

Por exemplo, se você selecionar **[!UICONTROL Pai]** para uma caixa de texto, poderá ver:

* Subseção
* Seção
* guideRootPanel
* Container de formulário adaptativo

J. **Outros**: fornece mais opções para trabalhar com o componente selecionado.

* Exibir expressão SOM
* Salvar um painel como fragmento (somente para painéis)
* Adicionar painel filho (somente para painéis)
* Adicionar barra de ferramentas do painel (somente para painéis)
* Substituir (exceto para painéis)

### Página do formulário adaptável {#af-page}

A página de Formulário adaptável é o formulário real. É como qualquer outra página WCM modelada como o WCM componente `cq:Page`. A imagem a seguir mostra a estrutura de conteúdo de um formulário adaptável típico.

![Estrutura de conteúdo de uma página WCM de formulário adaptável](assets/afstructure.png)

A estrutura de conteúdo normalmente contém os seguintes componentes principais:

* **guideContainer**: a raiz de um formulário adaptável, que é marcado como **[!UICONTROL Início do formulário adaptável]** na interface do formulário adaptável. Nesse componente, você pode especificar:

   * *Layout móvel do formulário adaptável*: define a aparência do formulário em dispositivos móveis.
   * *Página de agradecimento*: define a página para a qual o usuário é redirecionado após enviar o formulário.
   * *Enviar ação*: define como o formulário é processado no servidor depois que o usuário envia o formulário.
   * *Estilo*: especifica o caminho para o arquivo CSS usado para personalizar a aparência do formulário.

* **rootPanel:** o painel raiz de um formulário adaptável. Ele pode conter sub-painéis sob o nó itens. Cada painel, incluindo o painel raiz, pode ter um layout associado a ele. O layout do painel determina como o formulário é posicionado. Por exemplo, no layout Accordion, seus itens são apresentados como etapas Accordion.

* **barra de ferramentas:** um container de Formulário adaptável tem uma barra de ferramentas global associada, que é global ao formulário. Essa barra de ferramentas pode ser adicionada usando o **[!UICONTROL Adicionar barra de ferramentas]** na barra de edição, que permite que se adicionem ações, como Enviar, Salvar, Redefinir e assim por diante.

* **ativos:** esse nó contém informações adicionais usadas para a criação de formulários. Por exemplo, detalhes do modelo de formulário, detalhes de localização e assim por diante.

## Assistente de IA no AEM

Para clientes que possuem [critérios de pré-requisito concluídos](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access), o Assistente de IA do AEM está disponível para usuários de suas organizações. Consulte [Assistente de IA no AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

## Consulte também {#see-also}

{{see-also}}
