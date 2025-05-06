---
title: Como criar fragmentos de formulário para criação com base no WYSIWYG
description: Saiba como criar fragmentos de formulário no Editor universal e adicioná-los a formulários.
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: 8dfcec0648f5b474113325b6cc6cffc754e21ec2
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%

---

# Criação de fragmentos de formulário no Editor universal

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email com o nome da sua organização GitHub e o nome do repositório do seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>

<span class="preview"> É um recurso de pré-lançamento acessível através do nosso [canal de pré-lançamento](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features). </span>

O Forms geralmente inclui seções comuns, como informações de contato, detalhes de identificação ou contratos de consentimento. Os desenvolvedores de formulários criam essas seções toda vez que criam um novo formulário, que é repetitivo e demorado.
Para eliminar essa duplicação de esforços, o Universal Editor fornece uma maneira de criar segmentos de formulário reutilizáveis, como painéis ou grupos de campos, apenas uma vez e reutilizá-los em vários formulários. Esses segmentos reutilizáveis, modulares e independentes são chamados de fragmentos de formulário. Por exemplo, o mesmo fragmento de contato de emergência pode ser usado em diferentes seções de um formulário, como para detalhes de contato do funcionário e do supervisor.

No final do artigo, você aprenderá a criar e usar fragmentos em formulários usando o Editor universal.

## Recursos dos fragmentos de formulário do Edge Delivery Services

* **Mantendo a consistência com fragmentos de formulário**
É possível integrar fragmentos em diferentes formulários, ajudando a manter layouts consistentes e conteúdo padronizado.

  >[!NOTE]
  >
  > Com uma abordagem &quot;alterar uma vez, refletir em todos os lugares&quot;, qualquer atualização feita em um fragmento se aplica automaticamente a todos os formulários no modo Visualização. No entanto, no modo Publicar, você deve publicar o fragmento ou republicar o formulário para que as alterações sejam refletidas.

* **Adicionando fragmentos de formulário várias vezes no formulário**
Você pode adicionar um fragmento de formulário várias vezes em um formulário e configurar suas propriedades de associação de dados para fontes de dados ou esquemas.

* **Usando fragmentos dentro de fragmentos**
É possível criar fragmentos de formulário aninhados, o que significa que você pode adicionar um fragmento em outro fragmento e ter uma estrutura de fragmento aninhada.

  >[!NOTE]
  >
  > Não é possível aninhar um fragmento nele mesmo, pois isso pode causar referências recursivas e comportamento não intencional, resultando em erros ou problemas de renderização.

## Considerações ao usar fragmentos de formulário do Edge Delivery Services

* É necessário adicionar o mesmo URL do GitHub no fragmento e no formulário em que você pretende usar o fragmento.
* Não é possível editar um fragmento de formulário em um formulário. Para fazer alterações, modifique o fragmento de formulário independente.

## Pré-requisitos

* [Configure seu repositório GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) para estabelecer uma conexão entre seu ambiente AEM e o repositório GitHub.
* Se você já estiver usando o Edge Delivery Services, adicione a versão mais recente do [bloco adaptável do Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) ao seu repositório GitHub.
* A instância do Autor do AEM Forms inclui um modelo com base no Edge Delivery Services.
* Mantenha o URL da instância do autor do AEM Forms as a Cloud Service e do Repositório GitHub acessíveis.

## Trabalhar com fragmentos de formulário do Edge Delivery Services

Você pode criar fragmentos de formulário do Edge Delivery Services no Editor universal e adicionar os fragmentos criados aos formulários do Edge Delivery Services. Você pode executar as seguintes ações com os fragmentos de formulário do Edge Delivery Services:

* [Criação de fragmentos de formulário](#creating-form-fragments)
* [Adição de fragmentos de formulário a um formulário](#adding-form-fragments-to-a-form)
* [Gerenciamento de fragmentos de formulário](#managing-form-fragments)

### Criação de fragmentos de formulário

Para criar um fragmento de formulário no Universal Editor, execute as seguintes etapas:

1. Faça logon na instância de autor do AEM Forms as a Cloud Service.
1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Clique em **Criar > Fragmento de formulário adaptável**.

   ![Criar fragmento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   O assistente **Criar fragmento de formulário adaptável** é exibido.
1. Selecione o modelo baseado em Edge Delivery Services na guia **Selecionar modelo** e clique em **[!UICONTROL Avançar]**.
   ![Selecionar modelo do Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Especifique título, nome, descrição e tags para o fragmento. Certifique-se de especificar um nome exclusivo para o fragmento. Se outro fragmento existir com o mesmo nome, o fragmento não será criado.
1. Especifique a **URL do GitHub**. Por exemplo, se o repositório GitHub for nomeado como `edsforms`, ele estará localizado na conta `wkndforms`, a URL será `https://github.com/wkndforms/edsforms`.

   ![propriedades básicas](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Opcional) Clique para abrir a guia **Modelo de formulário** e, no menu suspenso **Selecionar de**, selecione um dos seguintes modelos para o fragmento:

   ![Exibe o tipo de modelo na guia Modelo de Formulário](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **Modelo de dados de formulário (FDM)**: integre objetos de modelo de dados e serviços de fontes de dados ao seu fragmento. Escolha Modelo de dados de formulário (FDM) se o formulário exigir leitura e gravação de dados de várias fontes.

   * **Esquema JSON**: integre seu formulário a um sistema de back-end associando um esquema JSON que define a estrutura de dados. Ela permite adicionar conteúdo dinâmico usando os elementos do esquema.
   * **Nenhum**: especifica criar o fragmento do zero sem usar nenhum modelo de formulário.

   >[!NOTE]
   >
   > Para saber como integrar formulários ou fragmentos a um Modelo de Dados de Formulário (FDM) no Editor Universal para usar fontes de dados de back-end diversas, [clique aqui](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Opcional) Especifique a **Data de publicação** ou a **Data de cancelamento da publicação** do fragmento na guia **Avançado**.

   ![Guia Avançado](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Clique em **Criar** e um assistente será exibido.

   ![Editar fragmento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Clique em **Editar** e o fragmento criado com um modelo padrão será aberto no Editor Universal para criação.

   ![Fragmento no Editor Universal para criação](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   No modo de edição, é possível adicionar qualquer componente de formulário ao fragmento. Para saber como criar um fragmento no Universal Editor, consulte o artigo [Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

   A captura de tela abaixo exibe o `contact fragment` criado no Editor Universal.

   ![Fragmento do contato](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   Depois de criar o fragmento, você pode [adicionar o fragmento criado no Edge Delivery Services Forms](#adding-form-fragments-in-forms).

### Adição de fragmentos de formulário a um formulário

Vamos criar um formulário `Employee Details` simples que inclua informações do funcionário e do supervisor. Você pode usar o fragmento `Contact Details` nos painéis de funcionário e supervisor. Para usar o fragmento de formulário no formulário, execute as seguintes etapas:

1. Abra o formulário no modo de edição.
1. Adicione o componente Fragmento de formulário ao formulário.
1. Abra o navegador Conteúdo e navegue até o componente **[!UICONTROL Formulário adaptável]** na **Árvore de conteúdo**.
1. Navegue até a seção em que deseja adicionar um fragmento. Por exemplo, navegue até o painel **Detalhes do Funcionário**.

   ![Navegar até a seção](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Clique no ícone **[!UICONTROL Adicionar]** e adicione o componente **[!UICONTROL Fragmento de Formulário]** da lista **Componentes de Formulário Adaptáveis**.
   ![Adicionar fragmento de formulário](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   Ao selecionar o componente **[!UICONTROL Fragmento de formulário]**, o fragmento é adicionado ao formulário. Você pode configurar as propriedades do fragmento adicionado abrindo suas **Propriedades**. Por exemplo, oculte o título do fragmento de suas **Propriedades**.

   ![Configurando propriedades do fragmento](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Selecione a **Referência do fragmento** na guia **Básico**. Todos os fragmentos disponíveis para o formulário, dependendo do modelo do formulário, são exibidos.

   Por exemplo, navegue até `/content/forms/af` e selecione o fragmento `Contact Details`.

   ![Selecionar fragmento](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Clique em **[!UICONTROL Selecionar]**.

   O fragmento de formulário é adicionado por referência ao formulário e permanece em sincronia com o fragmento de formulário independente.

   ![Fragmento no formulário](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   Você pode visualizar o formulário para ver como ele aparece no modo **Visualização**.

   ![Visualização](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Da mesma forma, você pode repetir as Etapas de 3 a 7 para inserir o fragmento `Contact Details` para o painel `Supervisor Details`.

   ![Formulário Detalhes do Funcionário](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### Gerenciamento de fragmentos de formulário

É possível executar várias operações em fragmentos de formulário usando a interface do usuário do AEM Forms.

1. Faça logon na instância de autor do AEM Forms as a Cloud Service.
1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

1. Selecione um fragmento de formulário e a barra de ferramentas exibe as seguintes operações que você pode executar no fragmento selecionado.

   ![Gerenciar fragmento](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>Operação</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
    </tr>
    <tr>
   <td><p>Editar</p> </td>
   <td><p>Abre o fragmento de formulário no modo de edição.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Propriedades</p> </td>
   <td><p>Fornece opções para modificar as propriedades do fragmento de formulário.<br /> <br /> </p> </td>
    </tr>
    <td><p>Copiar</p> </td>
   <td><p> Fornece opções para copiar o fragmento de formulário e colá-lo no local desejado. <br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>Visualização</p> </td>
   <td><p>Fornece opções para visualizar o fragmento como HTML ou executar uma visualização personalizada mesclando dados de um arquivo XML com o fragmento. <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Download</p> </td>
   <td><p>Baixa o fragmento selecionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Iniciar revisão/Gerenciar revisão</p> </td>
   <td><p>Permite iniciar e gerenciar uma revisão do fragmento selecionado.<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>Publicar/Desfazer publicação</p> </td>
   <td><p>Publica/cancela a publicação do fragmento selecionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Excluir</p> </td>
   <td><p>Exclui o fragmento selecionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Comparar</p> </td>
   <td><p>Compara dois fragmentos de formulário diferentes para fins de visualização.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## Práticas recomendadas

* Certifique-se de que o nome do fragmento seja exclusivo. O fragmento não é criado se houver um fragmento existente com o mesmo nome.
* Qualquer expressão, script ou estilo em um fragmento de formulário independente é retido quando inserido por referência ou incorporado em um formulário.
* Ao publicar um formulário, os fragmentos de formulário inseridos por referência no formulário são publicados automaticamente.

## Consulte também

{{universal-editor-see-also}}
