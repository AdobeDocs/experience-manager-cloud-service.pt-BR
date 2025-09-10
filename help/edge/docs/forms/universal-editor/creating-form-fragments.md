---
title: Como criar fragmentos de formulário para criação com base no WYSIWYG
description: Saiba como criar fragmentos de formulário no Editor universal e adicioná-los a formulários.
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 1%

---

# Criação de fragmentos de formulário no Editor universal

Os fragmentos de formulário são componentes reutilizáveis que eliminam o trabalho de desenvolvimento repetitivo e garantem a consistência entre os formulários de sua organização. Em vez de recriar seções comuns, como informações de contato, detalhes de endereço ou contratos de consentimento para cada formulário, você pode criar esses elementos uma vez como fragmentos e reutilizá-los em vários formulários.

**O que você realizará neste artigo:**

- Compreender o valor comercial e os recursos técnicos dos fragmentos de formulário
- Criar fragmentos de formulário reutilizáveis usando o Editor universal
- Integrar fragmentos em formulários existentes com a configuração adequada
- Gerenciar o ciclo de vida do fragmento e manter a consistência entre formulários

**Benefícios para os negócios:**

- **Tempo de desenvolvimento reduzido**: criar seções de formulário comuns uma vez, reutilizar em todos os lugares
- **Consistência aprimorada**: layouts e conteúdo padronizados em todos os formulários
- **Manutenção simplificada**: atualize um fragmento uma vez para refletir as alterações em todos os formulários que o utilizam
- **Conformidade aprimorada**: garanta que as seções normativas permaneçam consistentes e atualizadas

Os fragmentos de formulário no Edge Delivery Services oferecem suporte a recursos avançados, incluindo fragmentos aninhados, várias instâncias em um único formulário e integração contínua com fontes de dados.

## Noções básicas sobre fragmentos de formulário

Os fragmentos de formulário no Edge Delivery Services fornecem recursos avançados para o desenvolvimento de formulários modulares:

**Principais recursos:**

- **Gerenciamento de consistência**: os fragmentos mantêm layouts e conteúdo idênticos em vários formulários. Com uma abordagem &quot;alterar uma vez, refletir em qualquer lugar&quot;, as atualizações de um fragmento são automaticamente aplicadas a todos os formulários no modo Visualização.
- **Uso múltiplo**: adicione o mesmo fragmento várias vezes em um único formulário, cada um com dados independentes associados a diferentes fontes de dados ou elementos de esquema.
- **Estruturas aninhadas**: crie hierarquias complexas incorporando fragmentos a outros fragmentos para arquiteturas de formulário sofisticadas.

**Requisitos técnicos:**

- **Consistência de URL do GitHub**: o fragmento e qualquer formulário que o utilize devem especificar a mesma URL de repositório do GitHub
- **Edição independente**: os fragmentos só podem ser modificados em sua forma independente; as alterações não podem ser feitas no formulário do host

**Comportamento da publicação:**

>[!IMPORTANT]
>
>No modo de Visualização, as alterações no fragmento refletem imediatamente em todos os formulários. No modo Publicar, você deve republicar o fragmento e quaisquer formulários que o usem para ver as atualizações.

>[!CAUTION]
>
>Evite referências de fragmento recursivas (aninhar um fragmento dentro de si mesmo), pois isso causa erros de renderização e comportamento inesperado.

## Pré-requisitos

**Requisitos de configuração técnica:**

- [Repositório GitHub configurado](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) com conexão estabelecida entre seu ambiente AEM e o repositório GitHub
- [Bloco Adaptive Forms mais recente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) adicionado ao seu repositório GitHub (para projetos Edge Delivery Services existentes)
- Instância do autor do AEM Forms com modelo do Edge Delivery Services disponível
- Acesso ao URL da instância do autor do AEM Forms as a Cloud Service e ao URL do repositório do GitHub

**Conhecimentos e permissões necessários:**

- Compreensão básica de conceitos de design de formulário e hierarquia de componentes
- Familiaridade com a interface do Editor universal e workflows de criação de formulários
- Permissões no nível do autor no AEM Forms para criar e gerenciar ativos de formulário
- Noções básicas sobre os padrões de formulários de sua organização e requisitos de componentes reutilizáveis

## Trabalhar com fragmentos de formulário do Edge Delivery Services

Você pode criar fragmentos de formulário do Edge Delivery Services no Editor universal e adicionar os fragmentos criados aos formulários do Edge Delivery Services. Você pode executar as seguintes ações com os fragmentos de formulário do Edge Delivery Services:

- [Criação de fragmentos de formulário no Editor universal](#creating-form-fragments-in-universal-editor)
   - [Noções básicas sobre fragmentos de formulário](#understanding-form-fragments)
   - [Pré-requisitos](#prerequisites)
   - [Trabalhar com fragmentos de formulário do Edge Delivery Services](#working-with-edge-delivery-services-form-fragments)
   - [Práticas recomendadas](#best-practices)
   - [Resumo](#summary)

+++ Criação de fragmentos de formulário

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

   - **Modelo de dados de formulário (FDM)**: integre objetos de modelo de dados e serviços de fontes de dados ao seu fragmento. Escolha Modelo de dados de formulário (FDM) se o formulário exigir leitura e gravação de dados de várias fontes.

   - **Esquema JSON**: integre seu formulário a um sistema de back-end associando um esquema JSON que define a estrutura de dados. Ela permite adicionar conteúdo dinâmico usando os elementos do esquema.
   - **Nenhum**: especifica criar o fragmento do zero sem usar nenhum modelo de formulário.

   >[!NOTE]
   >
   > Para saber como integrar formulários ou fragmentos a um Modelo de dados de formulário (FDM) no Editor Universal para usar fontes de dados de back-end diversas, consulte [Integrar formulários com o Modelo de dados de formulário no Editor Universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Opcional) Especifique a **Data de publicação** ou a **Data de cancelamento da publicação** do fragmento na guia **Avançado**.

   ![Guia Avançado](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Clique em **Criar** para gerar o fragmento. Uma caixa de diálogo de sucesso é exibida com opções de edição.

   ![Editar fragmento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Clique em **Editar** para abrir o fragmento no Universal Editor com o modelo padrão aplicado.

   ![Fragmento no Editor Universal para criação](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **Crie o conteúdo do fragmento**: adicione componentes de formulário (campos de texto, listas suspensas, caixas de seleção) para criar a seção reutilizável. Para obter orientações detalhadas sobre componentes, consulte [Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

1. **Configurar propriedades do componente**: defina nomes de campos, regras de validação e valores padrão conforme necessário para o caso de uso.

1. **Salvar e visualizar**: salve o fragmento e use o modo de Visualização para verificar o layout e a funcionalidade.

   ![Captura de tela de um fragmento de formulário de detalhes do contato concluído no Editor Universal, mostrando campos para nome, telefone, email e endereço que podem ser reutilizados em vários formulários](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**Ponto de verificação de validação:**

- Carregamento de fragmento sem erros no Universal Editor
- Todos os componentes do formulário são renderizados corretamente
- As propriedades de campo e as regras de validação funcionam conforme esperado
- O fragmento é salvo e está disponível no console Forms e documentos

Depois que o fragmento for concluído, você poderá [integrá-lo a qualquer formulário do Edge Delivery Services](#adding-form-fragments-to-a-form).

+++


+++ Adição de fragmentos de formulário a um formulário

Este exemplo demonstra a criação de um formulário `Employee Details` que usa o fragmento `Contact Details` para as seções de informações do funcionário e do supervisor. Essa abordagem garante uma coleta de dados consistente e, ao mesmo tempo, reduz o esforço de desenvolvimento.

Para integrar um fragmento de formulário ao formulário:

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

   O fragmento de formulário é adicionado por referência ao formulário e permanece sincronizado com o fragmento de formulário independente.

   ![Captura de tela mostrando o fragmento de detalhes do contato integrado com êxito em um formulário de funcionário no Universal Editor, demonstrando como os fragmentos mantêm sua estrutura quando reutilizados](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   >[!NOTE]
   >
   > O botão **Editar fragmento** permite que os usuários naveguem diretamente para o fragmento do formulário para edição.

   Você pode visualizar o formulário para ver como ele aparece no modo **Visualização**.

   ![Visualização](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Da mesma forma, você pode repetir as Etapas de 3 a 7 para inserir o fragmento `Contact Details` para o painel `Supervisor Details`.

   ![Formulário Detalhes do Funcionário](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ Gerenciamento de fragmentos de formulário

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

+++ 

## Práticas recomendadas

**Design e nomenclatura do fragmento:**

- **Usar nomes descritivos e exclusivos**: escolha nomes que indiquem claramente a finalidade do fragmento (por exemplo, &quot;detalhes de contato com validação&quot; em vez de &quot;fragmento1&quot;)
- **Planejar reutilização**: crie fragmentos para que eles sejam independentes de contexto para que funcionem em diferentes tipos de formulário
- **Manter fragmentos focalizados**: crie fragmentos de finalidade única em vez de componentes complexos de várias funções

**Fluxo de trabalho de desenvolvimento:**

- **Testar fragmentos independentemente**: verifique a funcionalidade do fragmento antes de integrar a formulários
- **Manter URLs consistentes do GitHub**: verifique se a mesma URL de repositório é usada em todos os fragmentos e formulários relacionados
- **Finalidade do fragmento do documento**: incluir descrições e marcas claras para ajudar os membros da equipe a entender quando usar cada fragmento

**Publicação e manutenção:**

- **Coordenar publicação**: ao atualizar fragmentos, planeje republicar todos os formulários dependentes simultaneamente
- **Controle de versão**: usar mensagens de confirmação relevantes ao atualizar fragmentos para rastrear alterações ao longo do tempo
- **Monitorar dependências**: controle quais formulários usam cada fragmento para avaliar o impacto da atualização

>[!TIP]
>
>Os estilos de fragmento, scripts e expressões são preservados quando incorporados, portanto, o design deve ter essa herança em mente.

## Resumo

Você aprendeu com sucesso a usar os fragmentos de formulário no Edge Delivery Services para melhorar a eficiência do desenvolvimento e manter a consistência nos formulários de sua organização.

**Principais realizações:**

- **Noções básicas**: o valor comercial e os recursos técnicos dos fragmentos de formulário foram obtidos
- **Criação**: fragmentos de formulário reutilizáveis compilados usando o Editor Universal com configuração adequada
- **Integração**: adição de fragmentos a formulários com configuração de propriedade e configuração de referência corretas
- **Gerenciamento**: operações de ciclo de vida de fragmento exploradas e fluxos de trabalho de manutenção

**Próximas etapas:**

- Crie uma biblioteca de fragmentos usados com frequência para sua organização.
- Estabeleça convenções de nomenclatura e políticas de governança para o uso de fragmentos.
- Explore uma integração avançada com os [Modelos de dados de formulário](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) para fragmentos dinâmicos orientados por dados
- Implemente modelos de formulário baseados em fragmento para obter experiências consistentes do usuário.

Seus formulários agora se beneficiam de uma arquitetura modular e que pode ser dimensionada com eficiência entre os projetos, garantindo ao mesmo tempo experiências consistentes do usuário.


