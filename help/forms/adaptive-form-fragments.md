---
title: Como criar e usar fragmentos de formulário adaptáveis?
description: O fragmento de formulário é um componente modular e reutilizável de um formulário. Saiba como criar fragmentos de formulário e reutilizá-los em formulários para uma montagem de formulário eficiente.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
source-git-commit: 8de3189495c374fad156e7e6cb23c96c84ece482
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 1%

---


# Criar e usar fragmentos adaptáveis do Forms em um formulário adaptável  {#adaptive-form-fragments}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Embora cada formulário seja projetado para um propósito específico, há alguns segmentos comuns na maioria dos formulários, como o de fornecer detalhes pessoais, como nome e endereço, detalhes da família, detalhes de renda etc. Os desenvolvedores de formulários são necessários para criar esses segmentos comuns sempre que um novo formulário for criado. O Forms adaptável fornece um mecanismo conveniente para criar segmentos de formulário, como um painel ou um grupo de campos, somente uma vez e reutilizá-los no Forms adaptável. Esses segmentos reutilizáveis e independentes são chamados de Fragmentos de formulário adaptáveis.


## Criar um fragmento {#create-a-fragment}

Você pode criar um fragmento de formulário adaptável do zero ou salvar um painel em um formulário adaptável existente como fragmento.

### Criar fragmento do zero {#create-fragment-from-scratch}

1. Efetue logon no [!DNL AEM Forms] instância do autor em https://[*hostname*]:[*porta*]/aem/forms.html.
1. Clique em **Criar > Fragmento de formulário adaptável**.
1. Especifique título, nome, descrição e tags para o fragmento.

   >[!NOTE]
   >
   >Certifique-se de especificar um nome exclusivo para o fragmento. Se já existir outro fragmento com o mesmo nome, o fragmento não será criado.

1. Clique para abrir a **Modelo de formulário** e na guia **Selecionar de** selecione um dos seguintes modelos para o fragmento:

   * **Nenhum**: especifica criar o fragmento do zero sem usar nenhum modelo de formulário.

     >[!NOTE]
     >
     > Em Forms adaptáveis baseados em Componentes principais, é possível usar um único fragmento de formulário várias vezes em um formulário. Ele oferece suporte a fragmentos de formulário baseados em nenhum e em esquema.

   * **Modelo de formulário**: especifica criar o fragmento usando um modelo XDP carregado no [!DNL AEM Forms]. Selecione o modelo XDP apropriado como o modelo de formulário para o fragmento.

   ![Criação de um formulário adaptável usando o modelo de formulário como modelo](assets/form-template-model.png)

   Os subformulários marcados como fragmentos no formulário selecionado modelo também são exibidos. É possível selecionar um subformulário para o Fragmento de formulário adaptável no lista suspenso.

   ![Selecione os subformulários no formulário especificado modelo](assets/fragment-subform.png)

   Além disso, é possível criar um Fragmento de formulário adaptável usando subformulários que não são marcados como fragmentos no formulário modelo especificando o expressão SOM para o subformulário na caixa suspensa.

   * **Esquema** XML: especifica a criação do fragmento usando uma schema XML enviada para [!DNL AEM Forms]. É possível upload ou selecionar nos esquemas XML disponíveis como o modelo de formulário do fragmento.

   ![Criar um fragmento de formulário adaptável baseado em um schema XML como modelo](assets/xml-schema-model.png)

   Você também pode criar um fragmento de formulário adaptável selecionando um complexType presente no esquema selecionado na caixa suspensa.

   ![Selecione um tipo complexo no modelo de esquema XML especificado](assets/complex-type.png)

1. Clique em **Criar** e clique em **Abertura** para abrir o fragmento, com um modelo padrão, no modo de edição.

No modo de edição, você pode arrastar e soltar qualquer componente de Formulário adaptável do sidekick do AEM no fragmento. <!-- For information about Adaptive Form components, see Introduction to authoring Adaptive Forms. -->

Além disso, se você selecionou um esquema XML ou modelo de formulário XDP como o modelo de formulário do fragmento, uma nova guia que exibe a hierarquia do modelo de formulário aparece no localizador de conteúdo. Ela permite arrastar e soltar elementos do modelo de formulário no fragmento. Os elementos de modelo de formulário adicionados são convertidos em componentes de formulário, ao mesmo tempo em que retêm as propriedades originais do XDP ou XSD associado.

### Salvar painel como um fragmento {#save-panel-as-a-fragment}

1. Abra um Formulário adaptável que contenha o painel que você deseja salvar como Fragmento de formulário adaptável.
1. Na barra de ferramentas do painel, clique em **[!UICONTROL Salvar como fragmento]**. A caixa de diálogo Salvar como fragmento é aberta.

   >[!NOTE]
   >
   >Se o painel que você está salvando como fragmento contiver painel secundário, o fragmento resultante os incluirá.

1. Na caixa de diálogo Criação de fragmento, especifique as seguintes informações:

   * **Nome**: Nome do fragmento. O valor padrão é o nome do elemento do painel. É um campo obrigatório.

     >[!NOTE]
     >
     >Certifique-se de especificar um nome exclusivo para o fragmento. Se já existir outro fragmento com o mesmo nome, o fragmento não será criado.

   * **Título**: Título do fragmento. O valor padrão é o título do painel.

   * **Descrição**: Descrição do fragmento.

   * **Tags**: marca os metadados do fragmento.

   * **Caminho de destino**: Caminho do repositório onde o fragmento é salvo. Se você não especificar um caminho, um nó com o mesmo nome do fragmento será criado ao lado do nó que contém o Formulário adaptável. O fragmento é salvo neste nó.

   * **Modelo de formulário**: Dependendo do modelo de formulário para o Formulário adaptável, esse campo exibe a variável **Esquema XML**, **Modelo de formulário** ou **Nenhum**. É um campo não editável.

   * **Raiz do modelo de fragmento**: aparece somente no Adaptive Forms baseado em XSD. Especifica a raiz do modelo de fragmento. Você pode escolher **/** ou o tipo complexo XSD no menu suspenso. Observe que você só poderá reutilizar o fragmento em outro Formulário adaptável se selecionar o tipo complexo como a raiz do modelo de fragmento.
Se você escolher **/** como a raiz do modelo de fragmento, a árvore XSD completa da raiz fica visível na guia Modelo de dados do formulário adaptável. Para uma raiz de modelo de fragmento de tipo complexo, somente os descendentes do tipo complexo selecionado são visíveis na guia Modelo de dados do formulário adaptável.

   * **XSD Ref**: aparece somente no Adaptive Forms baseado em XSD. Ela exibe a localização do esquema XML.

   * **XDP Ref**: aparece somente no Adaptive Forms baseado em XDP. Ela exibe o local do modelo de formulário XDP.

   ![save-fragment](assets/save-fragment.png)

   Caixa de diálogo Salvar como fragmento

1. Clique em **OK**.

   O painel é salvo no local especificado ou padrão no repositório. No Formulário adaptável, o painel é substituído por um instantâneo do fragmento. Como mostrado abaixo, o painel Informações gerais e seus painéis secundários, Informações pessoais e Endereço, são salvos como um fragmento.

   Para editar o fragmento, clique em **[!UICONTROL Editar ativo]** na barra de ferramentas do painel. O fragmento é aberto em uma nova guia ou janela no modo de edição.

   ![Edição de fragmento](assets/edit-fragment.png)

## Trabalho com fragmentos {#working-with-fragments}

### Configurar a aparência do fragmento {#configure-fragment-appearance}

Qualquer fragmento inserido no Adaptive Forms é exibido como uma imagem de espaço reservado. O espaço reservado exibe títulos de até dez painéis secundários no fragmento. Você pode configurar [!DNL AEM Forms] para mostrar o fragmento completo em vez da imagem de espaço reservado.

Execute as seguintes etapas para mostrar fragmentos completos em formulários:

1. Vá para a página de configuração do console da Web do AEM em https:[*host*]:[*porta*]/system/console/configMgr

1. Pesquisar e clicar **[!UICONTROL Serviço de configuração de formulário adaptável]** para abri-lo no modo de edição.
1. Desativar **[!UICONTROL Ativar espaço reservado no lugar do fragmento]** para mostrar fragmentos completos em vez da imagem de espaço reservado.

### Inserir um fragmento em um Formulário adaptável {#insert-a-fragment-in-an-adaptive-form}

Os fragmentos de formulário adaptáveis criados são exibidos na guia Fragmentos de formulário adaptáveis do localizador de conteúdo do AEM. Para inserir um fragmento de formulário adaptável em um formulário adaptável:

1. Abra o Formulário adaptável, no modo de edição, no qual deseja inserir um Fragmento de formulário adaptável.
1. Clique em **Assets** ![assets-browser](assets/assets-browser.png) na barra lateral. No navegador de ativos, selecione **Fragmentos do formulário adaptável** no menu suspenso.

   Também é possível optar por exibir todos os Fragmentos de formulário adaptável ou filtrar com base em seu modelo de formulário - Modelo de formulário, Esquema XML ou Básico.

1. Arraste e solte um fragmento de formulário adaptável no formulário adaptável.

   >[!NOTE]
   >
   >O fragmento de formulário adaptável não está ativado para criação no formulário adaptável. Além disso, não é possível usar um fragmento baseado em XSD em um Formulário adaptável baseado em JSON e o oposto.

O fragmento de formulário adaptável é inserido por referência no formulário adaptável e é sincronizado com o fragmento de formulário adaptável independente. Ou seja, ao atualizar o Fragmento de formulário adaptável, as alterações são refletidas em todo o Forms adaptável onde o fragmento é usado.

### Incorporar um fragmento no Formulário adaptável {#embed-a-fragment-in-adaptive-form}

É possível optar por incorporar um fragmento de formulário adaptável em um formulário adaptável clicando **em Incorporar ativo: *fragmentName*>** botão na barra de ferramentas do painel do fragmento adicionado, como mostrado na imagem de exemplo a seguir.

![Incorpore um fragmento de formulário no formulário adaptável](assets/embed-fragment.png)

>[!NOTE]
>
>O fragmento incorporado não está mais vinculado ao fragmento independente. É possível editar os componentes no fragmento incorporado a partir do formulário adaptável.

### Uso de fragmentos em fragmentos {#using-fragments-within-fragments}

É possível criar Fragmentos de formulário adaptáveis aninhados, o que significa que é possível arrastar e soltar um fragmento em outro fragmento e ter uma estrutura de fragmento aninhada.

### Alterar fragmentos {#change-fragments}

É possível substituir ou alterar um fragmento de formulário adaptável por outro fragmento usando o **Selecionar ativo do fragmento** na caixa de diálogo Editar componente de um painel Fragmento de formulário adaptável.

### Uso de um fragmento de formulário várias vezes em um Formulário adaptável {#using-form-fragment-mutiple-times-in-af}

Você pode usar um fragmento de formulário baseado em esquema várias vezes em um Formulário adaptável para salvar dados exclusivamente para cada campo de fragmento de formulário. Por exemplo, você pode usar um fragmento de formulário de endereço para coletar detalhes de endereço para endereços permanentes, de comunicação e vivos presentes em um formulário de aplicativo de empréstimo.

![uso de vários fragmentos no formulário adaptável](/help/forms/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> * Se você usar fragmentos de formulário com base em nenhum várias vezes em um formulário adaptável, ocorre a sincronização de dados entre os campos dos fragmentos. Você pode usar um único [fragmento de formulário (com base nos componentes principais)](/help/forms/adaptive-form-fragments-core-components.md)  várias vezes em um formulário. Suporta fragmentos de formulário baseados em nenhuma base e em schema sem problemas de sincronização de dados.

## Mapeamento automático de fragmentos para associação de dados {#auto-mapping-of-fragments-for-data-binding}

Ao criar um fragmento de formulário adaptável usando um modelo de formulário XFA ou tipo complexo XSD e arrastar e soltar o fragmento em um formulário adaptável, o fragmento XFA ou o tipo complexo XSD é substituído automaticamente pelo fragmento de formulário adaptável correspondente cuja raiz do modelo de fragmento é mapeada ao fragmento XFA ou ao tipo complexo XSD.

É possível alterar o ativo do fragmento e suas associações na caixa de diálogo Editar componente.

>[!NOTE]
>
>Você também pode arrastar e soltar um fragmento de formulário adaptável vinculado da biblioteca de fragmentos de formulário adaptável no localizador de conteúdo de AEM e fornecer a referência de vinculação correta na caixa de diálogo Editar componente do painel Fragmento de formulário adaptável.

## Gerenciar fragmentos {#manage-fragments}

É possível executar várias operações em Fragmentos de formulário adaptável usando o [!DNL AEM Forms] interface.

1. Acesse `https://[hostname]:'port'/aem/forms.html`.

1. Clique **em Selecionar** na barra de ferramentas interface [!DNL AEM Forms] e selecione um fragmento de formulário adaptável. A barra de ferramentas exibe as seguintes operações que você pode executar no fragmento de formulário adaptável selecionado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operação</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>Abrir</p> </td>
   <td><p>Abre o fragmento de formulário adaptável selecionado no modo de edição.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Propriedades da exibição</p> </td>
   <td><p>Abre o painel Propriedades. No painel Propriedades, é possível visualizar e editar propriedades, gerar uma visualização e fazer upload de uma imagem em miniatura para o fragmento selecionado. Para obter mais informações, consulte <a href="manage-form-metadata.md" target="_blank">Gerenciamento de metadados</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copiar</p> </td>
   <td><p>Copia o fragmento selecionado. O botão Colar aparece na barra de ferramentas.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Baixa o fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Visualização</p> </td>
   <td><p>Fornece opções para visualizar o fragmento como um HTML ou uma visualização personalizada mesclando dados de um arquivo XML com o fragmento. <!-- For more information, see <a href="previewing-forms.md" target="_blank">Previewing a form</a>.<br /> <br /> --></p> </td>
  </tr>
  <tr>
   <td><p>Iniciar revisão/Gerenciar revisão</p> </td>
   <td><p>Permite iniciar e gerenciar uma revisão do fragmento selecionado. <!-- For more information, see <a href="create-reviews-forms.md" target="_blank">Creating and managing reviews</a>.<br /> <br /> </p> --> </td>
  </tr>
  <tr>
   <td><p>Criar dicionário</p> </td>
   <td><p>Gera um dicionário para localizar o fragmento selecionado. <!-- For more information, see <a href="lazy-loading-adaptive-forms.md" target="_blank">Localizing Adaptive Forms</a>.<br /> <br /> --> </p> </td>
  </tr>
  <tr>
   <td><p>Publicar/Desfazer a publicação</p> </td>
   <td><p>Publica/cancela a publicação do fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Excluir</p> </td>
   <td><p>Exclui o fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Localização do formulário adaptável que contém fragmentos {#localizing-adaptive-form-containing-fragments}

Para localizar um Formulário adaptável que contenha Fragmentos de formulário adaptável, é necessário localizar o fragmento e o formulário separadamente. A ideia é localizar um fragmento uma vez e reutilizá-lo em vários Forms adaptáveis.

>[!NOTE]
>
>As chaves de localização no fragmento não aparecerão no arquivo XLIFF para um Formulário adaptável.

## Pontos principais a serem lembrados ao trabalhar com fragmentos {#key-points-to-remember-when-working-with-fragments}

* Certifique-se de que o nome do fragmento seja exclusivo. O fragmento não é criado se houver um fragmento existente com o mesmo nome.
* Em um Formulário adaptável baseado em XDP, se você salvar um painel como fragmento que inclui outro fragmento XDP, o fragmento resultante será vinculado automaticamente ao fragmento XDP filho. No caso de um Formulário adaptável baseado em XSD, o fragmento resultante é vinculado à raiz do esquema.
* Ao criar um fragmento de formulário adaptável, um nó de fragmento é criado, o que é semelhante ao nó guideContainer de um formulário adaptável, no CRXDe Lite.
* Um fragmento em um Formulário adaptável que usa um Modelo de dados de formulário diferente não é compatível. Por exemplo, um fragmento baseado em XDP não é compatível com um Formulário adaptável baseado em XSD e vice-versa.
* Os fragmentos de formulário adaptáveis estão disponíveis para uso por meio da guia Fragmentos de formulário adaptáveis no localizador de conteúdo do AEM.
* Qualquer expressão, script ou estilo em um Fragmento de formulário adaptável independente é retido quando inserido por referência ou incorporado em um Formulário adaptável.
* Não é possível editar um fragmento de formulário adaptável, que é inserido por referência, a partir de um Formulário adaptável. Para editar, edite o Fragmento de formulário adaptável independente ou incorpore o fragmento no Formulário adaptável.
* Ao publicar um formulário adaptável, você precisa publicar os fragmentos de formulário adaptáveis independentes inseridos por referência no formulário adaptável.
* Ao republicar um fragmento de formulário adaptável atualizado, as alterações são refletidas nas instâncias publicadas do formulário adaptável em que o fragmento é usado.
* O formulário adaptável que contém o componente Verificar não é compatível com usuários anônimos. Além disso, não é recomendado usar o componente Verificar em um fragmento de formulário adaptável.
* (**Somente** Mac) Para garantir que os fragmentos de formulário funcionalidade funciona perfeitamente em todos os cenários, adicione a seguinte entrada ao arquivo /private/etc/hosts:
  `127.0.0.1 <Host machine>`**Máquina de host**: a máquina Apple Mac na qual [!DNL AEM Forms] é implantada.

## Fragmentos de referência {#reference-fragments}

Os fragmentos de formulário de referência adaptável que você pode usar para criar seu formulário estão disponíveis. Para obter mais informações, consulte [Fragmentos de referência](reference-adaptive-form-fragments.md).

>[!MORELIKETHIS]
>
>* [Fragmentos de formulário adaptável nos Componentes principais](/help/forms/adaptive-form-fragments-core-components.md)
