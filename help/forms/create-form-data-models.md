---
title: Como criar um modelo de dados de formulário?
description: A integração de dados do Experience Manager Forms oferece uma interface de usuário intuitiva para criar e trabalhar com modelos de dados de formulário. Saiba como criar modelos de dados de formulário com ou sem fontes de dados configuradas.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---

# Criar modelo de dados do formulário {#create-form-data-model}

![Integração de dados](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] a integração de dados oferece uma interface de usuário intuitiva para criar e trabalhar com modelos de dados de formulário. Um modelo de dados de formulário depende de fontes de dados para o intercâmbio de dados; no entanto, é possível criar um Modelo de dados de formulário com ou sem uma fonte de dados. Existem duas abordagens para criar um a partir do modelo de dados, dependendo se você configurou as fontes de dados:

* **Uso de fontes de dados pré-configuradas**: Se você configurou fontes de dados conforme descrito em [Configurar fontes de dados](configure-data-sources.md), é possível selecioná-los ao criar um modelo de dados de formulário. Ele traz todos os objetos, propriedades e serviços do modelo de dados das fontes de dados selecionadas disponíveis para uso no modelo de dados de formulário.

* **Sem fontes de dados**: Se você não tiver configurado fontes de dados para seu modelo de dados de formulário, ainda poderá criá-lo sem fontes de dados. Você pode usar o Modelo de dados de formulário para criar o Forms adaptável <!--and interactive communication--> e testá-los usando dados de amostra. Quando as fontes de dados estão disponíveis, é possível vincular o Modelo de dados de formulário às fontes de dados, o que reflete automaticamente no Forms adaptável associado<!--and interactive communications-->.

>[!NOTE]
>
>Você deve ser um membro de ambos **fdm-author** e **usuário de formulários** para criar e trabalhar com o modelo de dados de formulário. Entre em contato com seu [!DNL Experience Manager] administrador para se tornar membro dos grupos.

## Criar modelo de dados do formulário {#data-sources}

Verifique se você configurou as fontes de dados que pretende usar no Modelo de dados de formulário, conforme descrito em [Configurar fontes de dados](configure-data-sources.md). Faça o seguinte para criar um Modelo de dados de formulário com base em fontes de dados configuradas:

1. Em [!DNL Experience Manager] instância do autor, navegue até **[!UICONTROL Forms > Integrações de dados]**.
1. Toque **[!UICONTROL Criar > Modelo de dados de formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário :

   * Especifique um nome para o modelo de dados de formulário.
   * (**Opcional**) Especifique o título, a descrição e as tags para o modelo de dados de formulário.
   * (**Opcional e aplicável somente se as fontes de dados estiverem configuradas**) Toque no ícone de marca de verificação ao lado do **[!UICONTROL Configuração da Fonte de Dados]** e selecione o nó de configuração onde residem os serviços de nuvem das fontes de dados que você deseja usar. Ele restringe a lista de fontes de dados disponíveis para seleção na próxima página às disponíveis no nó de configuração selecionado. No entanto, qualquer banco de dados JDBC e [!DNL Experience Manager] as fontes de dados do perfil de usuário são listadas por padrão. Se você não selecionar um nó de configuração, as fontes de dados de todos os nós de configuração serão listadas.

1. Toque **[!UICONTROL Próximo]**.

1. (**Aplicável somente se as fontes de dados estiverem configuradas**) **[!UICONTROL Selecionar fonte de dados]** lista as fontes de dados disponíveis, se houver. Selecione fontes de dados que deseja usar no modelo de dados de formulário.
1. Toque **[!UICONTROL Criar]** e na caixa de diálogo de confirmação, toque em **[!UICONTROL Abrir]** para abrir o editor de Modelo de dados de formulário.

   Vamos analisar os diferentes componentes da interface do usuário do editor do Modelo de dados de formulário.

   ![Um Modelo de dados de formulário com três fontes de dados - um serviço RESTful, [!DNL Experience Manager] perfil do usuário e um RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL Fontes de dados]** Lista as fontes de dados em um modelo de dados de formulário. Expanda uma fonte de dados para exibir seus objetos e serviços do modelo de dados.

   B. **[!UICONTROL Atualizar Definições da Fonte de Dados]** Busca todas as alterações nas definições da fonte de dados de fontes de dados configuradas e as atualiza na guia Fontes de dados do editor do Modelo de dados de formulário.

   C. **[!UICONTROL Modelo]** Área de conteúdo na qual os objetos de modelo de dados adicionados são exibidos.

   D. **[!UICONTROL Serviços]** Área de conteúdo onde são exibidas operações ou serviços de fonte de dados adicionados.

   E. **[!UICONTROL Barra de ferramentas]** Ferramentas para trabalhar com o modelo de dados de formulário. A barra de ferramentas mostra mais opções dependendo do objeto selecionado no modelo de dados de formulário.

   F. **[!UICONTROL Adicionar Selecionado]** Adiciona objetos e serviços de modelo de dados selecionados ao modelo de dados de formulário.

Para obter mais informações sobre o editor de Modelo de dados de formulário e como trabalhar com ele para editar e configurar o modelo de dados de formulário, consulte [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md).

## Atualizar fontes de dados {#update}

Faça o seguinte para adicionar ou atualizar fontes de dados a um modelo de dados de formulário existente.

1. Ir para **[!UICONTROL Forms > Integrações de dados]**, selecione o Modelo de dados de formulário no qual deseja adicionar ou atualizar fontes de dados e toque em **[!UICONTROL Propriedades]**.
1. Nas propriedades do Modelo de dados de formulário, acesse **[!UICONTROL Atualizar origem]** guia .

   No **[!UICONTROL Atualizar origem]** guia :

   * Toque no ícone de navegação na **[!UICONTROL Configuração sensível ao contexto]** e selecione um nó de configuração em que reside a configuração da nuvem para a fonte de dados que você deseja adicionar. Se você não selecionar um nó, as configurações de nuvem residentes somente na variável `global` são listados ao tocar **[!UICONTROL Adicionar fontes]**.

   * Para adicionar uma nova fonte de dados, toque em **[!UICONTROL Adicionar fontes]** e selecione as fontes de dados a serem adicionadas ao modelo de dados do formulário. Todas as fontes de dados configuradas em `global` e o nó de configuração selecionado, se houver, serão exibidos.

   * Para substituir uma fonte de dados existente por outra fonte de dados do mesmo tipo, toque no **[!UICONTROL Editar]** ícone para a fonte de dados e selecione na lista de fontes de dados disponíveis.
   * Para excluir uma fonte de dados existente, toque no **[!UICONTROL Excluir]** ícone para a fonte de dados. O ícone Excluir será desativado se um objeto de modelo de dados na fonte de dados for adicionado ao modelo de dados de formulário.

      ![fdm-properties](assets/fdm-properties.png)

1. Toque **[!UICONTROL Salvar e fechar]** para salvar as atualizações.

>[!NOTE]
>
>Depois de adicionar novas fontes de dados ou atualizar as fontes de dados existentes em um modelo de dados de formulário, atualize as referências de vínculo, conforme apropriado, no Adaptive Forms<!--and interactive communications--> que usam o modelo de dados de formulário atualizado.

## Próximas etapas {#next-steps}

Agora, você tem um Modelo de dados de formulário com fontes de dados adicionadas a ele. Em seguida, edite o Modelo de dados de formulário para adicionar e configurar objetos e serviços do modelo de dados, adicionar associações entre objetos do modelo de dados, editar propriedades, adicionar objetos e propriedades do modelo de dados personalizado, gerar dados de amostra e assim por diante.

Para obter mais informações, consulte [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md).
