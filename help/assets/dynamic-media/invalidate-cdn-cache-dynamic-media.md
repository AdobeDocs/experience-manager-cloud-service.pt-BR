---
title: Invalidar o cache CDN por meio do Dynamic Media
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pelo Dynamic Media, em vez de aguardar a expiração do cache.
translation-type: tm+mt
source-git-commit: 68ee2c58588ad519aac673652349e0fefd20ee57
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---


# Invalidar o cache CDN por meio do Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Os ativos de Mídia dinâmica são armazenados em cache pelo CDN (Content Delivery Network) para delivery rápido aos seus clientes. No entanto, ao fazer atualizações nesses ativos, você pode desejar que essas alterações entrem em vigor imediatamente em seu site. Limpar ou invalidar o cache de CDN permite que você atualize rapidamente os ativos entregues pelo Dynamic Media. Em vez de esperar que o cache expire usando um valor TTL (Time To Live) (o padrão é 10 horas), você pode enviar uma solicitação da interface do usuário do Dynamic Media para que o cache expire em minutos.

>[!IMPORTANT]
>
>As etapas a seguir se aplicam somente ao Dynamic Media em AEM como Cloud Service. Você também deve usar o CDN predefinido que está fornecido com AEM Dynamic Media. Nenhum outro CDN personalizado é suportado por este recurso. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Consulte também Visão geral do [cache no Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o cache CDN por meio da mídia dinâmica**

*Parte 1: Criando um modelo de Invalidação CDN*

1. Em AEM como Cloud Service, toque em **[!UICONTROL Ferramentas > Ativos > Modelo de invalidação CDN.]**

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Na página Modelo **[!UICONTROL de Invalidação de]** CDN, execute uma das seguintes opções com base no seu cenário:

   | Cenário | Opção |
   | --- | --- |
   | Já criei um Modelo de Invalidação CDN no passado usando o Dynamic Media Classic. | O campo de texto **[!UICONTROL Criar modelo]** é preenchido previamente com os dados do modelo. Nesse caso, você pode editar o modelo ou continuar para a próxima etapa. |
   | Preciso criar um modelo. Em que eu entro? | No campo de texto **[!UICONTROL Criar modelo]** , insira um URL de imagem (incluindo predefinições de imagens ou modificadores) que faça referência `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:<br><br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br><br>Se o modelo apenas contiver `<ID>`, o Dynamic Media preencherá `https://<publishserver_name>/is/image` onde `<publishserver_name>` é o nome do Servidor de publicação e `ID` serão os ativos selecionados para invalidar.<br><br>Somente as imagens, ou seja, `/is/image`- podem ser formadas automaticamente com base no modelo. Por exemplo, `/is/content/`adicionar ativos como vídeos ou PDFs usando o seletor de ativos não gera URLs automaticamente. Em vez disso, você deve especificar tais ativos no modelo de Invalidação CDN ou pode adicionar manualmente o URL a esses ativos na *Parte 2: Definindo opções* de Invalidação de CDN.<br>Os formatos de ativos compatíveis com o Dynamic Media são elegíveis para invalidação. Ativos como PowerPoints ou arquivos de texto sem formatação não são ativos compatíveis com a invalidação de CDN.<br>Ao criar o modelo, mas certifique-se de prestar atenção à sintaxe e erros de digitação; O Dynamic Media não faz nenhuma validação de modelo.<br>O exemplo de modelo a seguir serve apenas para fins ilustrativos. |

   ![Modelo de Invalidação CDN - Criar](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. No canto superior direito da página Modelo de Invalidação CDN, toque em **[!UICONTROL Salvar]** e, em seguida, toque em **[!UICONTROL OK]**.

   *Parte 2: Definindo opções de invalidação de CDN*

1. Em AEM como um Cloud Service, toque em **[!UICONTROL Ferramentas > Ativos > Invalidação de CDN.]**

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Na página Invalidação **[!UICONTROL de]** CDN - **[!UICONTROL Adicionar detalhes]** , selecione os ativos para invalidação de CDN.

   ![Invalidação de CDN - Adicionar Detalhes](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se você decidir deixar as opções **[!UICONTROL Invalidar predefinições de imagens associadas a ativos em CDN]** *e* Invalidar com base no modelo **** desmarcadas, o URL base dos ativos selecionados será formado para invalidação. Você deve usar essa organização de opção apenas para imagens.


   | Opção | Descrição |
   | --- | --- |
   | **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** | (Opcional) Ao marcar essa opção, você pode selecionar um ou mais ativos de Dynamic Media, independentemente do tipo MIME e das predefinições de imagem associadas para a invalidação do cache.<br>Os ativos e seus URLs predefinidos associados são formados automaticamente para invalidação. Essa opção funciona somente para<br>ativos de imagemEmbora seja possível selecionar uma ou mais pastas que contenham ativos, o Adobe não recomenda essa abordagem. Em vez disso, você deve selecionar arquivos de ativos individuais. |
   | **[!UICONTROL Invalidação com base no modelo]** | (Opcional) Marque essa opção para usar somente o modelo definido para a formação de URL. |
   | **[!UICONTROL Adicionar ativos]** | Use o Seletor de ativos para selecionar ativos que deseja invalidar. Você pode selecionar ativos publicados ou não publicados.<br>Você pode obter uma lista em branco ao adicionar ativos. O Dynamic Media usa o Modelo de Invalidação CDN para criar automaticamente o URL para invalidar o CDN. Se nenhum Modelo de Invalidação de CDN tiver sido criado, você receberá uma lista em branco.<br>O cache no CDN é baseado em URL, não em ativos. Portanto, é necessário que você esteja ciente dos URLs completos que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los ao modelo.Em seguida, você pode selecionar e adicionar esses ativos e invalidar os URLs em uma etapa. A outra opção é adicionar URLs à lista de Invalidação CDN. Se preferir essa abordagem, não é necessário selecionar e adicionar ativos antes de tocar em **[!UICONTROL Próximo]** e, em seguida, em **[!UICONTROL Enviar]** para invalidação.<br>Use essa opção em conjunto com as predefinições de imagens associadas ao ativo **[!UICONTROL Invalidar no CDN]**, ou **[!UICONTROL Invalidar com base no modelo]**, ou em ambos. |
   | **[!UICONTROL Adicionar URL]** | Adicione ou cole manualmente caminhos de URL completos em ativos do Dynamic Media cujo cache de CDN você deseja invalidar. Use esta opção se você não tiver criado um Modelo de Invalidação CDN na ***Parte 1: Trabalhando com o Modelo*** de Invalidação CDN e tendo apenas alguns ativos para invalidar.<br> |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next]**.
1. Na página Invalidação **[!UICONTROL de]** CDN - **[!UICONTROL Confirmar]** , na caixa lista **[!UICONTROL URLs]** , você verá uma lista de um ou mais URLs gerados a partir do Modelo de Invalidação de CDN criado anteriormente e dos ativos que você acabou de adicionar.

   Por exemplo, com o Modelo de Invalidação CDN criado anteriormente, suponha que você tenha adicionado um único ativo chamado `spinset`. Quando você toca em **[!UICONTROL Ferramentas > Ativos > Invalidação]** de CDN, isso resulta nos cinco seguintes URLs gerados na **[!UICONTROL Invalidação de CDN - Confirmar]** interface do usuário:

   ![Invalidação de CDN - Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessário, toque no **X** à direita de um URL para excluí-lo do processo de invalidação. Você pode ter até 1000 URLs em um determinado momento.

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Enviar]** para iniciar o processo de invalidação de CDN.

## Solução de problemas de erros de invalidação de CDN

* Esse recurso permite que você invalide até 1000 URLs em um determinado momento. Um número maior que 1000 resulta em um erro que pode ser resolvido ao excluir URLs na página **[!UICONTROL CDN Invalidation - Confirm]** .
* Em todos os casos, o lote inteiro é processado para invalidação ou todo o lote falhou.

| Erro | Explicação |
| --- | --- |
| *Falha ao recuperar URL(s) para ativos selecionados.* | Ocorre se qualquer uma das seguintes situações for atendida:<br>- Uma configuração de Dynamic Media não foi encontrada.<br>- Há uma exceção ao recuperar um usuário de serviço através do qual a configuração do Dynamic Media é lida.<br>- O servidor de publicação ou a raiz de empresa usada para formar os URLs está ausente na configuração do Dynamic Media. |
| *Alguns URLs não estão definidos corretamente. Corrija e envie novamente.* | Ocorre se a API de invalidação do cache CDN IPS retornar um erro de que o URL está fazendo referência a uma empresa diferente ou se o URL não é válido de acordo com a validação feita pela API cdnCacheInvalidation IPS. |
| *Falha ao invalidar o cache de CDN.* | Ocorre se a solicitação de invalidação do cache CDN falhar por qualquer outro motivo. |
| *Nenhum URL inserido para ser invalidado.* | Ocorre se não houver URLs presentes na página **[!UICONTROL de Invalidação do]** CDN - Confirmar e você tocar em **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->