---
title: Como personalizar o modelo gerado automaticamente de Documento de registro para o Adaptive Forms?
description: Saiba como baixar, personalizar e recarregar o modelo de Documento de registro (DoR) gerado automaticamente para o Adaptive Forms usando o Adobe Forms Designer.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer
source-git-commit: 51ec9ef76a8f3f9b7bf2cdc25b03f72e286f586f
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 0%

---


# Personalizar o modelo de documento de registro gerado automaticamente

<span class="preview"> Este artigo se aplica aos **Componentes principais** e **Componentes básicos** baseados no Forms Adaptável.</span>

Quando você gera automaticamente um Documento de registro (DoR) para um Formulário adaptável, o AEM Forms cria um modelo padrão com base na estrutura do formulário. Você pode personalizar esse modelo gerado automaticamente para corresponder aos requisitos de marca e layout da sua organização.

O fluxo de trabalho de personalização envolve três etapas:

1. Baixe o modelo DoR gerado automaticamente do Forms Manager.
1. Modifique o modelo usando o Adobe Forms Designer.
1. Faça upload novamente do modelo personalizado para o AEM Forms e configure-o como um modelo personalizado.

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem o seguinte:

* Acesso ao AEM Forms Manager com permissões para baixar e fazer upload de modelos.
* Adobe Forms Designer instalado em seu computador local.
* Um Formulário Adaptável com **[!UICONTROL Gerar Documento de Registro]** habilitado.

## Etapa 1: baixar o modelo DoR gerado automaticamente {#download-auto-generated-dor-template}

Para baixar o modelo DoR gerado automaticamente (arquivo XDP) para o Formulário adaptável:

1. Faça logon na instância de autor do AEM Forms.
1. Navegue até **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione o Formulário adaptável para o qual deseja baixar o modelo DoR.
1. Abra as propriedades do Formulário adaptável selecionado.
1. No painel de propriedades, selecione a opção **[!UICONTROL Baixar documento de registro]** para baixar o modelo DoR gerado automaticamente (arquivo XDP).
1. Salve o arquivo XDP baixado no computador local.


## Etapa 2: Personalizar o modelo usando o Adobe Forms Designer {#customize-template-using-designer}

Abra o modelo XDP baixado no Adobe Forms Designer e modifique-o para atender às necessidades de sua organização.

1. Abra o arquivo XDP baixado no **Adobe Forms Designer**.
1. Personalize o modelo conforme necessário. Exemplos de personalizações incluem:

   * **Várias páginas mestras**: adicione mais páginas mestras para definir layouts diferentes para páginas específicas do documento de registro. Por exemplo, use uma primeira página distinta com papel timbrado de empresa e páginas subsequentes com layout mais simples.
   * **Cores e famílias de fontes**: altere a cor, o tamanho e a família da fonte para alinhar-se às diretrizes da marca corporativa.
   * **Elementos personalizados**: adicione elementos como logotipos, cabeçalhos, rodapés e texto de aviso de isenção de responsabilidade da empresa para estabelecer uma identidade de marca consistente.
   * **Layout e estilo da página**: ajuste as margens, o espaçamento e a estrutura geral da página para melhorar a leitura.
   * **Estilo e posicionamento do campo**: modifique a aparência e a posição dos campos de formulário para corresponder ao seu layout preferido.

1. Salve o modelo XDP personalizado.

>[!NOTE]
>
> Não remova nem modifique scripts presentes no modelo. Modificar scripts pode afetar a vinculação de dados e a geração do Documento de registro.

## Etapa 3: Faça upload novamente do modelo personalizado para o AEM {#reupload-customized-template}

Depois de personalizar o modelo, carregue-o no AEM Forms e configure o Formulário adaptável para usá-lo.

1. Faça upload do modelo XDP personalizado para sua instância do AEM Forms:
   * Navegue até **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
   * Selecione **[!UICONTROL Criar]** > **[!UICONTROL Carregar arquivo]** e carregue o arquivo XDP personalizado.

Em seguida, configure o formulário para usar o modelo personalizado. As etapas diferem dependendo se o formulário é baseado em Componentes principais ou Componentes de base.

>[!BEGINTABS]

>[!TAB Componentes principais]

Para o Forms adaptável com base nos Componentes principais:

1. Abra o Formulário adaptável no editor ao qual deseja aplicar o modelo personalizado.
1. Na árvore de conteúdo, selecione o **[!UICONTROL Guide Container]** (painel raiz).
1. Abra **[!UICONTROL Propriedades]** e clique no ícone do **[!UICONTROL Documento de Registro]** (DoR) para abrir as propriedades do Documento de Registro.
1. Na guia **[!UICONTROL Básico]**, abra a lista suspensa **[!UICONTROL Modelo]** e selecione **[!UICONTROL Personalizado]**.
1. Procure e selecione o modelo XDP personalizado carregado.
1. Selecione a marca de seleção a ser salva.

   ![Propriedades do Documento de Registro - Modelo definido como Personalizado (Componentes Principais)](/help/forms/assets/submission-pdf-dor-custom-template.png)

>[!TAB Componentes de base]

Para o Forms adaptável com base nos componentes de base:

1. Abra o Formulário adaptável no editor ao qual deseja aplicar o modelo personalizado.
1. Selecione o painel raiz (container do formulário).
1. Abra o **[!UICONTROL Documento de Propriedades de Registro]** (no painel de propriedades ou na guia DoR).
1. Na guia **[!UICONTROL Básico]**, abra a lista suspensa **[!UICONTROL Modelo]** e selecione **[!UICONTROL Personalizado]**.
1. Procure e selecione o modelo XDP personalizado carregado.
1. Selecione **[!UICONTROL Concluído]** para salvar.

   ![Propriedades do Documento de Registro - Modelo definido como Personalizado (Componentes de Base)](/help/forms/assets/dor-custom-template-foundation-components.png)

>[!ENDTABS]

O formulário adaptável agora usa o modelo personalizado ao gerar o documento de registro.

## Verificar o modelo personalizado {#verify-customized-template}

Para confirmar se o modelo personalizado foi aplicado corretamente:

1. Enviar uma entrada de teste para o Formulário adaptável.
1. Gere o documento de registro.
1. Verifique se o PDF gerado reflete suas personalizações, incluindo logotipos, fontes, alterações de layout e outros elementos de marca.

## Resolução de problemas {#troubleshooting}

| Problema | Resolução |
|---|---|
| O modelo personalizado não é carregado. | Verifique se o arquivo XDP é válido e não está corrompido. Verifique se você tem as permissões necessárias para fazer upload de arquivos para o AEM Forms. |
| As personalizações não aparecem no documento de registro gerado. | Confirme se você selecionou o modelo personalizado correto na seção **[!UICONTROL Configuração do modelo de documento de registro]** das propriedades do formulário. |
| Problemas de layout ou formatação no PDF gerado. | Verifique se as personalizações no Adobe Forms Designer seguem as [convenções de modelo base](/help/forms/generate-document-of-record-core-components.md#base-template-conventions). Verifique se todos os elementos estão posicionados corretamente na estrutura do modelo. |

## Consulte também {#see-also}

* [Gerar documento de registro para o Forms adaptável (componentes principais)](/help/forms/generate-document-of-record-core-components.md)
* [Gerar documento de registro para o Forms adaptável (componentes de base)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Modelo base de um documento de registro](/help/forms/generate-document-of-record-core-components.md#base-template-of-a-document-of-record)
* [Personalizar as informações de marca no documento de registro](/help/forms/generate-document-of-record-core-components.md#customize-the-branding-information-in-document-of-record)

