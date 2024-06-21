---
title: Gerenciamento de públicos
description: O console de Públicos permite criar, organizar e gerenciar públicos da sua conta do Adobe Target ou gerenciar segmentos do ContextHub
exl-id: dff72c15-afcd-4b16-a711-e9ca3010e3ec
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 86%

---

# Gerenciamento de públicos{#managing-audiences}

O console de Públicos permite criar, organizar e gerenciar públicos para sua conta do Adobe Target ou gerenciar segmentos do ContextHub:

* Adição de públicos-alvo, seja públicos-alvo do Adobe Target ou segmentos do ContextHub.
* Gerenciar públicos-alvo.

Um público, chamado de *segmento* no ContextHub, é uma classe de visitantes definida por critérios específicos, que determina quem vê uma atividade direcionada. Ao direcionar uma atividade, é possível selecionar públicos diretamente no processo de direcionamento ou criar novos no console Públicos-alvo.

No console Públicos-alvo, os públicos-alvo são organizados por marca.

Os Públicos estão disponíveis no modo Direcionamento para [criação de conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md), em que você também pode criar públicos (mas é necessário criar públicos do Adobe Target no console de Públicos). Os públicos-alvo criados no modo Direcionamento são exibidos no console Públicos-alvo.

Os públicos-alvo são exibidos com um rótulo que descreve que tipo de público-alvo está definido:

* CH - Segmento do ContextHub
* AT - Público-alvo do Adobe Target

## Criação de um segmento do ContextHub no console Públicos-alvo {#creating-a-contexthub-segment-in-the-audiences-console}

É possível criar um segmento do ContextHub no console Públicos-alvo ou durante o processo de direcionamento.

Para criar um segmento do ContextHub no console Públicos-alvo:

1. No console Navegação, selecione **Personalização**. Selecionar **Públicos-alvo**.
1. Selecionar **Criar segmento do ContextHub**.

   ![Criação de um segmento](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. Na caixa de diálogo **Novo segmento do ContextHub**, insira um título e ajuste o reforço e clique em **Criar**. Seu novo segmento do ContextHub aparece na lista de públicos-alvo.

   >[!NOTE]
   >
   >Classifique a lista modificada tocando ou clicando em **Modificado** para classificar por ordem decrescente para ver qualquer público-alvo criado.

Para obter mais detalhes sobre a criação de segmentos usando o ContextHub, consulte a documentação da Configuração da segmentação com o ContextHub. <!--For further detail about creating segments using ContextHub, see [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md).-->

## Criação de um público-alvo do Adobe Target usando o Console de público-alvo {#creating-an-adobe-target-audience-using-the-audience-console}

Podemos criar públicos-alvo do Adobe Target diretamente no AEM usando o console Públicos-alvo.

Os públicos-alvo são definidos por regras que determinam quem está incluído em uma atividade de direcionamento. Uma definição de público-alvo pode incluir várias regras, e cada uma delas pode incluir vários parâmetros.

Quando você usa mais de uma regra, elas são combinadas pelo operador boolean AND, o que significa que qualquer membro do público-alvo em potencial deve atender a todas as condições definidas para ser incluído na atividade. Por exemplo, se você definir uma regra de AND e uma regra de navegador, apenas os visitantes que usarem o SO definido e o navegador definido serão incluídos na atividade.

>[!NOTE]
>
>Se você não vir **Criar público-alvo** no menu **Criar**, não terá as permissões necessárias para criar um público-alvo. Você precisa de permissões de gravação no `/etc/segmentation` para criar públicos-alvo. Por padrão, os autores de conteúdo do grupo têm permissões de gravação.

Para criar um público-alvo do Adobe Target:

1. No console Navegação, selecione **Personalização**. Selecionar **Públicos-alvo**.

   ![Navegação até públicos](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. No console Públicos-alvo, selecione **Criar** e depois **Criar público-alvo**.

   ![Criação de um público do Target](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. No **Configuração do Adobe Target** , selecione a configuração de destino e selecione **OK**.
1. Na área Regra nº 1, selecione o tipo de atributo e insira quaisquer informações de atributo nos campos disponíveis. Ao terminar, selecione a marca de seleção à direita do atributo para salvá-lo. Consulte [Atributos e suas opções](#attributes-and-their-options) para obter informações sobre todos os atributos.
1. Clique em **Adicionar regra** para adicionar outra regra. Insira quantas regras forem necessárias. As regras são combinadas com o operador boolean AND, o que significa que o público-alvo deve atender a todos os requisitos de cada regra para ser elegível para uma atividade.
1. Selecione **Próximo**.
1. Insira um nome para o público e selecione **Salvar**.
1. Selecionar **Salvar**. Seu público-alvo estará na lista de Públicos-alvo.

### Atributos e suas opções {#attributes-and-their-options}

É possível criar regras de direcionamento para cada um dos seguintes atributos:

| **Atributo** | **Descrição** | **Para obter mais informações** |
|---|---|---|
| **Móvel** | Direcione dispositivos móveis com base em parâmetros como dispositivo móvel, tipo de dispositivo, fornecedor de dispositivo, dimensões de tela (por pixels), e muito mais. | Consulte [Documentação para dispositivos móveis](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=pt-BR) no Adobe Target. |
| **Personalizado** | Parâmetros personalizados são parâmetros mbox. Se você passar algum parâmetro de mbox para mboxes, ou usar a função targetPageParams, esses parâmetros aparecerão aqui para uso em públicos-alvo. | Consulte [Documentação de parâmetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=pt-BR) no Adobe Target. |
| **OS** | Você pode direcionar os visitantes que usam um determinado sistema operacional. | Direcionado a usuários que estejam usando Linux, Macintosh ou Windows. |
| **Páginas do site** | Direcione visitantes que estão em uma página específica ou têm um parâmetro específico de mbox. | Consulte [Documentação das páginas do site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=pt-BR) no Adobe Target. |
| **Navegador** | Você pode direcionar os usuários que utilizam um determinado navegador ou determinadas opções de navegador quando visitam sua página. | Consulte [Documentação das opções do navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=pt-BR) no Adobe Target. |
| **Perfil do visitante** | Direcione visitantes que atendem a parâmetros de perfil específicos. | Consulte [Documentação do perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=pt-BR) no Adobe Target. |
| **Fontes de tráfego** | Direcione visitantes com base no mecanismo de pesquisa ou página de aterrissagem de referência para o site. | Consulte [Documentação das origens de tráfego](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=pt-BR) no Adobe Target. |

## Modificação de um público-alvo no console Públicos-alvo {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Só é possível editar públicos-alvo do Adobe Target que foram criados na mesma instância do AEM na qual você está editando. Públicos-alvo criados em ambientes do AEM diferentes não podem ser editados.

É possível editar qualquer público do ContextHub no console de Públicos. Você pode editar os públicos do Adobe Target, mas somente aqueles que foram criados no AEM:

1. No console Navegação, selecione **Personalização**. Selecionar **Públicos-alvo**.
1. Selecione o ícone ao lado do segmento do ContextHub que você deseja editar e selecione **Editar**.
1. Faça edições no editor de segmentos. Consulte a documentação do ContextHub para obter mais informações. <!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
