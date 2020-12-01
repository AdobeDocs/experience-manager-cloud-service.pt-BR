---
title: Gerenciamento dos fragmentos de conteúdo
description: Os Fragmentos de conteúdo são armazenados como Ativos, portanto, são gerenciados principalmente no console Ativos.
translation-type: tm+mt
source-git-commit: 0a60687eacf054675205d9a9466473e1f4996db1
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 11%

---


# Gerenciamento dos fragmentos de conteúdo{#managing-content-fragments}

<!--
>[!CAUTION]
>
>Certain features for Content Fragments will be released in early 2021.
>
>The related documentation is already available for preview purposes.
>
>Please see the [Release Notes](/help/release-notes/release-notes-cloud/release-notes-current.md) for further details.
-->

>[!CAUTION]
>
>A API AEM GraphQL, para o Delivery de fragmento de conteúdo, será lançada no início de 2021.
>
>A documentação relacionada já está disponível para fins de pré-visualização.

Os Fragmentos de conteúdo são armazenados como **Ativos**, portanto, são gerenciados principalmente do console **Ativos**.

>[!NOTE]
>
>Fragmentos de conteúdo podem ser usados:
>
>* ao criar páginas; consulte [Criação de página com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* para [Delivery de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).


## Criação de fragmentos de conteúdo {#creating-content-fragments}

### Criando um Modelo de Conteúdo {#creating-a-content-model}

[A ](/help/assets/content-fragments/content-fragments-models.md) modelagem de fragmentos de conteúdo deve ser ativada e criada antes da criação de fragmentos de conteúdo com conteúdo estruturado.

### Criação de um fragmento de conteúdo {#creating-a-content-fragment}

O método de criação de um fragmento de conteúdo é:

1. Navegue até a pasta **Ativos** na qual deseja criar o fragmento.
2. Selecione **Criar** e **Fragmento de conteúdo** para abrir o assistente.
3. A primeira etapa do assistente requer que você especifique a base do novo fragmento.

   * [Modelo](/help/assets/content-fragments/content-fragments-models.md)  - usado para criar um fragmento que requer conteúdo estruturado; por exemplo, o  **** Adventremodel

      * Todos os modelos disponíveis são exibidos.

   Após a seleção, use **Próximo** para continuar.

   ![base do fragmento](assets/cfm-managing-01.png)

4. Na etapa **Propriedades**, especifique:

   * **Básico**

      * **Título**

         O título do fragmento.

         Obrigatório.

      * **Descrição**

      * **Tags**
   * **Avançado**

      * **Nome**

         O nome; será usada para formar o URL.

         Obrigatório; serão derivadas automaticamente do título, mas poderão ser atualizadas.


5. Selecione **Criar** para concluir a ação e, em seguida, **Abra** o fragmento para editar ou retorne ao console com **Concluído**.

## Ações para um fragmento de conteúdo {#actions-for-a-content-fragment}

No console **Assets**, várias ações estão disponíveis para seus fragmentos de conteúdo:

* Na barra de ferramentas; após a seleção do fragmento, todas as ações apropriadas estarão disponíveis.
* Como [ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions); um subconjunto de ações disponível para os cartões de fragmento individuais.

![ações](assets/cfm-managing-02.png)

Selecione o fragmento para revelar a barra de ferramentas com as ações aplicáveis:

* **Processar ativos novamente**
* **Criar**
* **Download**

   * Salve o fragmento como um arquivo ZIP; você pode definir se deseja incluir Elementos, Variações, Metadados.

* **Check-out**
* **Propriedades**

   * Permite que você visualização e/ou edite os metadados do fragmento.

* **Editar**

   * Permite [abrir o fragmento para editar conteúdo](/help/assets/content-fragments/content-fragments-variations.md) juntamente com seus elementos, variações, conteúdo associado e metadados.

* **Publicação rápida**
* **Gerenciar publicação**
* **Gerenciar tags**
* **Para a coleção**
* **Copiar** (e  **colar**)
* **Mover**
* **Excluir**

>[!NOTE]
>
>Muitas dessas ações são [ações padrão para Assets](/help/assets/manage-digital-assets.md) e/ou [AEM aplicativo de desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html).

## Abrir o Editor de fragmentos {#opening-the-fragment-editor}

Para abrir o fragmento para edição:

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa [das permissões apropriadas](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Entre em contato com o administrador do sistema se tiver problemas.

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa das permissões apropriadas. Entre em contato com o administrador do sistema se tiver problemas.

1. Use o console **Assets** para navegar até o local do fragmento do conteúdo.
2. Abra o fragmento para edição ao:

   * Clicar/tocar no fragmento ou link do fragmento (isso depende da visualização do console).
   * Selecionando o fragmento, em seguida, **Editar** na barra de ferramentas.

   O editor de fragmentos abrirá:

   ![editor de fragmentos](assets/cfm-managing-03.png)

   >[!NOTE]
   >
   >1. Uma mensagem será exibida quando o fragmento já estiver referenciado em uma página de conteúdo.
   >2. O painel lateral pode ser oculto/exibido usando o ícone **Alternar painel lateral**.


3. Navegue pelos três modos usando os ícones no painel lateral:

   * Variações: [Editar o conteúdo](#editing-the-content-of-your-fragment) e [Gerenciar suas variações](#creating-and-managing-variations-within-your-fragment)

   * [Anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
   * [Conteúdo associado](#associating-content-with-your-fragment)
   * [Metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)
   * [Árvore de estrutura](/help/assets/content-fragments/content-fragments-structure-tree.md)
   * [Visualizar](/help/assets/content-fragments/content-fragments-json-preview.md)

   ![modos](assets/cfm-managing-04.png)

4. Depois de fazer as alterações, use **Save** ou **Cancel** conforme necessário.

   >[!NOTE]
   >
   >Tanto **Salvar** quanto **Cancelar** sairão do editor - consulte [Salvar, cancelar e versões](#save-cancel-and-versions) para obter informações completas sobre como ambas as opções operam para fragmentos de conteúdo.

## Salvar, Cancelar e Versões {#save-cancel-and-versions}

>[!NOTE]
>
>As versões também podem ser [criadas, comparadas e revertidas da Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

O editor tem duas opções:

* **Salvar**

   Salva as alterações mais recentes e saia do editor.

   >[!CAUTION]
   >
   >Para editar um fragmento de conteúdo, você precisa [das permissões apropriadas](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Entre em contato com o administrador do sistema se tiver problemas.

   >[!NOTE]
   >
   >É possível permanecer no editor, fazendo uma série de alterações, antes de selecionar **Salvar**.

   >[!CAUTION]
   >
   >Além de simplesmente salvar suas alterações, **Salvar** também atualiza quaisquer referências e garante que o dispatcher seja liberado conforme necessário. Essas mudanças podem levar tempo para serem processadas. Devido a isso, pode haver um impacto no desempenho em um sistema grande/complexo/com carga intensa.
   >
   >
   >Lembre-se disso ao usar **Salvar** e, em seguida, reinserir rapidamente o editor de fragmentos para fazer e salvar outras alterações.

* **Cancelar**

   Sairá do editor sem salvar as alterações mais recentes.

Durante a edição do fragmento do conteúdo, AEM cria automaticamente versões para garantir que o conteúdo anterior possa ser restaurado se você **Cancelar** suas alterações:

1. Quando um fragmento de conteúdo é aberto para edição AEM verifica a existência do token baseado em cookies que indica se existe uma *sessão de edição*:

   1. Se o token for encontrado, o fragmento será considerado parte da sessão de edição existente.
   2. Se o token *não* estiver disponível e o usuário start a edição de conteúdo, uma versão será criada e um token para esta nova sessão de edição será enviado para o cliente, onde será salvo em um cookie.

2. Embora haja uma sessão de edição *ativa*, o conteúdo que está sendo editado é salvo automaticamente a cada 600 segundos (padrão).

   >[!NOTE]
   >
   >O intervalo de salvamento automático é configurável usando o mecanismo `/conf`.
   >
   >Valor padrão, consulte:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se o usuário selecionar **Cancelar** a edição, a versão criada no start da sessão de edição será restaurada e o token será removido para encerrar a sessão de edição.
4. Se o usuário selecionar **Salvar** para as edições, os elementos/variações atualizados serão mantidos e o token será removido para encerrar a sessão de edição.

## Editar o conteúdo do fragmento {#editing-the-content-of-your-fragment}

Depois de abrir o fragmento, use a guia [Variações](/help/assets/content-fragments/content-fragments-variations.md) para criar o conteúdo.

## Criação e gerenciamento de variações no seu fragmento {#creating-and-managing-variations-within-your-fragment}

Depois de criar o conteúdo Principal, você pode criar e gerenciar [Variações](/help/assets/content-fragments/content-fragments-variations.md) desse conteúdo.

## Associar conteúdo ao fragmento {#associating-content-with-your-fragment}

Você também pode [associar conteúdo](/help/assets/content-fragments/content-fragments-assoc-content.md) a um fragmento. Isso fornece uma conexão para que os ativos (ou seja, imagens) possam ser usados (opcionalmente) com o fragmento quando ele for adicionado a uma página de conteúdo.

## Visualização e edição dos metadados (Propriedades) do fragmento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

É possível visualização e editar as propriedades de um fragmento usando a guia [Metadados](/help/assets/content-fragments/content-fragments-metadata.md).

## Linha do tempo para fragmentos de conteúdo {#timeline-for-content-fragments}

Além das opções padrão, [Linha do tempo](/help/assets/manage-digital-assets.md#timeline) fornece informações e ações específicas para fragmentos de conteúdo:

* Informações de visualização sobre versões, comentários e anotações
* Ações para versões

   * **[Reverter para esta versão](#reverting-to-a-version)**  (selecione um fragmento existente e, em seguida, uma versão específica)

   * **[Comparar com Atual](#comparing-fragment-versions)**  (selecione um fragmento existente e, em seguida, uma versão específica)

   * Adicionar um **Rótulo** e/ou **Comentário** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **Salvar como versão**  (selecione um fragmento existente e, em seguida, a seta para cima na parte inferior da Linha do tempo)

* Ações para anotações

   * **Excluir**

>[!NOTE]
Os comentários são:
* Funcionalidade padrão para todos os ativos
* Feito na Linha do tempo
* Relacionado ao ativo de fragmento

As anotações (para Fragmentos de conteúdo) são:
* Inserido no editor de fragmentos
* Específico para um segmento selecionado de texto dentro do fragmento



Por exemplo:

![linha do tempo](assets/cfm-managing-05.png)

## Comparação de versões de fragmento {#comparing-fragment-versions}

A ação **Comparar com Atual** está disponível na [Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) depois de selecionar uma versão específica.

Isso abrirá:

* a versão **Atual** (mais recente) (esquerda)

* a versão selecionada **v&lt;*x.y*>** (direita)

Elas serão mostradas lado a lado, onde:

* Quaisquer diferenças são destacadas

   * Texto excluído - vermelho
   * Texto inserido - verde
   * Texto substituído - azul

* O ícone de tela cheia permite que você abra qualquer versão por conta própria; em seguida, alterne de volta para a visualização paralela
* Você pode **Reverter** para a versão específica
* **O** Dono retornará ao console

>[!NOTE]
Não é possível editar o conteúdo do fragmento ao comparar fragmentos.

![comparação](assets/cfm-managing-06.png)

## Reverter para uma versão {#reverting-to-a-version}

É possível reverter para uma versão específica do fragmento:

* Diretamente da [Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Selecione a versão necessária e a ação **Reverter para esta versão**.

* Enquanto [compara uma versão à versão atual](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) você pode **Reverter** para a versão selecionada.

## Publicar e fazer referência a um fragmento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
Se o fragmento for baseado em um modelo, verifique se o modelo [foi publicado](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
Se você publicar um fragmento de conteúdo para o qual o modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado com o fragmento.

Fragmentos de conteúdo devem ser publicados para uso no ambiente de publicação. Podem ser publicados:

* Após a criação; no console **Assets**.
* Quando você [publica uma página que usa o fragmento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing); o fragmento será listado nas referências de página.

>[!CAUTION]
Depois que um fragmento é publicado e/ou referenciado, AEM exibirá um aviso quando um autor abrir o fragmento para edição novamente. Isso serve para avisar que as alterações no fragmento também afetarão as páginas referenciadas.

## Excluindo um fragmento {#deleting-a-fragment}

Para excluir um fragmento:

1. No console **Assets**, navegue até o local do fragmento de conteúdo.
2. Selecione o fragmento.

   >[!NOTE]
   A ação **Delete** não está disponível como uma ação rápida.

3. Selecione **Excluir** na barra de ferramentas.
4. Confirme a ação **Delete**.

   >[!CAUTION]
   Se o fragmento já estiver referenciado em uma página, você verá uma mensagem de aviso e será solicitado a confirmar se deseja continuar com uma **Exclusão forçada**. O fragmento, junto com seu componente do fragmento de conteúdo, será excluído de qualquer página de conteúdo.
