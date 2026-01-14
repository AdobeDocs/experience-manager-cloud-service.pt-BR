---
title: Notas de versão do Adobe Experience Manager as a Cloud Service 2020.6.0
description: Notas de versão do as a Cloud Service [!DNL Adobe Experience Manager] para 2020.6.0.
exl-id: fd6ebe2b-6d98-498c-a45d-b9a9c34e6be7
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 91%

---

# Notas da versão para AEM as a Cloud Service 2020.6.0 {#release-notes}

Esta página descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.6.0.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Experience Manager] as a Cloud Service 2020.6.0 é 4 de junho de 2020.

## Novidades do AEM Sites {#aem-sites}

Consulte esta seção para saber mais sobre as novidades e atualizações do AEM Sites no AEM as a Cloud Service, versão 2020.6.0.

### Novidades {#whats-new-2020.6.0}

A versão 2.9.0 dos [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) agora está disponível como parte do AEM Sites, incluindo:

* Integração entre a [Camada de dados do cliente Adobe](https://github.com/adobe/adobe-client-data-layer) e os Componentes principais
* Atributos de ID HTML configuráveis para todos os componentes
* Um novo componente da Barra de progresso
* Muitas correções de erros

### Correções de erros {#sites-bug-fixes}

* Os componentes dentro do container de layout não ficam visíveis quando o container de layout é copiado e colado novamente em uma página.

* Corrigido um problema com o redimensionamento do componente de layout.

* Foi adicionada a capacidade de gerenciar o roteamento de páginas exclusivas do Angular e de páginas do AEM/Angular.

### Acessibilidade {#accessibility}

* A narrativa de funções e estados agora são possíveis para os itens de Alvenaria na caixa de diálogo **Criar página** ao navegar no modo de navegação usando a seta para baixo.

* Foi adicionado um link na navegação para permitir que os usuários pulem para o conteúdo principal.

* Melhorias em leitores de tela.

## Novidades nos componentes de base do AEM as a Cloud Service {#foundations}

Os tempos de compilação de um projeto do AEM melhorarão com a remoção de todas as referências ao repositório remoto `https://downloads.experiencecloud.adobe.com/content/maven/public` no pom.xml do projeto AEM.

O Jar da API SDK do AEM as a Cloud Service, que anteriormente estava hospedado nesse local, agora está localizado no Maven Central, que é o repositório de artefatos padrão do Maven.

## Novidades do Cloud Manager {#cloud-manager}

Consulte esta seção para saber mais sobre as novidades e atualizações do Cloud Manager no AEM as a Cloud Service, versão 2020.6.0.

### Novidades {#what-is-new-cloud-manager}

* Os usuários com a função de *Proprietário da empresa* no Cloud Manager agora podem excluir um Programa de sandbox a partir da página de destino (com o botão de ação rápida no cartão Programa) ou dentro do programa.

  Consulte [Exclusão de um programa de sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html?lang=pt-BR) para obter mais detalhes.

* Os usuários de programas de sandbox com a função de *Proprietário da empresa* ou *Gerente de implantação* no Cloud Manager agora podem excluir seu conjunto de ambientes de produção e preparo na interface do Cloud Manager. A opção de exclusão agora está disponível no cartão Ambiente da página **Visão geral de programas**, bem como na página **Ambientes**. Selecionar a opção de exclusão no ambiente de produção também exclui o ambiente de preparo no mesmo conjunto, e vice-versa.

  Consulte [Exclusão de um programa de sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html?lang=pt-BR) para obter mais detalhes.

* Há notas explicativas na página de destino para informar e instruir o usuário sobre a navegação básica.

* Há notas explicativas na página **Visão geral de programas** para informar e instruir o usuário sobre a navegação básica dentro do Cloud Manager.

* Agora há uma página **Saiba mais** na área de navegação superior do Cloud Manager. Essa página inclui recursos para ajudar os usuários a saber mais sobre os fluxos de trabalho usados com mais frequência, conforme a relevância para as suas funções atribuídas no Cloud Manager.

* Os Programas de sandbox agora são identificados por meio de um selo **Sandbox**, que é exibido no cartão do programa na página de destino e também ao lado do nome do programa na página **Visão geral de programas**.

* Os usuários que estiverem exercendo a função SysAdmin agora têm acesso com um só clique ao local do Admin Console onde podem gerenciar funções ou permissões de usuários para o Cloud Manager. Agora há um botão **Gerenciar acesso** na página de destino, ao lado do botão **Adicionar programa**.

  Consulte [Tarefas do administrador do sistema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=pt-BR#sysadmin-tasks) para obter mais detalhes.

* Agora os usuários com a função administrador do sistema têm acesso à instância de criação diretamente do Cloud Manager com apenas um clique.

  Consulte [Gerenciamento do acesso à instância de criação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=pt-BR#manage-access-aem) para saber mais.

* O log da etapa Criar agora inclui a lista de artefatos descobertos, incluindo pacotes de conteúdo ignorados.

* A etapa Criar agora verifica se todos os pacotes de conteúdo gerados incluem todas as propriedades obrigatórias: nome, grupo e versão.

* A etapa Criar agora verifica se a criação produziu pelo menos um pacote de conteúdo.

### Correções de erros {#bug-fixes-cm}

* Em determinadas situações, os ícones na caixa de diálogo **Criar programa** estavam desalinhados.

* O identificador de versão do AEM não era exibido de maneira consistente na página **Visão geral de programas**.

* Ao configurar o pipeline de produção, a opção **Implantação agendada** não estava visível para alguns clientes.

### Problemas conhecidos {#known-issues-cm}

* Os ambientes do programa de sandbox hibernam quando não é detectada nenhuma atividade por um determinado período. Isso não ocorre no Cloud Manager, mas pode ocorrer por meio do Console do desenvolvedor. O problema será resolvido em uma versão futura.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibe a opção de cancelar hibernação/hibernar o ambiente de um Programa de sandbox. Para resolver isso, uma vez no Console do desenvolvedor, adicione o padrão `#release-cm-p1234-e5678` ao final do URL, em que *1234* é a ID do programa e *5678* é a ID do ambiente. O problema será resolvido em uma versão futura.

## Novidades do [!DNL Adobe Experience Manager Assets] {#aem-assets}

**Experiência do usuário guiada para tags inteligentes aprimoradas, viabilizada pela IA do Adobe**

As tags inteligentes aprimoradas permitem que as organizações treinem modelos de tags inteligentes para reconhecer imagens com base em tags comerciais específicas de clientes, além de tags inteligentes genéricas.

Esta versão oferece uma experiência do usuário nova e guiada que ajuda a configurar o treinamento de tags inteligentes para conjuntos de tags específicos do cliente e treiná-las com ativos que devem ser reconhecidos e marcados no futuro. Agora, a experiência está mais intuitiva.
Treine as tags inteligentes aprimoradas para uma experiência mais intuitiva. Consulte [como adicionar tags inteligentes a ativos](/help/assets/smart-tags.md).

**Suporte para ingestão, pré-visualização e entrega de conteúdo 3D**

Agora, as organizações podem armazenar e usar arquivos 3D no AEM Assets. O usuário pode fazer upload, pré-visualizar e usar vários arquivos principais em 3D, incluindo arquivos OBJ, STL, GLTF e GLB. Com a adição do [!DNL Dynamic Media], você pode configurar e entregar experiências em 3D usando URLs ou visualizadores agnósticos. Isso inclui um visualizador 3D do [!DNL Dynamic Media], um componente de visualizador 3D do Sites e a capacidade de fornecer arquivos 3D pelo [!DNL Dynamic Media] (RA/RV). Consulte [Trabalho com ativos 3D no Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Suporte do Adobe Asset Link para o Adobe XD**

Com a versão mais recente, o [!DNL Experience Manager Assets] oferece suporte para um novo plug-in do [!DNL Adobe Asset Link], lançado com o [!DNL Adobe XD] v29.3. A integração permite que os designers acessem e usem ativos do [!DNL Experience Manager] em seus projetos, sem a necessidade de deixar o [!DNL Adobe XD]. Consulte a [documentação do Adobe Asset Link para o Adobe XD](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html).

Com esse lançamento, usuários criativos e designers agora podem trabalhar com ativos gerenciados no [!DNL AEM Assets], usando o [!DNL Adobe Asset Link] em diversos aplicativos para desktop da Creative Cloud, incluindo [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator] e [!DNL InDesign].

**Aprimoramentos de acessibilidade**

Agora, o [!DNL Adobe Experience Manager Assets] está mais acessível, em conformidade com as diretrizes da Web Content Accessibility Guidelines (WCAG) v2.1. A acessibilidade melhorou nos seguintes casos de uso ou interfaces:

Os elementos da interface do usuário são amigáveis para leitores de tela, são acessíveis por teclado e têm melhor contraste. Veja a seguir uma lista detalhada das melhorias:

* As barras de progresso [!UICONTROL Opções], [!UICONTROL Escopo] e [!UICONTROL Fluxos de trabalho] na página [!UICONTROL Gerenciar publicação] não são lidas pelo leitor de tela como barras de progresso. Em vez disso, os usuários de leitores de tela percebem esses indicadores de status como uma lista de guias. (CQ-4273015)

* Ao adicionar tags na página [!UICONTROL Propriedades] de um ativo, os usuários navegam por uma estrutura em árvore de tags. A estrutura em árvore não é acessível, pois os usuários de leitores de tela não ouvem nada ao navegarem por ela. (CQ-4272964)

* Na caixa de diálogo de compartilhamento de links, no modo de navegação, o leitor de tela:

   * Narra as informações da tabela imediatamente quando a caixa de diálogo é carregada.
   * Não consegue acessar todas as sugestões automáticas listadas.
   * Não narra as sugestões automáticas exibidas para a caixa de combinação [!UICONTROL Adicionar endereço de email/Pesquisar]. (CQ-4294232)

* A página [!UICONTROL Editor de esquema de metadados] e seus elementos agora são acessíveis com o teclado e podem ser usados facilmente com leitores de tela. (CQ-4272953) Os usuários podem arrastar os componentes usando o teclado no modo de navegação NVDA. (CQ-4296326)

* Na interface do Assets, as configurações de visualização não podem ser acessadas pelo teclado. (CQ-4289038)

* A taxa de luminosidade é menor que 3:1 para os ícones de classificação de cor amarela. Isso não é útil para usuários com visão limitada e sem percepção de cor. As estrelas de classificação são exibidas na guia no modo de visualização de ativos ou cartões

* A cor e o contraste de alguns elementos da interface do usuário são atualizados para que os usuários com visão limitada ou usuários sem percepção de cor possam distinguir esses elementos da interface do usuário. Por exemplo, a cor dos ícones de classificação de estrelas na seção [!UICONTROL Classificação] da guia [!UICONTROL Avançado], em [!UICONTROL Propriedades] de um ativo e em uma visualização de cartão é alterada para obter o contraste apropriado. (CQ-4295106)

* Agora, os leitores de tela podem ler as entradas do menu pop-up de caixas de listagem da caixa de combinação (em vários campos em páginas diferentes) como lista de opções. (CQ-4294017)

* Para aplicar um fluxo de trabalho a um ativo, a seta de divisa na [!UICONTROL Linha do tempo] pode ser acessada pelo teclado. (CQ-4289268)

* Os usuários podem remover tags selecionadas no campo [!UICONTROL Tags] da guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] de um ativo usando o símbolo `x`. Agora, os leitores de tela anunciam a finalidade e o número de tags selecionadas (CQ-4273033).

* Os campos de formulário somente leitura podem ser focalizados com teclado. Um exemplo são os campos desativados na guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] de um ativo. (CQ-4273031)

* Agora é possível acessar as opções para filtrar ativos na barra lateral esquerda usando um teclado. (CQ-4273018)

* O leitor de tela anuncia a finalidade de vários elementos de caixa de combinação, como o campo Caminho e a opção de abrir a caixa de diálogo Seleção na guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] de um ativo. (CQ-4273016)

* Os controles de volume para vídeos são acessíveis através do teclado. (CQ-4272696)

* Muitas opções acionáveis na interface do Assets não indicam o foco quando se usa o teclado. (CQ-4272694)

* Agora, os usuários de leitores de tela sabem quando as linhas em uma exibição em lista são selecionáveis através de um teclado. As informações são anunciadas quando o ponteiro é posicionado sobre as linhas. (CQ-4271824)

* Alguns campos de formulário, como o nome de usuário e os campos de senha na página de logon, dependem dos valores de espaço reservado para fornecer um rótulo acessível. (CQ-4271716)

* Alguns elementos interativos da interface do usuário, como links, e algumas opções, como opções de cabeçalho e zoom de página de ativos ou navegação de pastas, agora podem ser acessados com teclado. (CQ-4271412)

* Os títulos de todas as páginas do [!DNL Adobe Experience Manager] Assets agora são exclusivos. (CQ-4271409)

**Outras melhorias**

A versão oferece as seguintes melhorias adicionais:

* Capacidade de reprocessar ativos com perfis de processamento de ativos, dando aos usuários controle total sobre o processo (basta executar o processamento completo de ativos, aplicar perfis de processamento específicos e decidir se o fluxo de trabalho de pós-processamento deve ser executado).
* Agora, as consultas de pesquisa dão resultados com mais rapidez quando a instância de cluster subjacente é reiniciada nos bastidores (antes, a execução de pesquisa inicial podia durar mais tempo nesse caso).
* Classifique por &quot;Nome&quot; ao visualizar ativos na exibição em lista da interface do Assets e em resultados de pesquisa. Consulte [pesquisar ativos](/help/assets/search-assets.md#sort).
* Classifique por &quot;Criado&quot; (Data) ao visualizar ativos na exibição em lista da interface do Assets e nos resultados da pesquisa. Consulte [pesquisar ativos](/help/assets/search-assets.md#sort).
* Suporte para converter arquivos EPS em imagens usando microsserviços de ativos.

### Correções de erros {#assets-bug-fixes}

Além dos novos recursos acima, a versão atual fornece as seguintes correções de erros com base no feedback de clientes para o [!DNL Assets].

* Para arquivos de música MP3, o botão Reproduzir exibido na miniatura na pré-visualização do DAM não funciona. (CQ-4294731)
* Passar o ponteiro sobre a exibição de cartão faz com que a tela role como resultado do foco (automático) nas ações rápidas disponíveis no cartão. (GRANITE-26895)
* A exibição de muitas imagens após a rolagem de vários resultados de pesquisa causa falha do navegador. (GRANITE-26432)
* Ao baixar um ativo, se a opção de email estiver selecionada e mesmo se uma ID de email válida for fornecida, a opção de download não fica disponível. (CQ-4296535)
* Filtros personalizados salvos como coleções inteligentes não são aplicados corretamente a ativos. (CQ-4294942)
* Várias melhorias de pesquisa e indexação e correções de erros para melhorar o desempenho. (CQ-4286373)
* A guia de propriedades da pasta não pode ser acessada no Assets e retorna um erro 500. (CQ-4295701)
