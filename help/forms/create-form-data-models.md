---
title: Como criar o Modelo de dados de formulário (FDM)?
description: Saiba como criar um modelo de dados de formulário (FDM) e enviar ou recuperar dados para uma fonte de dados usando um formulário adaptável ou um fluxo de trabalho do AEM.
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 1%

---

# Criar modelo de dados de formulário (FDM) {#create-form-data-model}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) |
| AEM as a Cloud Service | Este artigo |


![Integração de dados](do-not-localize/data-integeration.png)

A integração de dados do [!DNL Experience Manager Forms] fornece uma interface de usuário intuitiva para criar e trabalhar com modelos de dados de formulário. Um Modelo de dados de formulário (FDM) depende de fontes de dados para troca de dados; no entanto, você pode criar um Modelo de dados de formulário (FDM) com ou sem uma fonte de dados. Há duas abordagens para criar um a partir do modelo de dados, dependendo se você configurou as fontes de dados:

* **Usando fontes de dados pré-configuradas**: se você tiver configurado as fontes de dados conforme descrito em [Configurar fontes de dados](configure-data-sources.md), poderá selecioná-las ao criar um modelo de dados de formulário (FDM). Ele traz todos os objetos, propriedades e serviços do modelo de dados das fontes de dados selecionadas disponíveis para uso no modelo de dados de formulário (FDM).

* **Sem fontes de dados**: se você não tiver configurado fontes de dados para seu modelo de dados de formulário (FDM), ainda poderá criá-lo sem fontes de dados. Você pode usar o Modelo de Dados de Formulário (FDM) para criar o Forms Adaptável <!--and interactive communication--> e testá-los usando dados de amostra. Quando as fontes de dados estiverem disponíveis, você poderá vincular o Modelo de Dados de Formulário (FDM) às fontes de dados, o que refletirá automaticamente no Forms Adaptável associado<!--and interactive communications-->.

>[!NOTE]
>
>Você deve ser membro de ambos os grupos **fdm-author** e **forms-user** para poder criar e trabalhar com o modelo de dados de formulário (FDM). Contate o administrador do [!DNL Experience Manager] para se tornar um membro dos grupos.

## Criar modelo de dados de formulário (FDM) {#data-sources}

Verifique se você configurou as fontes de dados que pretende usar no Modelo de Dados de Formulário (FDM) conforme descrito em [Configurar fontes de dados](configure-data-sources.md). Faça o seguinte para criar um Modelo de dados de formulário (FDM) com base nas fontes de dados configuradas:

1. Na instância do autor [!DNL Experience Manager], navegue até **[!UICONTROL Forms > Integrações de dados]**.
1. Selecione **[!UICONTROL Criar > Modelo de dados de formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário:

   * Especifique um nome para o modelo de dados de formulário (FDM).
   * (**Opcional**) Especifique o título, a descrição e as marcas para o modelo de dados de formulário (FDM).
   * (**Opcional e aplicável somente se as fontes de dados estiverem configuradas**) Selecione o ícone de marca de verificação ao lado do campo **[!UICONTROL Configuração do Data Source]** e selecione o nó de configuração onde residem os serviços em nuvem para as fontes de dados que você deseja usar. Ele restringe a lista de origens de dados disponíveis para seleção na próxima página às disponíveis no nó de configuração selecionado. No entanto, todas as fontes de dados de perfil de usuário do [!DNL Experience Manager] são listadas por padrão. Se você não selecionar um nó de configuração, as origens de dados de todos os nós de configuração serão listadas.

1. Selecione **[!UICONTROL Próximo]**.

1. (**Aplicável somente se as fontes de dados estiverem configuradas**) A tela **[!UICONTROL Selecionar Fonte de Dados]** lista as fontes de dados disponíveis, se houver. Selecione as fontes de dados que deseja usar no modelo de dados do formulário.
1. Selecione **[!UICONTROL Criar]** e, na caixa de diálogo de confirmação, selecione **[!UICONTROL Abrir]** para abrir o editor de Modelo de Dados de Formulário.

   Vamos revisar os diferentes componentes da interface do editor do Modelo de dados de formulário.

   ![Um Modelo de Dados de Formulário com três fontes de dados - um serviço RESTful, [!DNL Experience Manager] perfil de usuário e um RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL Fontes de dados]** Lista as fontes de dados em um modelo de dados de formulário. Expanda uma fonte de dados para exibir seus objetos de modelo de dados e serviços.

   B. **[!UICONTROL Atualizar Definições do Data Source]** Busca todas as alterações nas definições de fonte de dados das fontes de dados configuradas e as atualiza na guia Fontes de Dados do editor de Modelo de Dados de Formulário.

   C. **[!UICONTROL Modelo]** Área de conteúdo na qual os objetos de modelo de dados adicionados aparecem.

   D. **[!UICONTROL Serviços]** Área de conteúdo em que aparecem as operações ou os serviços da fonte de dados adicionados.

   E. **[!UICONTROL Barra de ferramentas]** Ferramentas para trabalhar com o modelo de dados de formulário (FDM). A barra de ferramentas mostra mais opções dependendo do objeto selecionado no modelo de dados de formulário (FDM).

   F. **[!UICONTROL Adicionar Selecionados]** Adiciona objetos e serviços de modelo de dados selecionados ao modelo de dados de formulário.

Para obter mais informações sobre o editor do Modelo de Dados de Formulário e como trabalhar com ele para editar e configurar o modelo de dados de formulário (FDM), consulte [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md).

## Atualizar fontes de dados {#update}

Faça o seguinte para adicionar ou atualizar fontes de dados a um modelo de dados de formulário (FDM) existente.

1. Vá para **[!UICONTROL Forms > Integrações de Dados]**, selecione o Modelo de Dados de Formulário (FDM) no qual deseja adicionar ou atualizar fontes de dados e selecione **[!UICONTROL Propriedades]**.
1. Nas propriedades do modelo de dados de formulário, vá para a guia **[!UICONTROL Atualizar Source]**.

   Na guia **[!UICONTROL Atualizar Source]**:

   * Selecione o ícone de procura no campo **[!UICONTROL Configuração sensível ao contexto]** e selecione um nó de configuração em que esteja a configuração em nuvem da fonte de dados que você deseja adicionar. Se você não selecionar um nó, as configurações de nuvem que residem somente no nó `global` serão listadas quando você selecionar **[!UICONTROL Adicionar Fontes]**.

   * Para adicionar uma nova fonte de dados, selecione **[!UICONTROL Adicionar Fontes]** e selecione as fontes de dados a serem adicionadas ao modelo de dados de formulário (FDM). Todas as fontes de dados configuradas em `global` e o nó de configuração selecionado, se houver, são exibidos.

   * Para substituir uma fonte de dados existente por outra fonte de dados do mesmo tipo, selecione o ícone **[!UICONTROL Editar]** para a fonte de dados e selecione na lista de fontes de dados disponíveis.
   * Para excluir uma fonte de dados existente, selecione o ícone **[!UICONTROL Excluir]** para a fonte de dados. O ícone Excluir será desativado se um objeto de modelo de dados na fonte de dados for adicionado no modelo de dados de formulário (FDM).

     ![propriedades-fdm](assets/fdm-properties.png)

1. Selecione **[!UICONTROL Salvar e fechar]** para salvar as atualizações.

>[!NOTE]
>
>Depois de adicionar novas fontes de dados ou atualizar fontes de dados existentes em um modelo de dados de formulário (FDM), atualize as referências de associação, conforme apropriado, no Forms Adaptável <!--and interactive communications--> que usa o modelo de dados de formulário (FDM) atualizado.

## Configurações sensíveis ao contexto para modos de execução específicos {#runmode-specific-context-aware-config}

O [!UICONTROL Modelo de Dados de Formulário (FDM)] usa [configurações com reconhecimento de contexto do Sling](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) para oferecer suporte a diferentes parâmetros de fonte de dados para conexão com fontes de dados para diferentes modos de execução [!DNL Experience Manager].

Quando o [!UICONTROL Modelo de Dados de Formulário (FDM)] usa configurações de nuvem para armazenar parâmetros, que, ao ser submetido a check-in e implantado por meio do controle do código-fonte (repositório GIT do Cloud-Manager), cria configurações de nuvem com os mesmos parâmetros para todos os modos de execução (Desenvolvimento, Preparo e Produção). No entanto, para casos de uso em que há necessidade de ter conjuntos de dados diferentes para ambientes de teste e produção, usamos parâmetros de fonte de dados (por exemplo, URL da fonte de dados) para diferentes modos de execução do [!DNL Experience Manager].

Para fazer isso, você precisa criar uma configuração OSGi que contenha pares de parâmetros-valores da fonte de dados. Isso substitui o mesmo par da configuração de nuvem do [!UICONTROL Modelo de Dados de Formulário (FDM)] em tempo de execução. Como as configurações do OSGi são compatíveis com esses modos de execução por padrão, é possível substituir um parâmetro de fonte de dados por valores diferentes com base no modo de execução.

Para habilitar configurações de nuvem específicas da implantação no [!UICONTROL Modelo de Dados de Formulário (FDM)]:

1. Criar configuração de nuvem na instância de desenvolvimento local. Para obter etapas detalhadas, consulte [Como configurar fontes de dados](/help/forms/configure-data-sources.md).

1. Armazene a configuração da nuvem no sistema de arquivos.
   1. Criar pacote com filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Use o mesmo `{foldername}` da etapa 1. E substitua `fdm` por `azurestorage` para configuração de armazenamento do Azure.
   1. Criar e baixar pacote. Para obter detalhes, consulte [ações do pacote](/help/implementing/developing/tools/package-manager.md).

1. Integrar configuração de nuvem no Projeto do Arquétipo [!DNL Experience Manager].
   1. Descompacte o pacote baixado.
   1. Copie a pasta `jcr_root` e coloque-a como `ui.content` > `src` > `main` > `content`.
   1. Atualize `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` para conter o filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Para obter detalhes, consulte o [módulo ui.content do Arquétipo de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). Quando esse projeto de arquétipo é implantado por meio do pipeline CM, a mesma configuração de nuvem é instalada em todos os ambientes (ou modos de execução). Para alterar o valor de campos (como URL) das configurações de nuvem com base no ambiente, use a configuração OSGi discutida na etapa a seguir.

1. Crie uma configuração com reconhecimento de contexto do Apache Sling. Para criar a configuração OSGi:
   1. **Configure os arquivos de configuração OSGi no projeto do Arquétipo [!DNL Experience Manager].**
Crie arquivos de Configuração de Fábrica OSGi com PID `org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. Crie um arquivo com o mesmo nome em cada pasta de modo de execução, onde os valores precisam ser alterados por modo de execução. Para obter detalhes, consulte [Configurar OSGi para [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **Defina o json de configuração OSGI.** Para usar o provedor de substituição de configuração sensível ao contexto do Apache Sling:
      1. Na instância de desenvolvimento local `/system/console/configMgr`, selecione a configuração OSGi de fábrica com o nome **[!UICONTROL Provedor de Substituição de Configuração com Reconhecimento de Contexto Apache Sling: configuração OSGi]**.
      1. Forneça a descrição.
      1. Selecione **[!UICONTROL habilitado]**.
      1. Em substituições, forneça campos que precisam ser alterados com base no ambiente na sintaxe de substituição do sling. Para obter detalhes, consulte [Configuração com reconhecimento de contexto do Apache Sling - Substituição](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). Por exemplo, `cloudconfigs/fdm/{configName}/url="newURL"`.
Várias substituições podem ser adicionadas selecionando **[!UICONTROL +]**.
      1. Selecione **[!UICONTROL Salvar]**.
      1. Para obter o JSON de Configuração OSGi, siga as etapas em [Geração de Configurações OSGi usando o Quickstart do AEM SDK](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. Coloque o JSON nos arquivos de configuração de fábrica OSGi criados na etapa anterior.
      1. Alterar o valor de `newURL` com base no ambiente (ou modo de execução).
      1. Para alterar o valor secreto com base no modo de execução, a variável secreta pode ser criada usando a [API do Cloud Manager](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e posterior, e pode ser referenciada na [Configuração OSGi](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
Quando esse projeto de arquétipo é implantado por meio do pipeline CM, a substituição fornecerá valores diferentes em ambientes diferentes (ou modo de execução).

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] usuários podem criptografar os valores secretos usando o suporte de criptografia para obter detalhes. Consulte [suporte de criptografia para propriedades de configuração](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) e coloque o texto criptografado no valor após [configurações com reconhecimento de contexto estarem disponíveis no service pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. Atualize as definições de fonte de dados usando a opção para atualizar as definições de fonte de dados no [Editor de Modelo de Dados de Formulário](#data-sources) para atualizar o cache do FDM por meio da interface do FDM e obter a configuração mais recente.

## Próximas etapas {#next-steps}

Agora você tem um Modelo de dados de formulário (FDM) com fontes de dados adicionadas a ele. Em seguida, edite o Modelo de Dados de Formulário (FDM) para adicionar e configurar objetos e serviços de modelo de dados, adicionar associações entre objetos de modelo de dados, editar propriedades, adicionar objetos e propriedades de modelo de dados personalizados, gerar dados de amostra e assim por diante.

Para obter mais informações, consulte [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md).


