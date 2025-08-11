---
title: Criar e publicar Forms adaptável com o Edge Delivery Services
description: Instruções passo a passo para criar, criar e publicar o Adaptive Forms usando o Componente principal ou modelos do Edge Delivery Services no AEM, com foco na precisão e clareza técnicas.
keywords: formulários adaptáveis, serviços de entrega de borda, componentes principais, editor universal, criação de formulários, formulários do AEM, seleção de modelo, publicação de formulários
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 1%

---


# Criar e publicar Forms adaptável com o Edge Delivery Services

Este documento fornece instruções para criar, configurar e publicar o Adaptive Forms no AEM usando o Edge Delivery Services. Ele abrange os modelos do Componente principal e do Edge Delivery Services.

Ao final deste guia, você aprenderá a:

- Selecione o tipo de modelo apropriado para seu caso de uso
- Criar formulários usando os Componentes principais ou modelos do Edge Delivery Services
- Criar formulários usando o editor correto
- Configurar e publicar formulários no Edge Delivery Services
- Acesse os formulários publicados e verifique a implantação

## Seleção de modelo

Antes de começar, determine qual tipo de modelo se alinha aos seus requisitos:

| Critérios | Modelo dos Componentes principais | Modelo do Edge Delivery Services |
|-------------------------|-----------------------------------------|-------------------------------------|
| Melhor para | Fluxos de trabalho corporativos, integrações complexas | Formulários públicos de alto desempenho |
| Editor | Editor Forms adaptável | Editor universal |
| Publicação | AEM Publish + Edge Delivery Services | Somente Edge Delivery Services |
| Complexidade | Recursos avançados de formulário | Formulários rápidos e simplificados |
| Integração | Ecossistema completo do AEM | Desenvolvimento baseado no Git |
| Curva de aprendizagem | Familiarizado com os usuários do AEM | Abordagem moderna e simplificada |

**Diretrizes de decisão:**

![Decisão de Seleção de Modelo](/help/edge/docs/forms/universal-editor/assets/template-selection-decision.svg)

- Use os **Componentes principais** para fluxos de trabalho complexos, integração profunda do AEM ou se estiver aproveitando os ativos existentes do AEM.
- Use o **Edge Delivery Services** para obter desempenho, simplicidade e práticas modernas de desenvolvimento.


*Fluxograma de decisão para escolher o tipo de modelo apropriado*

## Pré-requisitos

Verifique se os seguintes pré-requisitos estão sendo atendidos antes de continuar:

### Requisitos técnicos

- **AEM Forms as a Cloud Service**: uma instância de autor ativa com uma licença do Forms.
- **Conta do GitHub**: conta pessoal ou organizacional para gerenciamento de repositório.
- **Configuração do Repositório**: escolha uma das seguintes opções:
   - **Novo projeto**: [Crie um novo projeto do AEM com Bloco de Forms Adaptável](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block). O repositório é pré-configurado para o Edge Delivery Services.
   - **Projeto existente**: [Adicionar bloco adaptável do Forms a um repositório existente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) e atualizar a configuração.

### Configuração de ambiente

- **Conexão AEM-GitHub**: [Estabeleça uma conexão](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) entre sua instância do AEM e o repositório GitHub.
- **Edge Delivery Services**: verifique se o repositório está configurado para implantação automática.
- **Permissões**: verifique se você tem os direitos de acesso necessários para a criação e publicação de formulários.

### Configurar validação


1. Confirme se o repositório do GitHub contém o bloco adaptável do Forms.
2. Teste a conexão entre o AEM e o repositório GitHub.
3. Certifique-se de publicar conteúdo no Edge Delivery Services.



## Fluxo de trabalho de criação e publicação de formulários

O processo consiste em três fases principais:

- **Fase 1:** [Seleção de Modelo e Criação de Formulário](#step-1-template-selection-and-form-creation)
- **Fase 2:** [Criação e design do formulário](#step-2-form-authoring-and-design)
- **Fase 3:** [Configuração e Publicação](#step-3-configuration-and-publishing)

Cada fase inclui etapas de validação para confirmar a configuração correta.

![Fluxo de Trabalho de Três Fases](/help/edge/docs/forms/universal-editor/assets/three-phase-workflow.svg)
*Visão geral das três fases principais na criação e publicação do formulário*

### Etapa 1: Seleção de Modelo e Criação de Formulário

Selecione o workflow com base na sua escolha de template:

>[!BEGINTABS]

>[!TAB Modelo do Edge Delivery Services]

**Caso de uso:** formulários de alto desempenho e fluxos de trabalho de desenvolvimento modernos.

**Recursos:** criação no Editor Universal e publicação no Edge Delivery Services.

#### Procedimento

1. **Criação do formulário de acesso**
   - Faça logon na instância de autor do AEM Forms as a Cloud Service.
   - Navegue até **Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
   - Clique em **Criar** > **Forms Adaptável**.

1. **Selecionar modelo**
   - Na guia **Source**, selecione um **modelo baseado no Edge Delivery Services**.
   - O botão **Criar** será habilitado.

     ![Criar EDS Forms](/help/edge/assets/create-eds-forms.png)

1. **Configurar Opções (Opcional)**
   - **Guia Data Source**: selecione a integração de dados, se necessário.
   - **Guia Envio**: escolha uma ação de envio (pode ser configurada posteriormente).
   - **Guia Entrega**: definir agendamento de publicação/despublicação.

1. **Concluir configuração do formulário**
   - Clique em **Criar** para abrir o assistente de Criação de Formulário.
   - Insira o seguinte:
      - **Nome**: identificador interno (sem espaços, use hífens).
      - **Título**: nome para exibição do formulário.
      - **URL do GitHub**: URL do repositório (por exemplo, `https://github.com/your-org/your-repo`).

   ![Criar Assistente de Formulário](/help/edge/assets/create-form-wizard.png)

1. **Validação**
   - Depois de clicar em **Criar**, verifique:
      - O formulário é aberto no Universal Editor.
      - O URL do GitHub está vinculado corretamente.
      - A paleta de componentes está disponível.
      - A tela do formulário está visível.

   ![Interface de Editor Universal](/help/edge/assets/author-form.png)

**Resultado:** O formulário está pronto para criação no Editor Universal.

>[!TAB Modelo do Componente Principal]

**Caso de uso:** fluxos de trabalho corporativos e integrações complexas.

**Recursos:** criação do Editor adaptável do Forms, publicação dupla (AEM + Edge Delivery Services), recursos avançados de formulário.

#### Procedimento

1. **Criação do formulário de acesso**
   - Faça logon na instância de autor do AEM Forms as a Cloud Service.
   - Navegue até **Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
   - Clique em **Criar** > **Forms Adaptável**.

1. **Selecionar Modelo e Tema**
   - Na guia **Source**, selecione um **modelo baseado em Componente Principal**.
   - Escolha um **tema** para estilo.
   - O botão **Criar** será habilitado.

   ![Seleção de Modelo de Componente Principal](/help/forms/assets/core-component-based-template.png)

1. **Configurar Opções (Opcional)**
   - **Guia Data Source**: selecione a integração de dados, se necessário.
   - **Guia Envio**: escolha uma ação de envio (pode ser configurada posteriormente).
   - **Guia Entrega**: definir agendamento de publicação/despublicação.

1. **Concluir configuração do formulário**
   - Clique em **Criar** para abrir o assistente de Criação de Formulário.
   - Insira o seguinte:
      - **Nome**: identificador interno (sem espaços, use hífens).
      - **Título**: nome para exibição do formulário.
      - **Caminho**: local de armazenamento no repositório do AEM.

     ![Criar Assistente de Formulário](/help/forms/assets/create-cc-form.png)

1. **Validação**
   - Depois de clicar em **Criar**, verifique:
      - O formulário é aberto no Editor Forms adaptável.
      - A barra de ferramentas do componente está disponível.
      - O painel de propriedades é acessível.
      - O estilo do tema é aplicado.

     ![Editor de formulário adaptável](/help/forms/assets/af-editor-form.png)

**Resultado:** O formulário está pronto para criação no Editor Forms Adaptável.

>[!ENDTABS]

### Etapa 2: criação e design do formulário

A experiência de criação varia de acordo com o modelo:

- **Modelo do Edge Delivery Services**: editor universal
- **Modelo do Componente Principal**: Editor Forms Adaptável

![Comparação do editor](/help/edge/docs/forms/universal-editor/assets/editor-comparison.svg)
*Comparação dos recursos do Editor Universal com o Editor Adaptive Forms*

>[!BEGINTABS]

>[!TAB Editor Universal (Edge Delivery Services)]

**Interface:** edição moderna e otimizada para desempenho.

#### Adicionar componentes de formulário

1. **Acessar Biblioteca de Componentes**
   - Abra o Navegador de conteúdo no Editor universal.
   - Navegue até o componente **Formulário adaptável** na árvore de conteúdo.

   ![Navegação da Árvore de Conteúdo](/help/edge/assets/content-tree.png)

1. **Adicionar campos de formulário**
   - Clique no ícone **Adicionar** para abrir a biblioteca de componentes.
   - Selecione componentes na lista **Componentes de formulários adaptáveis**.
   - Arraste e solte componentes na tela de formulário.

   ![Adicionar componentes](/help/edge/assets/add-component.png)

1. **Criar o formulário**
   - Configure as propriedades do campo no painel de propriedades.
   - Definir regras e comportamentos de validação.
*s Ajuste o estilo e o layout conforme necessário.

   ![Formulário de Registro Concluído](/help/edge/assets/contact-us.png)

#### Validação

- Todos os campos obrigatórios estão presentes.
- As propriedades do campo estão configuradas corretamente.
- O layout é responsivo e acessível.
- As regras de validação funcionam conforme esperado.

#### Próximas etapas

- [Configurar ações de envio](/help/edge/docs/forms/universal-editor/submit-action.md) para manipulação de dados.
- [Guia do Editor Universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) para recursos avançados.

>[!TAB Editor Adaptável do Forms (Componentes Principais)]

**Interface:** edição completa de recursos com recursos de formulário avançados.

#### Adicionar componentes de formulário

1. **Acessar Biblioteca de Componentes**
   - Clique em **Inserir componente** na seção **Arraste componentes aqui**.

   ![Área de Inserção do Componente](/help/forms/assets/drag-components-af-editor.png)

2. **Adicionar campos de formulário**
   - Procure a lista **Componentes de formulários adaptáveis**.
   - Arraste os componentes desejados para o formulário.
   - Use componentes avançados, como painéis, assistentes e integrações de dados.

   ![Adicionar Biblioteca de Componentes](/help/forms/assets/add-component-af.png)

3. **Criar o formulário**
   - Configure as propriedades do campo no painel de propriedades.
   - Definir regras de validação complexas e lógica de negócios.
   - Aplicar temas e estilo avançado.

   ![Formulário de inscrição concluído](/help/forms/assets/af-editor-form.png)

#### Validação

- Todos os campos obrigatórios estão presentes.
- Regras de validação complexas são configuradas.
- O estilo do tema é aplicado.
- A integração de dados funciona conforme o esperado (se aplicável).

#### Próximas etapas

- [Configurar ações de envio](/help/forms/configure-submit-actions-core-components.md) para fluxos de trabalho avançados.
- [Guia dos Componentes principais](/help/forms/creating-adaptive-form-core-components.md) para recursos corporativos.

>[!ENDTABS]

### Etapa 3: configuração e publicação

Configure o Edge Delivery Services e publique seu formulário. O processo difere por tipo de modelo.

#### Configuração do Edge Delivery Services

>[!BEGINTABS]
>[!TAB Modelo do Edge Delivery Services (Automático)]

**Configuração:** Automática (nenhuma configuração manual é necessária).

- A conexão do repositório GitHub e a configuração do Edge Delivery Services são criadas durante a criação do formulário.
- Os endpoints de publicação são configurados automaticamente.

**Verificação:**

- Confirme se a configuração aparece nas configurações do formulário.
- Verifique se o URL do GitHub está vinculado corretamente.

![Configuração automática de EDS](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB Modelo do Componente Principal (Manual)]

**Configuração:** Configuração manual necessária.

#### Etapas de configuração manual

1. **Acessar Ferramentas de Configuração**
   - Navegue até **Ferramentas** > **Serviços na Nuvem** > **Configuração do Edge Delivery Services**.

   ![Acesso à Configuração EDS](/help/edge/assets/select-eds-conf.png)

1. **Criar configuração**
   - Selecione a pasta correspondente ao nome do formulário (por exemplo, `forms/enrollment-form`).
   - Clique em **Criar** > **Configuração**.

   ![Criar configuração de EDS](/help/forms/assets/create-eds-conf.png)

1. **Configurar Propriedades**
   - Clique em **Configuração do Edge Delivery Services**.
   - Selecione **Propriedades** para abrir a caixa de diálogo de configuração.

   ![Propriedades de Configuração](/help/forms/assets/eds-conf.png)

1. **Definir Parâmetros**
   - **Obrigatório:**
      - **Organização**: nome da organização GitHub.
      - **Nome do site**: nome do repositório GitHub.
      - **Ramificação**: nome da ramificação (deixe vazio para principal).
   - **Opcional:**
      - **Host do Edge**: Padrão (publica em .page e .live).
      - **Token de Autenticação do Site**: para autenticação segura (se necessário).

1. **Salvar configuração**
   - Clique em **Salvar e fechar**.

#### Validação

- A configuração foi criada com sucesso.
- A organização e o repositório do GitHub estão especificados corretamente.
- As configurações de ramificação correspondem à estrutura do repositório.
- O formulário aparece na pasta de configuração.

>[!ENDTABS]

#### Publicação do formulário

>[!BEGINTABS]
>[!TAB Publicação do Editor Universal]

**Para Modelos do Edge Delivery Services**

1. No Universal Editor, clique no botão **Publicar** (canto superior direito).
2. Confirme o sucesso da publicação na caixa de diálogo.
3. Observe os URLs gerados para versões preparadas e ativas.

   ![Publicação do Editor Universal](/help/edge/assets/publish-form.png)

- [Guia de publicação](/help/edge/docs/forms/universal-editor/publish-forms.md)

>[!TAB Publicação adaptável do editor do Forms]

1. No console Experience Manager Forms, selecione o formulário a ser publicado.
2. Clique em **[!UICONTROL Publicar]** na barra de ferramentas. Revisar ativos de referência a serem publicados.

![Publicar formulário no Editor de formulário adaptável](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> Consulte [Gerenciar publicação no Experience Manager Forms](/help/forms/manage-publication.md) para obter detalhes.

>[!ENDTABS]

## URLs de formulário

Os formulários publicados podem ser acessados por meio das URLs do Edge Delivery Services.

### Estrutura do URL

- **Preparado (Visualização/Teste):**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **Ao vivo (Produção):**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### Parâmetros de URL

- `<branch>`: nome da ramificação do GitHub (por exemplo, `main`, `develop`)
- `<repo>`: nome do repositório GitHub (por exemplo, `my-forms-project`)
- `<owner>`: Organização ou nome de usuário do GitHub (por exemplo, `company-name`)
- `<form_name>`: Identificador de formulário conforme definido no AEM (por exemplo, `contact-us`)

#### Exemplo

Exemplo do formulário `contact-us` no repositório `forms-project` na organização `acme-corp`:

- **Preparado:** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **Ao vivo:** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### Diferenças de ambiente

- **Estágios (.page):** Alterações mais recentes para teste.
- **Ao vivo (.live):** Conteúdo publicado para produção.

![Estrutura de URL](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Detalhamento da estrutura de URL do formulário do Edge Delivery Services*

#### Exemplos Visuais

**Modelo do Edge Delivery Services:**

- Preparado: ![Versão preparada do formulário de registro](/help/forms/assets/registration-form-staged-version.png)
- Ao vivo: ![Versão de registro ao vivo](/help/forms/assets/registration-form-live-version.png)

**Modelo do Componente Principal:**

- Preparado: ![Versão preparada do formulário de inscrição](/help/forms/assets/enrollment-form-staged-version.png)
- Live: ![Versão de inscrição online](/help/forms/assets/enrollment-form-live-version.png)

## Resolução de problemas

Abaixo estão problemas comuns e soluções para o AEM Forms com o Edge Delivery Services.

+++Formulário não carregado

**Problema:** A URL do formulário retorna 404 ou uma página em branco.

**Resolução:**

- Remover extensão `.html` das URLs.
- Verifique se o formulário foi publicado.
- Verifique o repositório GitHub para o bloco adaptável do Forms.
- Verifique se o nome do formulário corresponde à URL (diferencia maiúsculas de minúsculas).

+++

+++Problemas de configuração

**Problema:** a configuração do Edge Delivery Services não está funcionando.

**Resolução:**

- Verifique se a URL do GitHub está no formato `https://github.com/owner/repository`.
- Use o nome correto da ramificação na configuração.
- Verificar o acesso ao repositório (público ou autenticado).
- Verifique `fstab.yaml` para obter os detalhes corretos do GitHub.

+++

+++Problemas de publicação

**Problema:** alterações não aparecem no site ativo.

**Resolução:**

- Aguarde de 2 a 3 minutos para atualizar o cache da CDN.
- Confirme se o fluxo de trabalho de publicação foi concluído.
- Primeiro, teste o ambiente de preparo (.page).
- Verifique se o repositório do GitHub foi atualizado.

+++

+++Problemas do editor universal

**Problema:** não é possível editar o formulário ou os componentes que não estão carregando.

**Resolução:**

- Use um navegador compatível (Chrome, Firefox, Safari).
- Limpar o cache do navegador e os cookies.
- Verifique a conectividade da rede.
- Confirme as permissões do autor.

+++

+++Erros de envio de formulário

**Problema:** os envios de formulários não estão funcionando.

**Resolução:**

- Configure a ação de envio nas propriedades do formulário.
- Testar pontos de extremidade de envio manualmente.
- Verifique as configurações do CORS se estiver incorporando formulários.
- Verifique se os campos obrigatórios estão configurados.

+++

+++Problemas de desempenho

**Problema:** Carregamento lento ou desempenho insatisfatório.

**Resolução:**

- Otimizar imagens.
- Remova componentes desnecessários.
- Aproveite a CDN do Edge Delivery Services.
- Minimize o JavaScript/CSS personalizado.

+++

+++Obtendo ajuda

Se os problemas persistirem:

1. Verifique o status do serviço do Adobe Experience Cloud.
2. Revise a [documentação do Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=pt-BR).
3. Visite A [Comunidade Da Adobe Experience League](https://experienceleaguecommunities.adobe.com/?profile.language=pt).
4. Entre em contato com o Atendimento ao cliente da Adobe.

+++

## Próximas etapas

Após concluir a criação e a publicação do formulário, considere o seguinte:

### Ações imediatas

- Teste o formulário usando este guia.
- Valide seu repositório GitHub e a conexão com o AEM.
- Revise os formulários de amostra.

### Tópicos avançados

- [Configurar Ações de Envio](/help/edge/docs/forms/universal-editor/submit-action.md): configure a manipulação de dados e as integrações.
- [Modelos de Dados de Formulário](/help/forms/create-form-data-models.md): conectar formulários a fontes de dados de back-end.

### Otimização do desempenho

- [Práticas recomendadas da Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=pt-BR): maximize o desempenho.
- [Análise de formulários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html): controle o desempenho do formulário e o comportamento do usuário.

