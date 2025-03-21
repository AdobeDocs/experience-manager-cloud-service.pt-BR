---
title: Invalidar o cache da rede de entrega de conteúdo por meio do Dynamic Media
description: Saiba como invalidar o conteúdo em cache do CDN (Content Delivery Network) para permitir que você atualize rapidamente os ativos entregues pelo Dynamic Media, em vez de esperar a expiração do cache.
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 1%

---

# Invalidar o cache da CDN por meio do Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

Os ativos do Dynamic Media são armazenados em cache pela CDN (Content Delivery Network) para entrega rápida aos clientes. No entanto, ao atualizar esses ativos, você deseja que essas alterações entrem em vigor imediatamente no site. A limpeza ou invalidação do cache CDN permite atualizar rapidamente os ativos entregues pelo Dynamic Media. Não é mais necessário aguardar a expiração do cache usando um valor TTL (Time To Live) (o padrão é dez horas). Em vez disso, você pode enviar uma solicitação da interface do usuário do Dynamic Media para que o cache expire em minutos.

>[!NOTE]
>
>Esse recurso exige que você use a CDN fornecida pela Adobe que acompanha o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso.

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

Se você habilitou o [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) em sua conta e está usando a CDN agrupada em Adobe, é possível limpar todos os URLs com diferentes cadeias de caracteres de consulta, limpando o URL de base única.

Por exemplo, invalidar `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image` também invalida as seguintes URLs:

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* e assim por diante.

No entanto, esse não é o caso para domínios genéricos que não oferecem suporte para Smart Imaging, como `s7d1.scene7.com`. Esses domínios ainda precisam do URL completo para que a invalidação funcione com êxito.

**Para invalidar o cache CDN por meio do Dynamic Media:**

*Parte 1 de 2: Criando um modelo de Invalidação da CDN*

1. No Adobe Experience Manager as a Cloud Service, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Modelo de Invalidação da CDN]**.

   ![Recurso de validação da CDN](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Na página **[!UICONTROL Modelo de invalidação da CDN]**, execute uma das seguintes opções com base no seu cenário:

   | Cenário | Opção |
   | --- | --- |
   | Já criei um modelo de invalidação CDN no passado usando o Dynamic Media Classic. | O campo de texto **[!UICONTROL Criar Modelo]** é preenchido automaticamente com seus dados de modelo. Nesse caso, você pode editar o modelo ou continuar para a próxima etapa. |
   | Preciso criar um template. O que eu insiro? | No campo de texto **[!UICONTROL Criar Modelo]**, insira uma URL de imagem (incluindo predefinições de imagem ou modificadores) que faça referência a `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se o modelo contiver apenas `<ID>`, o Dynamic Media preencherá `https://<publishserver_name>/is/image/<company_name>/<ID>`, onde `<publishserver_name>` é o nome do seu Servidor de Publicação definido em Configurações Gerais no Dynamic Media Classic. O `<company_name>` é o nome da raiz da sua empresa associada a esta instância do Experience Manager e `<ID>` são os ativos selecionados por meio do seletor de ativos a serem invalidados.<br>Quaisquer predefinições/modificadores após `<ID>` são copiados como estão na definição de URL.<br>Somente imagens, ou seja, `/is/image`, podem ser formadas automaticamente com base no modelo.<br>Para `/is/content/`, adicionar ativos como vídeos ou PDFs usando o seletor de ativos não gera URLs automaticamente. Em vez disso, você deve especificar esses ativos no modelo de Invalidação da CDN ou pode adicionar manualmente a URL a esses ativos em *Parte 2 de 2: Definindo opções de Invalidação da CDN*.<br>**Exemplos:**<br> Neste primeiro exemplo, o modelo de invalidação contém `<ID>` junto com a URL do ativo que tem `/is/content`. Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. O Dynamic Media forma a URL com base nesse caminho, sendo `<ID>` os ativos selecionados por meio do seletor de ativos que você deseja invalidar.<br>Neste segundo exemplo, o modelo de invalidação contém a URL completa do ativo usado em suas propriedades da Web com `/is/content` (não depende do seletor de ativos). Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` onde backpack é a ID do ativo.<br>Os formatos de ativos com suporte no Dynamic Media estão qualificados para invalidação. Os tipos de arquivos de ativos que *não* são compatíveis com a invalidação da CDN incluem PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word e Rich Text Format.<br><br>· Ao criar o modelo, mas preste muita atenção à sintaxe e aos erros de digitação; o Dynamic Media não faz nenhuma validação de modelo.<br>· O Modelo de Invalidação da CDN pode salvar texto de até 2500 caracteres.<br>· Especifique as URLs para recortes inteligentes de imagem neste modelo de Invalidação de CDN ou no campo de texto **[!UICONTROL Adicionar URL]** em *Parte 2: Definição de opções de Invalidação de CDN.*<br>· Cada entrada em um modelo de Invalidação CDN deve estar em sua própria linha.<br>· O exemplo de modelo de Invalidação da CDN a seguir é somente para fins de demonstração. |

   ![Modelo de invalidação da CDN - Criar](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >O Modelo de invalidação da CDN pode salvar texto de até 2500 caracteres.

1. No canto superior direito da página **[!UICONTROL Modelo de invalidação da CDN]**, selecione **[!UICONTROL Salvar]** e **[!UICONTROL OK]**.<br>
   *Parte 2 de 2: Definindo opções de Invalidação da CDN*
   <br>

1. No Experience Manager as a Cloud Service, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidação de CDN]**.

   ![Recurso de validação da CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Na página **[!UICONTROL Invalidação de CDN]** - **[!UICONTROL Adicionar Detalhes]**, selecione os ativos para invalidação de CDN.

   ![Invalidação da CDN - Adicionar Detalhes](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se você decidir deixar as opções **[!UICONTROL Invalidar predefinições de imagens associadas a ativos na CDN]** *e* **[!UICONTROL Invalidar com base no modelo]** desmarcadas, a URL de base dos ativos selecionados será formada para invalidação. Use esta organização de opção somente para imagens.


   | Opção | Descrição |
   | --- | --- |
   | **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** | (Opcional) Ao marcar essa opção, os ativos selecionados e todos os URLs de predefinição de imagem associados são formados automaticamente para invalidação de cache.<br>O Assets e suas URLs predefinidas predefinidas associadas são formados automaticamente para invalidação. Essa opção funciona somente para ativos de imagem. |
   | **[!UICONTROL Invalidação baseada no modelo]** | (Opcional) Marque essa opção para usar somente o modelo definido para a formação de URL. |
   | **[!UICONTROL Adicionar Assets]** | Use o Seletor de ativos para selecionar os ativos que deseja invalidar. Você pode selecionar ativos publicados ou não publicados.<br>O armazenamento em cache na CDN é baseado em URL e não em ativo. Portanto, é necessário que você esteja ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los ao modelo. Em seguida, você pode selecionar e adicionar esses ativos e invalidar os URLs em uma etapa. <br>Use esta opção com **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]**, ou **[!UICONTROL Invalidação com base no modelo]**, ou ambos. |
   | **[!UICONTROL Adicionar URL]** | Adicione ou cole manualmente caminhos completos de URL para ativos do Dynamic Media cujo cache de CDN você deseja invalidar. Use essa opção se você não tiver criado um Modelo de Invalidação CDN em ***Parte 1 de 2: Criação de um Modelo de Invalidação CDN*** e tiver apenas alguns ativos para invalidar.<br>**Importante:** cada URL adicionado deve estar em sua própria linha.<br>Você pode invalidar até 1000 URLs em um determinado momento. Se o número de URLs no campo de texto **[!UICONTROL Adicionar URL]** for maior que 1000, você não poderá selecionar **[!UICONTROL Avançar]**. Nesses casos, você deve selecionar **[!UICONTROL X]** à direita de um ativo selecionado ou uma URL adicionada manualmente para excluí-lo da lista de invalidação.<br>Especifique as URLs para cortes inteligentes de imagem no modelo de Invalidação CDN ou neste campo de texto **[!UICONTROL Adicionar URL]**. |

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Invalidação de CDN]** - **[!UICONTROL Confirmar]**, na caixa de listagem **[!UICONTROL URLs]**, você verá uma lista de uma ou mais URLs geradas a partir do Modelo de Invalidação de CDN criado anteriormente e dos ativos que você acabou de adicionar.

   Por exemplo, usando o exemplo de Modelo de invalidação CDN mostrado nas etapas anteriores, suponha que você tenha adicionado um único ativo chamado `spinset`. Ao acessar **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Invalidação de CDN]**, você obterá as cinco URLs geradas a seguir na interface de usuário **[!UICONTROL Invalidação de CDN - Confirmar]**:

   ![Invalidação da CDN - Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessário, selecione **X** à direita de uma URL para excluí-la do processo de invalidação.

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Enviar]** para iniciar o processo de invalidação da CDN.

## Solução de problemas de erros de invalidação da CDN

Em todos os casos, o lote inteiro é processado para invalidação ou o lote inteiro falha.

| Erro | Explicação |
| --- | --- |
| *Falha ao recuperar as URLs dos ativos selecionados.* | Ocorre se qualquer um dos seguintes cenários for atendido:<br>- Uma configuração do Dynamic Media não foi encontrada.<br>- Há uma exceção ao recuperar um usuário de serviço por meio do qual a configuração do Dynamic Media é lida.<br>- O servidor de publicação ou a raiz da empresa usada para formar as URLs está ausente na configuração do Dynamic Media. |
| *Algumas URLs não estão definidas corretamente. Corrigir e reenviar.* | Ocorre se a API de invalidação do cache CDN do IPS retornar um erro. O erro indica que o URL se refere a uma empresa diferente ou o URL não é válido de acordo com a validação feita pela API cdnCacheInvalidation do IPS. |
| *Falha ao invalidar o cache da CDN.* | Ocorre se a solicitação de invalidação de cache CDN falhar por qualquer outro motivo. |
| *Nenhuma URL inserida para ser invalidada.* | Ocorre se não houver URLs na página **[!UICONTROL Invalidação de CDN]** - **[!UICONTROL Confirmar]** e você selecionar **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. While you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
