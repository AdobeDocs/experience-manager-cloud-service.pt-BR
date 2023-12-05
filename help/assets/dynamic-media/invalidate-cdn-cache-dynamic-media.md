---
title: Invalidar o cache da rede de entrega de conteúdo por meio do Dynamic Media
description: Saiba como invalidar o conteúdo em cache do CDN (Content Delivery Network) para permitir que você atualize rapidamente os ativos entregues pelo Dynamic Media, em vez de esperar a expiração do cache.
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 1%

---

# Invalidar o cache da CDN por meio do Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Os ativos do Dynamic Media são armazenados em cache pela CDN (Content Delivery Network) para entrega rápida aos clientes. No entanto, ao atualizar esses ativos, você deseja que essas alterações entrem em vigor imediatamente no site. A limpeza ou invalidação do cache CDN permite atualizar rapidamente os ativos entregues pelo Dynamic Media. Não é mais necessário aguardar a expiração do cache usando um valor TTL (Time To Live) (o padrão é dez horas). Em vez disso, você pode enviar uma solicitação de dentro da interface do usuário do Dynamic Media para que o cache expire em minutos.

>[!NOTE]
>
>Esse recurso exige que você use o CDN em pacote de Adobe que vem com o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso.

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

Se você ativou [Imagem inteligente](/help/assets/dynamic-media/imaging-faq.md) em sua conta e estiver usando o CDN agrupado por Adobe, você poderá limpar todos os URLs com diferentes cadeias de caracteres de consulta limpando o URL de base única.

Por exemplo, invalidar `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`, também invalida os seguintes URLs:

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* e assim por diante.

No entanto, esse não é o caso para domínios genéricos que não oferecem suporte à Imagem inteligente, como `s7d1.scene7.com`. Esses domínios ainda precisam do URL completo para que a invalidação funcione com êxito.

**Para invalidar o cache CDN por meio do Dynamic Media:**

*Parte 1 de 2: Criação de um modelo de Invalidação da CDN*

1. No Adobe Experience Manager as a Cloud Service, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Modelo de invalidação da CDN]**.

   ![Recurso de validação da CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. No **[!UICONTROL Modelo de invalidação da CDN]** execute uma das seguintes opções com base no seu cenário:

   | Cenário | Opção |
   | --- | --- |
   | Já criei um modelo de invalidação CDN no passado usando o Dynamic Media Classic. | A variável **[!UICONTROL Criar modelo]** O campo de texto é pré-preenchido com os dados do modelo. Nesse caso, você pode editar o modelo ou continuar para a próxima etapa. |
   | Preciso criar um template. O que eu insiro? | No **[!UICONTROL Criar modelo]** campo de texto, insira um URL de imagem (incluindo predefinições de imagem ou modificadores) que faça referência `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se o modelo contiver apenas `<ID>`, então o Dynamic Media preenche `https://<publishserver_name>/is/image/<company_name>/<ID>` onde `<publishserver_name>` é o nome do servidor de publicação definido em Configurações gerais no Dynamic Media Classic. A variável `<company_name>` é o nome da raiz da empresa associada a essa instância do Experience Manager e `<ID>` Os ativos selecionados por meio do seletor de ativos estão sendo invalidados.<br>Quaisquer predefinições/modificadores após `<ID>` são copiados como estão na definição do URL.<br>Somente imagens, ou seja, `/is/image`- pode ser formado automaticamente com base no modelo.<br>Para `/is/content/`, a adição de ativos como vídeos ou PDF usando o seletor de ativos não gera URLs automaticamente. Em vez disso, você deve especificar esses ativos no modelo de Invalidação da CDN ou pode adicionar manualmente o URL a esses ativos no *Parte 2 de 2: Definição de opções de invalidação de CDN*.<br>**Exemplos:**<br> Neste primeiro exemplo, o template de invalidação contém `<ID>` juntamente com o URL do ativo com `/is/content`. Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. O Dynamic Media forma o URL com base nesse caminho, com `<ID>` são os ativos selecionados por meio do seletor de ativos que você deseja invalidar.<br>Neste segundo exemplo, o modelo de invalidação contém o URL completo do ativo usado nas propriedades da Web com `/is/content` (não depende do seletor de ativos). Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` onde backpack é a ID do ativo.<br>Os formatos de ativos compatíveis com o Dynamic Media são qualificados para invalidação. Tipos de arquivos de ativos que são *não* Os compatíveis com a invalidação de CDN incluem PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word e Rich Text Format.<br><br>· Ao criar o modelo, mas preste muita atenção à sintaxe e aos erros de digitação; o Dynamic Media não faz nenhuma validação de modelo.<br>· O Modelo de invalidação da CDN pode salvar texto de até 2500 caracteres.<br>· Especifique URLs para cortes inteligentes de imagem neste modelo de Invalidação da CDN ou no **[!UICONTROL Adicionar URL]** campo de texto em *Parte 2: Definir opções de invalidação da CDN.*<br>· Cada entrada em um modelo de Invalidação da CDN deve estar em sua própria linha.<br>· O seguinte exemplo de modelo de Invalidação de CDN é somente para fins de demonstração. |

   ![Modelo de invalidação da CDN - Criar](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >O Modelo de invalidação da CDN pode salvar texto de até 2500 caracteres.

1. No canto superior direito da **[!UICONTROL Modelo de invalidação da CDN]** selecione **[!UICONTROL Salvar]** e selecione **[!UICONTROL OK]**.<br>
   *Parte 2 de 2: Definição de opções de invalidação de CDN*
   <br>

1. No Experience Manager as a Cloud Service, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidação da CDN]**.

   ![Recurso de validação da CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. No **[!UICONTROL Invalidação da CDN]** - **[!UICONTROL Adicionar detalhes]** selecione os ativos para invalidação da CDN.

   ![Invalidação da CDN - Adicionar detalhes](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se você decidir deixar as opções **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** *e* **[!UICONTROL Invalidar com base no modelo]** desmarcada, o URL básico dos ativos selecionados é formado para invalidação. Use esta organização de opção somente para imagens.


   | Opção | Descrição |
   | --- | --- |
   | **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** | (Opcional) Ao marcar essa opção, os ativos selecionados e todos os URLs de predefinição de imagem associados são formados automaticamente para invalidação de cache.<br>Os ativos e seus URLs predefinidos predefinidos associados são formados automaticamente para invalidação. Essa opção funciona somente para ativos de imagem. |
   | **[!UICONTROL Invalidação com base no modelo]** | (Opcional) Marque essa opção para usar somente o modelo definido para a formação de URL. |
   | **[!UICONTROL Adicionar ativos]** | Use o Seletor de ativos para selecionar os ativos que deseja invalidar. Você pode selecionar ativos publicados ou não publicados.<br>O armazenamento em cache na CDN é baseado em URL, não em ativo. Portanto, é necessário que você esteja ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los ao modelo. Em seguida, você pode selecionar e adicionar esses ativos e invalidar os URLs em uma etapa. <br>Use esta opção com **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** ou **[!UICONTROL Invalidação com base no modelo]**, ou ambos. |
   | **[!UICONTROL Adicionar URL]** | Adicione ou cole manualmente caminhos completos de URL para ativos do Dynamic Media cujo cache do CDN você deseja invalidar. Use essa opção se você não criou um Modelo de invalidação CDN no ***Parte 1 de 2: Criação de um modelo de Invalidação da CDN*** e têm apenas alguns ativos para invalidar.<br>**Importante:** Cada URL que você adicionar deve estar em sua própria linha.<br>Você pode invalidar até 1000 URLs em um determinado momento. Se o número de URLs na variável **[!UICONTROL Adicionar URL]** o campo de texto for maior que 1000, você não poderá selecionar **[!UICONTROL Próxima]**. Nesses casos, você deve selecionar **[!UICONTROL X]** à direita de um ativo selecionado ou de um URL adicionado manualmente para excluí-lo da lista de invalidação.<br>Especifique URLs para cortes inteligentes de imagem no modelo de Invalidação da CDN ou neste **[!UICONTROL Adicionar URL]** campo de texto. |

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Próxima]**.
1. No **[!UICONTROL Invalidação da CDN]** - **[!UICONTROL Confirmar o]** página, no campo **[!UICONTROL URLs]** , você verá uma lista de um ou mais URLs gerados a partir do Modelo de invalidação CDN criado anteriormente e dos ativos que você acabou de adicionar.

   Por exemplo, usando o exemplo de Modelo de invalidação CDN que foi mostrado nas etapas anteriores, suponha que você tenha adicionado um único ativo chamado `spinset`. Quando você vai para o **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidação da CDN]**, isso resulta nos cinco URLs gerados a seguir no **[!UICONTROL Invalidação da CDN - Confirmar]** interface do usuário:

   ![Invalidação da CDN - Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessário, selecione **X** à direita de um URL para excluí-lo do processo de invalidação.

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Enviar]** para iniciar o processo de invalidação da CDN.

## Solução de problemas de erros de invalidação da CDN

Em todos os casos, o lote inteiro é processado para invalidação ou o lote inteiro falha.

| Erro | Explicação |
| --- | --- |
| *Falha ao recuperar URLs dos ativos selecionados.* | Ocorre se qualquer um dos seguintes cenários for atendido:<br>- Uma configuração Dynamic Media não foi encontrada.<br>- Há uma exceção ao recuperar um usuário de serviço por meio do qual a configuração do Dynamic Media é lida.<br>- O servidor de publicação ou a raiz da empresa usada para formar os URLs está ausente na configuração do Dynamic Media. |
| *Alguns URLs não estão definidos corretamente. Corrija e envie novamente.* | Ocorre se a API de invalidação do cache CDN do IPS retornar um erro. O erro indica que o URL se refere a uma empresa diferente ou o URL não é válido de acordo com a validação feita pela API cdnCacheInvalidation do IPS. |
| *Falha ao invalidar o cache da CDN.* | Ocorre se a solicitação de invalidação de cache CDN falhar por qualquer outro motivo. |
| *Nenhum URL inserido para ser invalidado.* | Ocorre se não houver URLs na variável **[!UICONTROL Invalidação da CDN]** - **[!UICONTROL Confirmar o]** e selecione **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. While you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
