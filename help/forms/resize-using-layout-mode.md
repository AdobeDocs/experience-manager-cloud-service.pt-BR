---
title: Como faço para usar o modo de layout para redimensionar componentes para formulários adaptáveis?
description: Defina a posição dos componentes do AEM Forms, aprenda a acessar o modo de layout, redimensionar componentes, redimensionar painéis e definir o layout de várias colunas para um painel.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components
exl-id: 53896a8e-4568-460b-bca7-994baea0c8eb
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 1%

---

# Usar o modo de layout para redimensionar componentes para o Adaptive Forms {#use-layout-mode-to-resize-components}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/resize-using-layout-mode.html) |
| AEM as a Cloud Service | Este artigo |

A interface de criação do Formulário adaptável permite redimensionar componentes usando o modo Layout. Arraste os pontos azuis dentro das colunas para definir os pontos inicial e final para posicionar os componentes. Os pontos azuis são exibidos depois de tocar no componente na grade responsiva. A grade responsiva consiste em 12 colunas iguais. O sombreamento das cores branco e azul em colunas alternadas diferencia uma coluna da outra.

Você pode usar o modo Layout para redimensionar componentes para todos os tipos de dispositivos, como desktop, tablet, telefone e outros dispositivos menores. O tablet deriva automaticamente a configuração de layout da versão do desktop e os dispositivos menores derivam a configuração de layout do telefone. No entanto, você pode substituir as configurações derivadas automaticamente para definir uma configuração diferente para cada tipo de dispositivo.

## Modo de layout de acesso {#access-layout-mode}

Selecionar **[!UICONTROL Layout]** na lista suspensa que aparece na parte superior da interface de criação do Formulário adaptável ao lado da guia **[!UICONTROL Visualizar]** opção. O formulário é exibido no modo Layout.

1. Faça logon no [!DNL Adobe Experience Manager] instância do autor e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Criar um novo ou abrir um existente [Formulário adaptável](creating-adaptive-form.md).
1. Selecionar **[!UICONTROL Layout]** na lista suspensa que aparece na parte superior ao lado da guia **[!UICONTROL Visualizar]** opção. O formulário é exibido no modo Layout.

   ![Modo de layout](assets/layout_mode_ic_new.png)

## Redimensionar componentes {#resize-components}

1. No modo Layout, selecione o componente a ser redimensionado. Os pontos azuis são exibidos no início e no fim da grade responsiva.
1. Arraste e solte os pontos azuis para definir a posição do componente na grade responsiva.

   ![Redimensionar usando o modo Layout](assets/layout_mode_resize_new_updated1.png)

   A barra de ferramentas exibida ao tocar em componentes consiste nas seguintes opções:

   * **[!UICONTROL Pai]**: seleciona o primário de um componente.
   * **[!UICONTROL Reverter layout do ponto de interrupção]**: desfaz todas as alterações de redimensionamento e aplica o layout padrão ao componente.
   * **[!UICONTROL Flutuar para a nova linha]**: desloque o componente para a próxima linha se houver vários componentes dentro da mesma linha.

   Você também pode usar a variável **[!UICONTROL Reverter layout do ponto de interrupção]** ( ![Reverter ponto de interrupção](assets/reverttopreviouslypublishedversion.png)) no nível do painel para desfazer todas as alterações de redimensionamento.

   >[!NOTE]
   >
   >Não é possível redimensionar componentes de coluna de tabela, barra de ferramentas, botão da barra de ferramentas e área de destino usando o modo Layout. Use o modo Estilo para redimensionar esses componentes.

### Exemplo {#example}

**Objetivo:** Você deseja inserir um componente Tabela e um componente Imagem e posicioná-los paralelamente um ao outro em um Formulário adaptável.

1. Insira os componentes de tabela e imagem usando [!UICONTROL Editar] no Formulário adaptável. O componente de imagem é exibido após o componente de tabela.
1. Alternar para [!UICONTROL Layout] e selecione a variável [!UICONTROL Tabela] componente. Os pontos azuis para redimensionar a exibição do componente nas colunas 1 e 12.
1. Arraste o ponto azul na coluna 12 para a coluna 6 da grade responsiva.

   ![Definir o ponto final da tabela](assets/layout_mode_end_point_table_new.png)

1. Da mesma forma, selecione o [!UICONTROL Imagem] e arraste o ponto azul na coluna 1 para a coluna 7 da grade responsiva. Os componentes de tabela e imagem são exibidos paralelamente um ao outro.

   ![Tabela e imagem em paralelo no modo Layout](assets/table_image_parallel_new.png)

   É possível selecionar o componente de Imagem e selecionar a variável **[!UICONTROL Flutuar para a nova linha]** opção disponível na barra de ferramentas para deslocar o componente Imagem para a próxima linha.

## Redimensionar painéis {#resize-panels-layout-mode}

Execute as seguintes etapas se desejar redimensionar o painel inteiro em vez de componentes individuais:

1. Selecione qualquer um dos componentes no painel que deseja redimensionar, selecione ![Selecionar pai](assets/select_parent_icon.svg)e selecione a primeira opção na lista suspensa, se o painel for o principal imediato do componente.

   Os pontos azuis são exibidos no início e no fim da grade responsiva.

1. Arraste e solte os pontos azuis para definir a posição do painel na grade responsiva.
Você pode repetir as etapas 1 e 2 e selecionar ![Selecionar pai](assets/float_to_new_line_icon.svg) para deslocar o painel redimensionado para a próxima linha.

## Definir layout de várias colunas para um painel

Execute as seguintes etapas para definir o número de colunas para um painel:

1. Entrada **[!UICONTROL Editar]** , selecione o painel, selecione ![Configurar](assets/configure-icon.svg)e selecione **[!UICONTROL Responsivo - tudo na página sem navegação]** opção no **[!UICONTROL Layout do painel]** lista suspensa.

1. Selecionar ![Salvar](assets/save_icon.svg) para salvar as propriedades.

1. No **[!UICONTROL Layout]** , selecione qualquer um dos componentes no painel, selecione ![Selecionar pai](assets/select_parent_icon.svg)e selecione o painel.

1. Selecionar ![várias colunas](assets/multi-column.svg) e selecione o número de colunas na lista suspensa. O número de colunas pode variar de 1 a 12. O painel é dividido em um layout de várias colunas.

![várias colunas no modo de layout](assets/multi-column-layout.png)

## Ativar a nova grade responsiva para layouts responsivos antigos {#enableresponsivegrid}

Habilite a nova grade responsiva para formulários criados com o [!DNL Adobe Experience Manager] Forms 6.4 ou versão inferior para redimensionar componentes.

>[!NOTE]
>
>Alternar para a nova grade responsiva descarta as propriedades de layout já definidas para componentes usados no formulário.

Execute as seguintes etapas para ativar a nova grade responsiva:

1. Selecionar **[!UICONTROL Layout]** na lista suspensa que aparece na parte superior ao lado da guia **[!UICONTROL Visualizar]** opção. Uma confirmação para ativar o modo Layout é exibida.
1. Selecionar **[!UICONTROL Sim]** para habilitar o **[!UICONTROL Layout]** para o formulário.

### Incorporar um fragmento antigo em um Formulário adaptável com um novo layout responsivo {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

O novo layout responsivo para Formulário adaptável permite adicionar um Fragmento de formulário adaptável com o layout responsivo antigo ao formulário. No entanto, o novo layout descarta as propriedades de layout já definidas para os componentes usados no fragmento. Você pode alternar para o modo Layout para definir as propriedades de layout dos componentes usados no fragmento.

### Incorporar um fragmento com o novo layout responsivo em um Formulário adaptável antigo {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Se você incorporar um fragmento com o novo layout responsivo em um Formulário adaptável com um layout responsivo antigo, o sistema solicitará que você ative o modo Layout para o formulário e incorpore novamente o fragmento.

Para ativar o modo Layout, selecione **[!UICONTROL Layout]** na lista suspensa que aparece na parte superior ao lado da guia **[!UICONTROL Visualizar]** e selecione **[!UICONTROL Sim]** para confirmar. Selecionar **[!UICONTROL Editar]** para incorporar novamente o fragmento.

## Desativar o modo Layout para formulários com layout responsivo antigo {#disable-layout-mode-for-forms-with-old-responsive-layout}

Você pode desativar o modo Layout para formulários com layout responsivo antigo editando propriedades para o modelo usado no formulário.

Execute as seguintes etapas para desativar o modo Layout:

1. Selecionar **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]** e abra o modelo usado no formulário no **[!UICONTROL Editar]** modo.
1. Selecione o Contêiner de formulário no painel esquerdo e selecione **[!UICONTROL Política.]**

   ![Desativar modo de layout](assets/policy_disable_layout_mode.png)

1. Selecione o **[!UICONTROL Configurações de layout]** e selecione **[!UICONTROL Desativar modo de layout]**.
1. Selecionar ![Salvar alterações](assets/save_icon.svg) para salvar as propriedades do template.

## Consulte também {#see-also}

{{see-also}}