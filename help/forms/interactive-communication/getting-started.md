---
title: Introdução ao Editor de comunicação interativa (IC)
description: A comunicação interativa permite que as organizações projetem e entreguem comunicações personalizadas orientadas por dados.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Introdução ao Editor de comunicação interativa (IC)

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

O **Editor de IC (Comunicação Interativa)** no Adobe Experience Manager (AEM) Forms permite que as organizações projetem e entreguem comunicações personalizadas orientadas por dados, como declarações, faturas e cartas, em canais digitais e de impressão. Este guia fornece uma visão geral de como começar — da integração à navegação na interface do Editor IC.


## Integração e acesso

### Requisitos de acesso

Para usar a Comunicação interativa, verifique se o ambiente do AEM Forms as a Cloud Service inclui o **complemento do AEM Forms** e se a sua conta tem as permissões apropriadas.

### Verificar o navegador

Para conhecer os navegadores e as plataformas cliente compatíveis, siga o artigo vinculado, [Plataformas cliente compatíveis](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/supported-platforms)

>[!NOTE]
>
> **Suporte para navegadores com ciclos de lançamento rápidos:**
> Atualizações regulares de versões do Firefox, Chrome e Edge. A Adobe tem o compromisso de manter o nível de suporte listado acima para as próximas versões desses navegadores.

### Configurar funções e permissões de usuário

O acesso aos recursos do Editor IC é regido por [funções de usuário no AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions). Estas são as principais funções envolvidas na criação e no gerenciamento de Comunicações interativas:

| **Função** | **Descrição** | **Permissões principais** |
| --------------------- | ---------------------------------------------------------- | -------------------------------------------- |
| **Autor do formulário** | Cria e edita Comunicações interativas. | Criar, editar, visualizar e publicar ICs. |
| **Autor do modelo** | Cria modelos reutilizáveis para Comunicações interativas. | Crie e bloqueie modelos, defina layouts. |
| **Administrador** | Gerencia acesso, permissões e configurações do usuário. | Atribuir funções, gerenciar modelos, publicar ICs. |
| **Autor do FDM** | [Cria e gerencia Modelos de Dados de Formulário (FDM)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models) para integração de dados. | Crie, edite e configure fontes de dados e modelos. |

>[!NOTE]
>
> Verifique se os usuários fazem parte dos grupos apropriados do AEM (por exemplo, `forms-user`, `fdm-author`, `template-authors`) para acessar os recursos correspondentes.

## Acessar o Editor IC

1. Faça logon na sua instância do **AEM Forms as a Cloud Service**.
2. Navegue até **Forms > Comunicações interativas**.
3. Clique em **Criar** → **Comunicação interativa**.
4. Escolha um **Modelo**, configure as fontes de dados e clique em **Criar** para abrir o **Editor de Comunicações Interativas**.

O editor fornece um ambiente unificado para projetar, visualizar e gerenciar versões impressas e da Web das comunicações.

## Navegar na interface

A interface do **Editor de Comunicação Interativa** foi criada para conceder aos autores acesso intuitivo a todas as ferramentas de design e opções de configuração.

![Localizar IC Docu](/help/forms/interactive-communication/assets/navigate-the-interface.png)

### &#x200B;1. Barra de ferramentas superior

![Localizar IC Docu](/help/forms/interactive-communication/assets/tool-bar.png)

**Local:** Seção mais alta

**Finalidade:** fornece acesso ao ambiente e ações globais.

**Inclui:**

Exibe o **ambiente do Adobe Experience Cloud** (por exemplo, Preparo), juntamente com o **título do projeto**, o **feedback do Beta**, as **notificações** e os **controles de perfil** para gerenciar configurações de usuário e acesso ao ambiente.

### &#x200B;2. Barra de guias (guias Design/Mestre e controles de arquivo)

![Localizar IC Docu](/help/forms/interactive-communication/assets/tab-bar.png)

**Local:** Abaixo do cabeçalho superior

**Propósito:** Gerenciar exibições e arquivos de comunicação.

**Inclui:**

**Guias:** alterne entre o **Modo de Exibição de Design** e o **Modo de Exibição de Página Mestra** para layout e design de elemento reutilizável

**Nome do Arquivo:** Exibe o título da comunicação atual (por exemplo, ic-11)

**Controles de Exibição:** Opções como regra, criação, Zoom (85%), Desfazer/Refazer, Excluir, Visualização do PDF e Salvar

### &#x200B;3. Painel esquerdo (Navegação e ferramentas de componente)

![Localizar IC Docu](/help/forms/interactive-communication/assets/left-panel.png)

**Local:** Lado esquerdo da interface

**Propósito:** Acessar a estrutura do projeto, os ativos reutilizáveis e as associações de dados.

**Inclui:**

* **Página Inicial:** Leva o usuário para a tela inicial principal Comunicação Interativa (IC), onde você pode visualizar e gerenciar ICs e pastas existentes.

* **Painel de Menus:** Exibe opções relacionadas à exibição, como Réguas, Limites de Objeto, Ajustar à Grade, Ajustar ao Objeto de Recurso e o recurso Importar XDP.

* **Modo de Exibição de Hierarquia:** Exibe a estrutura do componente da comunicação, mostrando a organização de páginas, painéis e subformulários.

* **Biblioteca de Componentes:** contém elementos de design como Texto, Imagem, Subformulário e Código de Barras que podem ser arrastados para a tela.

* **Fragmentos:** habilita a reutilização de blocos de design e conteúdo predefinidos em várias comunicações.

* **Modelo de Dados:** Conecta a comunicação aos Modelos de Dados de Formulário (FDM) subjacentes para associar dados dinâmicos.

### &#x200B;4. Workspace Central (Tela de Design)

![Localizar IC Docu](/help/forms/interactive-communication/assets/canvas.png)

**Local:** Centro da interface

**Propósito:** espaço de trabalho primário para criar Comunicações Interativas.

**Recursos:**

* Arrastar e soltar componentes da biblioteca

* Organizar e formatar o layout visual

* Adicionar ou editar páginas, subformulários e campos

* Navegue entre páginas (por exemplo, &quot;1 de 1&quot;) usando controles no canto inferior esquerdo

* Visualizar o layout final antes de publicar

### &#x200B;5. Painel direito (Painel Propriedades)

![Localizar IC Docu](/help/forms/interactive-communication/assets/right-panel.png)

**Local:** Lado direito da tela

**Propósito:** Personalizar comportamento e estilo do componente.

**Inclui:**

* Configurações gerais (nome, tipo, fluxo/posição)

* Opções de layout e aparência

* Controles de Paginação, Posição, Presença e Vinculação de dados