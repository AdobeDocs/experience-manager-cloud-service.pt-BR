---
title: Como criar o modelo de dados de formulário?
description: Saiba como criar um modelo de dados de formulário (FDM) e enviar ou recuperar dados para uma fonte de dados usando um Formulário adaptável ou um Fluxo de trabalho do AEM.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: e2f2aa18e2412bc92d1385a125281ecfb81f2ce8
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 1%

---

# Criar modelo de dados do formulário {#create-form-data-model}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) |
| AEM as a Cloud Service | Este artigo |


![Integração de dados](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] a integração de dados fornece uma interface de usuário intuitiva para criar e trabalhar com modelos de dados de formulário. Um modelo de dados de formulário depende de fontes de dados para troca de dados; no entanto, você pode criar um modelo de dados de formulário com ou sem uma fonte de dados. Há duas abordagens para criar um a partir do modelo de dados, dependendo se você configurou as fontes de dados:

* **Uso de fontes de dados pré-configuradas**: Se você tiver configurado as fontes de dados conforme descrito em [Configurar fontes de dados](configure-data-sources.md), você pode selecioná-los ao criar um modelo de dados de formulário. Ele traz todos os objetos, propriedades e serviços do modelo de dados das fontes de dados selecionadas disponíveis para uso no modelo de dados de formulário.

* **Sem fontes de dados**: se você não tiver configurado as fontes de dados para o seu modelo de dados de formulário, ainda será possível criá-lo sem fontes de dados. Você pode usar o modelo de dados de formulário para criar o Forms adaptável <!--and interactive communication--> e testá-los usando dados de amostra. Quando as fontes de dados estiverem disponíveis, você poderá vincular o Modelo de dados de formulário às fontes de dados, o que refletirá automaticamente no Forms adaptável associado<!--and interactive communications-->.

>[!NOTE]
>
>Você deve ser membro de ambos **fdm-author** e **forms-user** grupos para poder criar e trabalhar com o modelo de dados de formulário. Entre em contato com [!DNL Experience Manager] administrador para se tornar um membro dos grupos.

## Criar modelo de dados do formulário {#data-sources}

Verifique se você configurou as fontes de dados que pretende usar no Modelo de dados do formulário conforme descrito em [Configurar fontes de dados](configure-data-sources.md). Faça o seguinte para criar um modelo de dados de formulário com base nas fontes de dados configuradas:

1. Entrada [!DNL Experience Manager] instância do autor, navegue até **[!UICONTROL Forms > Integrações de dados]**.
1. Toque **[!UICONTROL Criar > Modelo de dados do formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário:

   * Especifique um nome para o modelo de dados de formulário.
   * (**Opcional**) Especifique o título, a descrição e as tags para o modelo de dados de formulário.
   * (**Opcional e aplicável somente se as fontes de dados estiverem configuradas**) Toque no ícone de marca de verificação ao lado da **[!UICONTROL Configuração da fonte de dados]** e selecione o nó de configuração onde residem os serviços em nuvem para as fontes de dados que deseja usar. Ele restringe a lista de origens de dados disponíveis para seleção na próxima página às disponíveis no nó de configuração selecionado. No entanto, qualquer [!DNL Experience Manager] as origens de dados do perfil do usuário são listadas por default. Se você não selecionar um nó de configuração, as origens de dados de todos os nós de configuração serão listadas.

1. Toque **[!UICONTROL Próxima]**.

1. (**Aplicável somente se as fontes de dados estiverem configuradas**) O **[!UICONTROL Selecionar fonte de dados]** lista as fontes de dados disponíveis, se houver. Selecione as fontes de dados que deseja usar no modelo de dados do formulário.
1. Toque **[!UICONTROL Criar]** e na caixa de diálogo de confirmação, toque em **[!UICONTROL Abertura]** para abrir o editor do Modelo de dados de formulário.

   Vamos revisar os diferentes componentes da interface do editor do Modelo de dados de formulário.

   ![Um modelo de dados de formulário com três fontes de dados - um serviço RESTful, [!DNL Experience Manager] perfil de usuário e um RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL Fontes de dados]** Lista as fontes de dados em um modelo de dados de formulário. Expanda uma fonte de dados para exibir seus objetos de modelo de dados e serviços.

   B. **[!UICONTROL Atualizar definições de fonte de dados]** Busca todas as alterações nas definições de fonte de dados das fontes de dados configuradas e as atualiza na guia Fontes de dados do editor de modelo de dados de formulário.

   C **[!UICONTROL Modelo]** Área de conteúdo em que os objetos de modelo de dados adicionados aparecem.

   D. **[!UICONTROL Serviços]** Área de conteúdo onde aparecem as operações ou os serviços da fonte de dados adicionados.

   E **[!UICONTROL Barra de ferramentas]** Ferramentas para trabalhar com o modelo de dados de formulário. A barra de ferramentas mostra mais opções dependendo do objeto selecionado no modelo de dados de formulário.

   F **[!UICONTROL Adicionar selecionado]** Adiciona objetos de modelo de dados e serviços selecionados ao modelo de dados de formulário.

Para obter mais informações sobre o editor do Modelo de dados de formulário e como você pode trabalhar com ele para editar e configurar o modelo de dados de formulário, consulte [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md).

## Atualizar fontes de dados {#update}

Faça o seguinte para adicionar ou atualizar fontes de dados a um modelo de dados de formulário existente.

1. Ir para **[!UICONTROL Forms > Integrações de dados]**, selecione o Modelo de dados de formulário no qual deseja adicionar ou atualizar fontes de dados e toque em **[!UICONTROL Propriedades]**.
1. Nas propriedades do Modelo de dados de formulário, vá para a **[!UICONTROL Atualizar fonte]** guia.

   No **[!UICONTROL Atualizar fonte]** guia:

   * Toque no ícone de navegação na **[!UICONTROL Configuração sensível ao contexto]** e selecione um nó de configuração em que reside a configuração em nuvem da fonte de dados que deseja adicionar. Se você não selecionar um nó, as configurações de nuvem que residem somente no `global` são listados ao tocar em **[!UICONTROL Adicionar fontes]**.

   * Para adicionar uma nova fonte de dados, toque em **[!UICONTROL Adicionar fontes]** e selecione as fontes de dados a serem adicionadas ao modelo de dados do formulário. Todas as fontes de dados configuradas no `global` e o nó de configuração selecionado, se houver, serão exibidos.

   * Para substituir uma fonte de dados existente por outra do mesmo tipo, toque no **[!UICONTROL Editar]** ícone da fonte de dados e selecione na lista de fontes de dados disponíveis.
   * Para excluir uma fonte de dados existente, toque no **[!UICONTROL Excluir]** ícone da fonte de dados. O ícone Excluir será desativado se um objeto de modelo de dados na fonte de dados for adicionado no modelo de dados de formulário.

     ![fdm-properties](assets/fdm-properties.png)

1. Toque **[!UICONTROL Salvar e fechar]** para salvar as atualizações.

>[!NOTE]
>
>Depois de adicionar novas fontes de dados ou atualizar fontes de dados existentes em um modelo de dados de formulário, atualize as referências de ligação, conforme apropriado, no Adaptive Forms<!--and interactive communications--> que usam o modelo de dados de formulário atualizado.

## Configurações sensíveis ao contexto para modos de execução específicos {#runmode-specific-context-aware-config}

[!UICONTROL Modelo de dados do formulário] utiliza [Configurações sensíveis ao contexto do Sling](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) para oferecer suporte a diferentes parâmetros de origem de dados para conexão com origens de dados para diferentes [!DNL Experience Manager] modos de execução.

Quando [!UICONTROL Modelo de dados do formulário] O usa configurações de nuvem para armazenar parâmetros, que quando verificados e implantados por meio do controle de origem (repositório GIT do Cloud Manager), criam configurações de nuvem com os mesmos parâmetros para todos os modos de execução (Desenvolvimento, Preparo e Produção). No entanto, para casos de uso em que há necessidade de ter conjuntos de dados diferentes para ambientes de teste e produção, usamos parâmetros de fonte de dados (por exemplo, URL da fonte de dados) para diferentes [!DNL Experience Manager] modos de execução.

Para fazer isso, você precisa criar uma configuração OSGi que contenha pares de parâmetros-valores da fonte de dados. Isso substitui o mesmo par de [!UICONTROL Modelo de dados do formulário] configuração da nuvem no tempo de execução. Como as configurações do OSGi são compatíveis com esses modos de execução por padrão, é possível substituir um parâmetro de fonte de dados por valores diferentes com base no modo de execução.

Para habilitar configurações de nuvem específicas para implantação no [!UICONTROL Modelo de dados do formulário]:

1. Criar configuração de nuvem na instância de desenvolvimento local. Para obter etapas detalhadas, consulte [Como configurar fontes de dados](/help/forms/configure-data-sources.md).

1. Armazene a configuração da nuvem no sistema de arquivos.
   1. Criar pacote com filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Usar o mesmo `{foldername}` como na etapa 1. E substituir `fdm` com `azurestorage` para a configuração de armazenamento do Azure.
   1. Criar e baixar pacote. Para obter detalhes, consulte [ações do pacote](/help/implementing/developing/tools/package-manager.md).

1. Integrar configuração de nuvem no [!DNL Experience Manager] Projeto Arquétipo.
   1. Descompacte o pacote baixado.
   1. Copiar `jcr_root` e coloque-a como sua `ui.content` > `src` > `main` > `content`.
   1. Atualizar `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` filtro para conter `/conf/{foldername}/settings/cloudconfigs/fdm`. Para obter detalhes, consulte [Módulo ui.content do Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). Quando esse projeto de arquétipo é implantado por meio do pipeline CM, a mesma configuração de nuvem é instalada em todos os ambientes (ou modos de execução). Para alterar o valor de campos (como URL) das configurações de nuvem com base no ambiente, use a configuração OSGi discutida na etapa a seguir.

1. Crie uma configuração com reconhecimento de contexto do Apache Sling. Para criar a configuração OSGi:
   1. **Configurar os arquivos de configuração do OSGi no [!DNL Experience Manager] Projeto do arquétipo.**
Criar arquivos de configuração de fábrica OSGi com PID `org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. Crie um arquivo com o mesmo nome em cada pasta de modo de execução, onde os valores precisam ser alterados por modo de execução. Para obter detalhes, consulte [Configuração do OSGi para [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **Defina o json de configuração OSGI.** Para usar o provedor de substituição de configuração com reconhecimento de contexto do Apache Sling:
      1. Na instância de desenvolvimento local `/system/console/configMgr`, selecione a configuração OSGi de fábrica com o nome **[!UICONTROL Provedor de substituição de configuração com reconhecimento de contexto do Apache Sling: configuração OSGi]**.
      1. Forneça a descrição.
      1. Selecionar **[!UICONTROL habilitado]**.
      1. Em substituições, forneça campos que precisam ser alterados com base no ambiente na sintaxe de substituição do sling. Para obter detalhes, consulte [Configuração sensível ao contexto do Apache Sling - Substituir](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). Por exemplo, `cloudconfigs/fdm/{configName}/url="newURL"`.
Várias sobreposições podem ser adicionadas selecionando **[!UICONTROL +]**.
      1. Selecione **[!UICONTROL Salvar]**.
      1. Para obter o JSON de configuração do OSGi, siga as etapas em [Gerar configurações OSGi usando o Quickstart do SDK do AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. Coloque o JSON nos arquivos de configuração de fábrica OSGi criados na etapa anterior.
      1. Altere o valor de `newURL` com base no ambiente (ou modo de execução).
      1. Para alterar o valor do segredo com base no modo de execução, a variável do segredo pode ser criada usando [API do cloud manager](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e posterior podem ser referenciados na variável [Configuração OSGi](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
Quando esse projeto de arquétipo é implantado por meio do pipeline CM, a substituição fornecerá valores diferentes em ambientes diferentes (ou modo de execução).
      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] os usuários podem criptografar os valores secretos usando o suporte de criptografia (para obter detalhes, consulte [suporte de criptografia para propriedades de configuração](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) e colocar texto criptografado no valor após [as configurações sensíveis ao contexto estão disponíveis no service pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. Atualize as definições de origem de dados usando a opção para atualizar definições de origem de dados no [Editor de modelo de dados de formulário](#data-sources) para atualizar o cache do FDM por meio da interface do FDM e obter a configuração mais recente.

## Próximas etapas {#next-steps}

Agora você tem um modelo de dados de formulário com fontes de dados adicionadas a ele. Em seguida, você pode editar o Modelo de dados de formulário para adicionar e configurar objetos e serviços de modelo de dados, adicionar associações entre objetos de modelo de dados, editar propriedades, adicionar objetos e propriedades de modelo de dados personalizados, gerar dados de amostra e assim por diante.

Para obter mais informações, consulte [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md).
