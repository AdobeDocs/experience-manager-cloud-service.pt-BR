---
title: Criar e publicar Forms adaptável com o Edge Delivery Services
description: Instruções detalhadas sobre como criar, criar e publicar o Adaptive Forms usando modelos do Edge Delivery Services no AEM, com foco na precisão e clareza técnicas.
keywords: formulários adaptáveis, serviços de entrega de borda, editor universal, criação de formulários, formulários do AEM, publicação de formulários
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---


# Criar e publicar Forms adaptável com o Edge Delivery Services

Este documento fornece instruções passo a passo para criar, configurar e publicar o Adaptive Forms usando modelos do Edge Delivery Services no AEM. Ele abrange o fluxo de trabalho completo, desde a criação de formulários até a implantação em produção.

Ao final deste guia, você aprenderá a:

- Criar formulários usando modelos do Edge Delivery Services
- Criar formulários usando o Editor universal
- Configurar e publicar formulários no Edge Delivery Services
- Acesse os formulários publicados e verifique a implantação



## Pré-requisitos

Verifique se os seguintes pré-requisitos estão sendo atendidos antes de continuar:


- **AEM Forms as a Cloud Service**: uma instância de autor ativa com uma licença do Forms.
- **Conta do GitHub**: conta pessoal ou organizacional para gerenciamento de repositório.
- **Configuração do Repositório**: escolha uma das seguintes opções:
   - **Novo projeto**: [Crie um novo projeto do AEM com Bloco de Forms Adaptável](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block). O repositório é pré-configurado para o Edge Delivery Services.
   - **Projeto existente**: [Adicionar bloco adaptável do Forms a um repositório existente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) e atualizar a configuração.

- **Conexão AEM-GitHub**: [Estabeleça uma conexão](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) entre sua instância do AEM e o repositório GitHub.
- **Edge Delivery Services**: verifique se o repositório está configurado para implantação automática.
- **Permissões**: verifique se você tem os direitos de acesso necessários para a criação e publicação de formulários.

- Confirme se o repositório do GitHub contém o bloco adaptável do Forms.



## Fluxo de trabalho de criação e publicação de formulários

O processo consiste em três fases principais:

- **Fase 1:** [Criação de Formulário](#step-1-form-creation)
- **Fase 2:** [Criação e design do formulário](#step-2-form-authoring-and-design)
- **Fase 3:** [Configuração e Publicação](#step-3-configuration-and-publishing)

Cada fase inclui etapas de validação para confirmar a configuração correta.


### Etapa 1: Criação do formulário

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

### Etapa 2: criação e design do formulário


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
   - Ajuste o estilo e o layout conforme necessário.

   ![Formulário de Registro Concluído](/help/edge/assets/contact-us.png)

#### Validação

- Todos os campos obrigatórios estão presentes.
- As propriedades do campo estão configuradas corretamente.
- O layout é responsivo e acessível.
- As regras de validação funcionam conforme esperado.

#### Próximas etapas

- [Configurar ações de envio](/help/edge/docs/forms/universal-editor/submit-action.md) para manipulação de dados.
- [Guia do Editor Universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) para recursos avançados.

### Etapa 3: configuração e publicação

Configure o Edge Delivery Services e publique seu formulário.

**Configuração:** Automática (nenhuma configuração manual é necessária).

- A conexão do repositório GitHub e a configuração do Edge Delivery Services são criadas durante a criação do formulário.
- Os endpoints de publicação são configurados automaticamente.

**Verificação:**

- Confirme se a configuração aparece nas configurações do formulário.
- Verifique se o URL do GitHub está vinculado corretamente.

![Configuração automática de EDS](/help/edge/assets/aem-instance-eds-configuration.png)

#### Publicação do formulário

1. No Universal Editor, clique no botão **Publicar** (canto superior direito).
2. Confirme o sucesso da publicação na caixa de diálogo.
3. Observe os URLs gerados para versões preparadas e ativas.

   ![Publicação do Editor Universal](/help/edge/assets/publish-form.png)

- [Guia de publicação](/help/edge/docs/forms/universal-editor/publish-forms.md)

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

## Resolução de problemas

Abaixo estão problemas comuns e soluções para o AEM Forms com o Edge Delivery Services.

+++Formulário não está carregando

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

+++Problemas do Universal Editor

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

- [Configurar Ações de Envio](/help/edge/docs/forms/universal-editor/submit-action.md): configure a manipulação de dados e as integrações.
- [Modelos de Dados de Formulário](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md): conectar formulários a fontes de dados de back-end.
- [Práticas recomendadas da Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=pt-BR): maximize o desempenho.
- [Análise de formulários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html): controle o desempenho do formulário e o comportamento do usuário.

