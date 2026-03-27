---
title: Habilitar e configurar a Interface do Usuário Associada para Comunicações Interativas
description: Saiba como habilitar a Exibição associada e configurar o fluxo de trabalho para atualizações nas Configurações de comunicação interativa para que os associados possam usar a Interface do usuário associada.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 7c3e8a2b-5f21-4a1e-9e2d-8a4b6c7d8e9f
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Habilitar e configurar a Interface do Usuário Associada para Comunicações Interativas

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

Este artigo descreve como ativar a Interface do usuário associada para uma Comunicação interativa (IC) e, opcionalmente, configurar um fluxo de trabalho do AEM para envios. Os autores executam essas etapas em **Configurações de comunicação interativa**.

Para obter uma visão geral das funções Associar interface e usuário, consulte [Associar interface no Interative Communication Editor](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md).

## Pré-requisitos

Antes de habilitar e configurar a Interface do usuário associada, verifique se você tem:

- **Acesso de autor** ao editor de comunicação interativa.
- Uma **Comunicação Interativa** criada com o layout e as associações de dados necessários.
- **Usuários associados** adicionados ao grupo **Forms-associates** (necessário para que os associados acessem a interface do usuário associada).
- **Autores** adicionado ao grupo **formulários-associados** (necessário para que os autores acessem a interface do usuário para associados).

Quando estiver pronto para integrar a interface do usuário Associate ao seu aplicativo e chamá-la na instância de Publicação, você também precisará de um navegador com suporte a pop-up ativado e a IC publicada. Consulte [Integrar a interface do usuário associada no seu aplicativo](/help/forms/interactive-communication/invoke-associate-ui.md) para obter os pré-requisitos de integração completa.

## Habilitar Exibição Associada (Interface do Usuário Associada)

Ative a interface do usuário Associar no nível do documento para que as Comunicações interativas possam ser usadas pelos associados.

1. Abra a Comunicação interativa no editor.
1. Na barra de ações ou nas opções do documento superiores, abra **Configurações de Comunicação Interativa** (ou **Configurações**).

   ![Configurações de Comunicação Interativa - Associar Propriedades a Habilitar a Edição de Exibição Associada](/help/forms/assets/associate-ui-settings.png)

1. No painel esquerdo, verifique se **Associar propriedades** está selecionado.
1. À direita, marque **Habilitar Edição de Exibição Associada**.
1. Clique em **Aplicar alterações** e salve o documento.

   ![Configurações de Comunicação Interativa - Associar Propriedades a Habilitar a Edição de Exibição Associada](/help/forms/assets/associate-ui-enable-view.png)

Uma mensagem pode lembrá-lo de aplicar alterações e salvar o documento para ativar a opção Associar exibição. Depois de salvar, o IC está disponível para uso orientado por associados.

### Permitir edição de Interface de Usuário Associada por componente

Quando a opção Associar exibição estiver habilitada para a IC, você deverá ativar **Permitir edição por associação** para cada componente que a associação possa editar. Os componentes sem essa configuração ativada permanecem como somente leitura na Interface do usuário associada.

1. No editor IC, selecione o componente (por exemplo, um campo de texto) na tela ou na Hierarquia de componentes.
1. No painel direito **Propriedades**, expanda **Propriedades Associadas**.
1. Ative **Permitir Edição pelo Associado** **Ativado** para esse componente.
1. Repita o procedimento para cada componente associado que precisa editar e salve o documento.

![Permitir edição por associação nas propriedades do componente](/help/forms/assets/associate-ui-allow-editing-by-associate.png)

>[!NOTE]
>
> As **Propriedades Associadas** também incluem opções como **Tipografia** (fonte, tamanho e estilo do campo na Interface do Usuário Associada), **Dica de Ferramenta** e **Padrões** (validações). Use-os para controlar a aparência e o comportamento do componente quando os associados o editarem — por exemplo, defina padrões de validação para que os associados insiram dados no formato necessário.

## Configurar fluxo de trabalho para a interface do usuário associada

Para executar um fluxo de trabalho do AEM quando os usuários enviam ou atualizam dados pela interface do usuário Associate, configure o seguinte:

1. Em **Configurações de comunicação interativa**, selecione **Fluxo de trabalho** no painel esquerdo (em Propriedades de associação).
1. Ativar **Configurar Fluxo de Trabalho para Atualização** **Ativado**.
1. Em **Selecionar modelo de fluxo de trabalho**, escolha o modelo de fluxo de trabalho do AEM a ser executado (por exemplo, `conversionWorkflow` ou um caminho como `/var/workflow/models/submit-workflow-1`).
1. Opcionalmente, defina **Mensagem de Êxito do Fluxo de Trabalho** (exibida ao usuário após a conclusão do fluxo de trabalho).
1. Opcionalmente, defina a **URL de redirecionamento** para enviar o usuário para uma página específica após o envio.
1. Clique em **Aplicar alterações** e salve o documento.

   ![Configurações de Comunicação Interativa - Configuração de fluxo de trabalho para Interface do Usuário Associada](/help/forms/assets/associate-ui-configure-workflow.png)

Quando você habilita um fluxo de trabalho, ele é executado sempre que os usuários enviam pela Interface do usuário associada. Para saber como o envio e o fluxo de trabalho funcionam, onde são executados, quem usa qual instância e as principais considerações, consulte [Fluxo de trabalho de envio para Interface do Usuário Associada](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior). Esse artigo também inclui um exemplo de um fluxo de trabalho que gera o PDF a partir de envios IC.

## Concluir a configuração da interface do usuário Associar

Depois de ativar a opção Associar exibição e configurar o fluxo de trabalho:

1. **Habilitar campos editáveis:** nas seções necessárias da IC, habilite os campos associados que podem ser editados. Defina validações e comportamento obrigatório/somente leitura conforme necessário.
1. **Publique a IC** para que ela esteja disponível na instância de Publicação para associados.
1. Compartilhar o link IC publicado com associados. Eles autenticam (por exemplo, por meio da [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) e abrem a Interface do Usuário Associada, inserem ou confirmam dados do cliente e geram a comunicação final. Se você tiver configurado um fluxo de trabalho, ele será executado no envio. Para saber como o envio e o fluxo de trabalho funcionam, consulte [Fluxo de trabalho de envio para Interface do Usuário Associada](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior).

## Consulte também:

- [Associar a interface no Editor de comunicação interativa](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Integrar a interface do usuário do Associate no seu aplicativo](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Fluxo de trabalho de envio para Interface do Usuário Associada — IC Gerar Saída do PDF](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md) — como o envio e o fluxo de trabalho funcionam, além de um exemplo de fluxo de trabalho que gera o PDF a partir de envios de IC.
