---
title: Trabalhar com publicação seletiva no Dynamic Media
description: Saiba como trabalhar com Publicação seletiva no Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Publishing,Dynamic Media
role: User
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2946'
ht-degree: 3%

---

# Configurar publicação seletiva no nível da pasta no Dynamic Media {#selective-publish-configure-folder}

Você pode optar por publicar ou cancelar a publicação de ativos para ou a partir do Adobe Experience Manager ou Dynamic Media. Você pode fazer isso no nível da pasta, usando **[!UICONTROL Gerenciar publicação]** ou **[!UICONTROL Publicação rápida]**. Este método de publicação é útil porque não depende exclusivamente da **[!UICONTROL Configuração do Dynamic Media]**, cujas configurações são globais para todas as pastas na sua instância do Dynamic Media.

Por exemplo, com a publicação seletiva, é possível trabalhar em ativos para produtos que ainda não estão online. Nesse caso, uma equipe de marketing pode acessar imagens de recorte inteligente e representações dinâmicas que são sincronizadas com o Dynamic Media. Eles podem criar materiais promocionais, tudo sem precisar publicar esses ativos no Dynamic Media para delivery global.

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Copiar* ativos de e para pastas limpa o estado de publicação desses ativos. No entanto, quando você *move* ativos de e para pastas cuja propriedade de pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

Se você decidir alterar posteriormente as configurações de **[!UICONTROL Publicação seletiva]** em uma pasta, essas alterações afetarão somente os novos ativos que você carregar nessa pasta a partir desse ponto. O estado de publicação dos ativos existentes na pasta permanece como está até que você os altere manualmente da caixa de diálogo **[!UICONTROL Publicação rápida]** ou **[!UICONTROL Gerenciar publicação]**.

A opção **[!UICONTROL Modo de publicação do Dynamic Media]** no nível da pasta sempre assume como padrão o valor encontrado na configuração **[!UICONTROL Publicar Assets]** da **[!UICONTROL Configuração do Dynamic Media]**. No entanto, as etapas a seguir neste tópico mostram como alterar manualmente esse valor padrão no nível da pasta (conforme descrito nas etapas a seguir) para substituir o valor **[!UICONTROL Configuração do Dynamic Media]**.

Independentemente de você confiar em:

* O valor **[!UICONTROL Publicar Assets]** definido em **[!UICONTROL Configuração do Dynamic Media]**
* Ou o valor **[!UICONTROL Modo de publicação do Dynamic Media]** definido nas propriedades de nível de pasta

Você ainda pode escolher **[!UICONTROL Imediatamente]**, **[!UICONTROL Na Ativação]** ou **[!UICONTROL Publicação Seletiva]**. Por exemplo, você pode definir o valor de **[!UICONTROL Publicar Assets]** na **[!UICONTROL Configuração do Dynamic Media]** como **[!UICONTROL Na ativação]**. E você pode definir o valor do modo de **[!UICONTROL Publicação do Dynamic Media]** no nível da pasta como **[!UICONTROL Publicação seletiva]**, vice-versa e assim por diante.

Depois de configurar a publicação seletiva em uma pasta, siga um destes procedimentos:

* [Publique ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação](#selective-publish-manage-publication).
* [Desfaça a publicação seletiva de ativos do Dynamic Media ou do Experience Manager usando Gerenciar publicação](#selective-unpublish-manage-publication).
* [Publicar ativos no Dynamic Media ou Experience Manager usando a Publicação rápida](#quick-publish-aem-dm).
* [Publicar ou cancelar a publicação seletiva de ativos por meio dos resultados da pesquisa](#selective-publish-unpublish-search-results).

**Para configurar a Publicação Seletiva no nível da pasta no Dynamic Media:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas) e vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Siga uma das seguintes opções:
   * Edite as propriedades de uma pasta existente - Na **[!UICONTROL Exibição de Cartão]**, na **[!UICONTROL Exibição de Coluna]** ou na **[!UICONTROL Exibição de Lista]**, navegue até uma pasta cujas propriedades você deseja editar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
   * Edite as propriedades de uma nova pasta - Na **[!UICONTROL Exibição de Cartão]**, **[!UICONTROL Exibição de Coluna]** ou **[!UICONTROL Exibição de Lista]**, próximo ao canto superior direito da página, vá para **[!UICONTROL Criar]** > **[!UICONTROL Pasta]**. Na caixa de diálogo **[!UICONTROL Criar Pasta]**, digite um título (obrigatório) para a pasta e selecione **[!UICONTROL Criar]**. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.

1. Na lista suspensa **[!UICONTROL Modo de sincronização]**, selecione uma das seguintes opções:

   | Modo de sincronização | Descrição |
   | --- | --- |
   | **[!UICONTROL Herdado]** | Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão definido na sua **[!UICONTROL Configuração do Dynamic Media]**. O status detalhado de **[!UICONTROL Herdado]** é mostrado por meio de uma dica de ferramenta. |
   | **[!UICONTROL Sincronizar tudo nesta subárvore da pasta com o Dynamic Media]** | Para que a publicação no Dynamic Media tenha êxito, os ativos devem ser sincronizados com o Dynamic Media. Selecionar essa opção inclui todos os ativos nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem a configuração padrão na **[!UICONTROL Configuração do Dynamic Media]**. |
   | **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** | Exclua todos os ativos nesta subárvore da sincronização com o Dynamic Media. |

   ![Publicação seletiva no nível da pasta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Na lista suspensa **[!UICONTROL Modo de publicação do Dynamic Media]**, selecione uma opção. A opção **[!UICONTROL Modo de publicação do Dynamic Media]** sempre padroniza o valor definido na **[!UICONTROL Configuração do Dynamic Media]**. No entanto, você pode substituir manualmente esse valor padrão de **[!UICONTROL Configuração do Dynamic Media]** usando uma das seguintes opções.

   >[!IMPORTANT]
   >
   >Independentemente da opção de modo de Publicação do Dynamic Media que você selecionar, qualquer atualização que você fizer posteriormente em um ativo que *já* tenha sido publicado, essas atualizações serão publicadas imediatamente, sem nenhuma outra ação do usuário.

   | Opção de modo de publicação do Dynamic Media | Descrição |
   | --- | --- |
   | **[!UICONTROL Imediatamente]** | Quando os ativos são carregados para essa pasta, o sistema assimila os ativos na Experience Manager e fornece o URL/Incorporar instantaneamente. Essa opção está vinculada somente à publicação no Experience Manager e não há necessidade de intervenção do usuário para publicar ativos.<br>Esta opção está *não* disponível se você selecionou **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** em **[!UICONTROL Modo de sincronização]** na etapa anterior. |
   | **[!UICONTROL Na Ativação]** | Quando os ativos são carregados para essa pasta, você deve publicar explicitamente o ativo primeiro, antes que um link de URL/Incorporação seja fornecido. Essa opção está vinculada somente à publicação no Experience Manager.<br>Esta opção está *não* disponível se você selecionou **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** em **[!UICONTROL Modo de sincronização]** na etapa anterior. |
   | **[!UICONTROL Publicação seletiva]** | Os Assets são publicados à sua escolha no Experience Manager ou no Dynamic Media para entrega no domínio público. Ambos os métodos de publicação são mutuamente exclusivos. Ou seja, você pode publicar ativos no DMS7 para usar recursos como Recorte inteligente ou representações dinâmicas. Ou você pode publicar ativos exclusivamente no Experience Manager para visualização segura; esses mesmos ativos *não* são publicados no DMS7 para entrega no domínio público. Esta opção não estará disponível se você tiver selecionado **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** no **[!UICONTROL modo de sincronização]** na etapa anterior. |

1. No canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]** e **[!UICONTROL OK]** para retornar ao Experience Manager Assets.

## Publicar ativos seletivamente no Dynamic Media ou no Experience Manager as a Cloud Service usando Gerenciar publicação{#selective-publish-manage-publication}

Antes de poder usar o **[!UICONTROL Gerenciar publicação]** para publicar seletivamente ativos no Dynamic Media ou no Experience Manager, verifique se você:

* Defina a opção **[!UICONTROL Publicar Assets]** em **[!UICONTROL Configuração do Dynamic Media]** para **[!UICONTROL Publicação seletiva]**.
* Ou então, a publicação seletiva configurada no nível da pasta.

Consulte [Criar uma configuração do Dynamic Media](#configuring-dynamic-media-cloud-services) ou [Configurar publicação seletiva no nível da pasta no Dynamic Media](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Copiar* ativos de e para pastas limpa o estado de publicação desses ativos. No entanto, quando você *move* ativos de e para pastas cuja propriedade de pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

**Para publicar seletivamente ativos no Dynamic Media ou no Experience Manager as a Cloud Service usando Gerenciar Publicação:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas) e vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de Cartão]**, **[!UICONTROL Exibição de Coluna]** ou **[!UICONTROL Exibição de Lista]**, siga um destes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Gerenciar Publicação]**. Use a **[!UICONTROL Exibição de Lista]** para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar Publicação]**. Use a **[!UICONTROL Exibição de lista]** para verificar mais facilmente o status de publicação de um ativo específico.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gerenciar Publicação]** não for exibido na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Gerenciar Publicação]** no menu da lista.

1. Na página **[!UICONTROL Gerenciar Publicação - Opções]**, em **[!UICONTROL Ação]**, selecione o tipo de ativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Publicar]** (no Experience Manager) | Para publicar ativos no Experience Manager para visualização segura, selecione essa opção. |
   | **[!UICONTROL Publicar no Dynamic Media]** | Para publicar ativos no Dynamic Media para entrega no domínio público ou para usar recursos como Recorte inteligente ou representações dinâmicas, selecione essa opção.<br>Esta opção estará disponível somente se o **[!UICONTROL Modo de publicação do Dynamic Media]** estiver definido como **[!UICONTROL Publicação seletiva]** nas propriedades da pasta. |

1. Em **[!UICONTROL Agendar]**, defina o tempo de publicação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para publicar os ativos imediatamente. |
   | **[!UICONTROL Mais tarde]** | Selecione para publicar os ativos em uma data e hora específicas. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação]**, selecione **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Gerenciar Publicação - Escopo]**, siga um destes procedimentos:
   * Se necessário, selecione um ou mais ativos que deseja remover da publicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar Publicação - Escopo]**, selecione **[!UICONTROL Publicar]** ou **[!UICONTROL Publicar no Dynamic Media]**.
1. Selecione **[!UICONTROL OK]**.

### Cancelar a publicação de ativos seletivamente do Dynamic Media ou do Experience Manager usando Gerenciar publicação {#selective-unpublish-manage-publication}

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas) e vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de Cartão]**, **[!UICONTROL Exibição de Coluna]** ou **[!UICONTROL Exibição de Lista]**, siga um destes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Gerenciar Publicação]**. Use a **[!UICONTROL Exibição de Lista]** para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar Publicação]**. Use a **[!UICONTROL Exibição de lista]** para verificar mais facilmente o status de publicação de um ativo específico.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gerenciar Publicação]** não for exibido na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Gerenciar Publicação]** no menu da lista.

1. Na página **[!UICONTROL Gerenciar Publicação - Opções]**, em **[!UICONTROL Ação]**, selecione o tipo de desativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Cancelar publicação]** (do Experience Manager) | Para cancelar a publicação de ativos do Experience Manager, selecione essa opção. |
   | **[!UICONTROL Cancelar publicação no Dynamic Media]** | Para cancelar a publicação de ativos do Dynamic Media, selecione essa opção.<br>Esta opção estará disponível somente se o **[!UICONTROL Modo de publicação do Dynamic Media]** estiver definido como **[!UICONTROL Publicação seletiva]** nas propriedades da pasta. |

1. Em **[!UICONTROL Agendar]**, defina o tempo de desativação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para cancelar a publicação dos ativos imediatamente. |
   | **[!UICONTROL Mais tarde]** | Selecione para desfazer a publicação dos ativos em uma data e hora específicas. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação]**, selecione **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Gerenciar Publicação - Escopo]**, siga um destes procedimentos:
   * Selecione um ou mais ativos que deseja remover da publicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar Publicação - Escopo]**, selecione **[!UICONTROL Cancelar Publicação]** ou **[!UICONTROL Cancelar Publicação do Dynamic Media]**.
1. Selecione **[!UICONTROL OK]**.

## Publicar ativos no Dynamic Media ou Experience Manager usando a Publicação rápida {#quick-publish-aem-dm}

Você pode usar a **[!UICONTROL Publicação rápida]** para casos de ativação de ativos simples. A **[!UICONTROL Publicação rápida]** publica os ativos selecionados imediatamente, sem qualquer outra interação com o usuário. As referências não publicadas também são publicadas automaticamente.

>[!NOTE]
>
>Para usar a **[!UICONTROL Publicação rápida]** para publicar ativos no Dynamic Media ou no Experience Manager, verifique se a **[!UICONTROL Publicação seletiva]** está habilitada na **[!UICONTROL Configuração do Dynamic Media]** ou nas propriedades de pasta da pasta selecionada.

**Para publicar ativos no Dynamic Media ou no Experience Manager usando a Publicação Rápida:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas) e, no lado direito da página, vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de Cartão]**, **[!UICONTROL Exibição de Coluna]** ou **[!UICONTROL Exibição de Lista]**, siga um destes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Use a **[!UICONTROL Exibição de Lista]** para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Use a **[!UICONTROL Exibição de lista]** para verificar mais facilmente o status de publicação de um ativo específico.

     >[!NOTE]
     >
     >Se a **[!UICONTROL Publicação rápida]** não for exibida na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Publicação rápida]** no menu de lista.

     ![Publicação rápida no nível de pasta no Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selecione uma das opções a seguir na lista de menus **[!UICONTROL Publicação Rápida]**.

   | opção Publicação rápida | O que faz |
   | --- | --- | 
   | Publicar no Experience Manager | Publica os ativos selecionados imediatamente no Experience Manager. |
   | Publicar no Brand Portal | Publica os ativos selecionados imediatamente no **[!UICONTROL Brand Portal]**.<br>Esta opção só estará disponível se a instância do Experience Manager Assets já tiver o **[!UICONTROL Brand Portal]** configurado. |
   | Publicar no Dynamic Media | Publica os ativos selecionados imediatamente no Dynamic Media.<br>Um ativo já deve estar sincronizado com o Dynamic Media. Se necessário, verifique se o **[!UICONTROL Modo de sincronização]** nas propriedades de uma pasta já está definido como **[!UICONTROL Sincronizar tudo nesta subárvore de pasta com o Dynamic Media]**. |

1. Selecione **[!UICONTROL OK]** e **[!UICONTROL Fechar]**.

## Publicar ou cancelar a publicação de ativos de maneira seletiva por meio dos resultados da pesquisa {#selective-publish-unpublish-search-results}

Os resultados da pesquisa podem mostrar ativos de várias pastas de ativos que têm configurações de publicação diferentes do Dynamic Media. Quando você tiver selecionado um ou mais ativos nos resultados da pesquisa e os ativos tiverem diferentes configurações de modo de publicação do Dynamic Media, será possível acionar **[!UICONTROL Gerenciar publicação]** na barra de ferramentas para publicar ou desfazer a publicação.

Consulte também [Pesquisar ativos no Experience Manager](/help/assets/search-assets.md).

**Para publicar ou desfazer a publicação seletiva de ativos por meio dos resultados da pesquisa:**

1. No Experience Manager, no canto superior esquerdo da página, selecione o logotipo do Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas) e vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Na barra de ferramentas, próximo ao canto superior direito da página, selecione o ícone Pesquisar (lupa).
1. No campo de texto **[!UICONTROL Digite para pesquisar]**, digite uma palavra-chave e pressione **[!UICONTROL Enter]**.
1. Próximo ao canto superior direito da página, selecione o ícone **[!UICONTROL Exibição de lista]**.
1. Próximo ao canto superior esquerdo da página, selecione o ícone **[!UICONTROL Filtros]**.

   ![Exibição de Lista e Filtros nos resultados da pesquisa](/help/assets/assets-dm/select-publish-search-result.png)

1. No painel esquerdo, expanda **[!UICONTROL Status]** e expanda o predicado de pesquisa **[!UICONTROL Dynamic Media]**.
1. Use as caixas de seleção **[!UICONTROL Publicado]** e **[!UICONTROL Não publicado]** para refinar ainda mais os resultados da pesquisa com base no estado publicado dos ativos do Dynamic Media.
Como opção, você pode usar essas caixas de seleção com o predicado de pesquisa **[!UICONTROL Publicar]** para refinar os resultados da pesquisa de ativos do Experience Manager **[!UICONTROL Publicados]** e **[!UICONTROL Não publicados]**.
1. Siga uma das seguintes opções:
   * Selecione um ou mais ativos que deseja publicar ou cancelar a publicação.
   * Próximo ao canto superior direito da página **[!UICONTROL Resultados da Pesquisa]**, selecione **[!UICONTROL Selecionar Tudo]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar Publicação]**. Se necessário, selecione o ícone de reticências na barra de ferramentas para ver **[!UICONTROL Gerenciar publicação]**.
1. Na página **[!UICONTROL Gerenciar Publicação - Opções]**, selecione a ação desejada.

   | Ação selecionada | Publicar a configuração do Assets na configuração do Dynamic Media | Assets são |
   | --- | --- | --- |
   | Publicação | Imediatamente ou Após ativação | Publicado no Experience Manager e no Dynamic Media. |
   | Publicação | Publicação seletiva | Publicado somente no Experience Manager. |
   | Desfazer publicação | Imediatamente ou Após ativação | A publicação desse item no Experience Manager e no Dynamic Media foi desfeita. |
   | Desfazer publicação | Publicação seletiva | Publicação cancelada somente no Experience Manager. |
   | Publicar no Dynamic Media | Imediatamente ou Após ativação | Não publicado no Experience Manager, Dynamic Media ou ambos. |
   | Publicar no Dynamic Media | Publicação seletiva | Publicado somente no Dynamic Media. |
   | Desfazer publicação no Dynamic Media | Imediatamente ou Após ativação | Não ter a publicação desfeita do Experience Manager, Dynamic Media ou ambos. |
   | Desfazer publicação no Dynamic Media | Publicação seletiva | A publicação desse item foi desfeita somente no Dynamic Media. |

1. Em **[!UICONTROL Agendar]**, defina o tempo de desativação.

   | Agendamento selecionado | O que acontece |
   | --- | --- |
   | Agora | A ação selecionada é executada imediatamente. |
   | Posteriormente | A ação selecionada é executada na data e hora específicas selecionadas. |

1. No canto superior direito da página **[!UICONTROL Gerenciar Publicação - Opções]**, selecione **[!UICONTROL Avançar]**.
1. (Opcional) Na página **[!UICONTROL Gerenciar publicação - Escopo]**, revise a coluna **[!UICONTROL Destino de publicação]** na tabela para os ativos selecionados.

   | Publicar a configuração do Assets na configuração do Dynamic Media | Ação selecionada | Destino de publicação |
   | --- | --- | --- |
   | Imediatamente ou <br>Após a Ativação | Publicação | Experience Manager e Dynamic Media |
   | Imediatamente ou <br>Após a Ativação | Publicar no Dynamic Media | Nenhum |
   | Publicação seletiva | Publicação | Experience Manager |
   | Publicação seletiva | Publicar no Dynamic Media | Dynamic Media |
   | Imediatamente ou <br>Após a Ativação | Desfazer publicação | Experience Manager e Dynamic Media |
   | Imediatamente ou <br>Após a Ativação | Desfazer publicação no Dynamic Media | Nenhum |
   | Publicação seletiva | Desfazer publicação | Experience Manager |
   | Publicação seletiva | Desfazer publicação no Dynamic Media | Dynamic Media |

1. Na página **[!UICONTROL Gerenciar Publicação - Escopo]**, siga um destes procedimentos:
   * Selecione um ou mais ativos que deseja remover da publicação ou do cancelamento da publicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar Publicação - Escopo]**, selecione **[!UICONTROL Publicar]** ou **[!UICONTROL Cancelar Publicação]** para iniciar a ação.
1. Selecione **[!UICONTROL OK]**.

## Verificar o status de publicação de um ativo {#check-publish-status-of-asset}

Você pode usar a **[!UICONTROL Linha do Tempo]** com a **[!UICONTROL Exibição de cartão]**, a **[!UICONTROL Exibição de coluna]** ou a **[!UICONTROL Exibição de lista]** no Experience Manager para verificar rapidamente o estado de publicação de um ativo.

**Para verificar o status de publicação de um ativo:**

1. No Experience Manager, no canto superior esquerdo da página, selecione o logotipo do Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas) e vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de Cartão]**, **[!UICONTROL Exibição de Coluna]** ou **[!UICONTROL Exibição de Lista]** (a captura de tela abaixo mostra a **[!UICONTROL Exibição de Lista]**), abra uma pasta que contenha ativos publicados ou não.
1. Selecione um ativo para que ele apareça com uma marca de seleção. Consulte a captura de tela abaixo para obter um exemplo.
1. Próximo ao canto superior esquerdo da página, no menu suspenso, selecione **[!UICONTROL Linha do tempo]**. A região **[!UICONTROL Status]** no painel esquerdo mostra o estado de publicação do ativo selecionado.
Quando você usa a **[!UICONTROL Exibição de Lista]**, uma coluna extra para o estado de publicação do **[!UICONTROL Dynamic Media]** é exibida.
   * Uma pasta configurada para sincronização com o Dynamic Media exibe a coluna **[!UICONTROL Dynamic Media]** por padrão.
   * Uma pasta *não* configurada para sincronização com o Dynamic Media não exibe a coluna Dynamic Media.
     ![Modo de Exibição de Lista e Linha do Tempo](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solução de problemas de publicação seletiva {#selective-publish-troubleshoot}

Um ativo que não está sincronizado com o Dynamic Media, mas tem uma ação de publicação do Dynamic Media acionada, resulta na seguinte mensagem de erro e solução:

![Erro de publicação seletiva](/help/assets/assets-dm/selective-publish-error.png)
