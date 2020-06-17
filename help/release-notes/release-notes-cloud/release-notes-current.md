---
title: Notas de versão do Adobe Experience Manager as a Cloud Service para 2020.6.0
description: Notas de versão do Experience Manager para 2020.6.0
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 7%

---


# Notas de versão para AEM as a Cloud Service 2020.6.0{#release-notes}

A seção a seguir descreve as Notas de versão gerais para Experience Manager as a Cloud Service 2020.6.0.

## Data de lançamento {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.6.0 is June 04, 2020.

## Novidades no AEM Sites {#aem-sites}

Siga esta seção para saber mais sobre as novidades e atualizações do AEM Sites no AEM as a Cloud Service versão 2020.6.0.

### Novidades {#whats-new-2020.6.0}

A versão 2.9.0 dos Componentes [](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/introduction.html) principais agora está disponível como parte dos AEM Sites, incluindo:

* Integração entre a camada [de dados do cliente](https://github.com/adobe/adobe-client-data-layer) Adobe e os componentes principais
* Atributos de ID HTML configuráveis para todos os componentes
* Um novo componente de barra de progresso
* Muitas correções de erros

### Correções de erros {#sites-bug-fixes}

* Os componentes dentro do container de layout não ficam visíveis quando o container Layout é copiado e colado novamente em uma página.

* Corrigido o problema com o redimensionamento do componente de layout.

* Foi adicionada a capacidade de gerenciar somente páginas Angular de roteamentos e páginas AEM/Angular.

### Acessibilidade {#accessibility}

* A função e o estado de narração agora são possíveis para os itens de alvenaria na caixa de diálogo **Criar página** ao navegar no modo de navegação usando a seta para baixo.

* Foi adicionado um link na navegação para permitir que os usuários pulem para o conteúdo principal.

* Melhorias no leitor de tela.

## Novidades do AEM como Cloud Service {#foundations}

Os tempos de criação do projeto AEM melhorarão com a remoção de todas as referências no pom.xml do projeto AEM para o repositório remoto `https://downloads.experiencecloud.adobe.com/content/maven/public`.

O AEM como um Cloud Service SDK API Jar, que anteriormente estava hospedado nesse local, agora está localizado no Maven Central, que é o repositório de artefatos padrão do Maven.

## Novidades do Cloud Manager {#cloud-manager}

Siga esta seção para saber mais sobre as novidades e atualizações do Cloud Manager no AEM as a Cloud Service versão 2020.6.0.

### Novidades {#what-is-new-cloud-manager}

* Um usuário na função Proprietário *da* empresa no Cloud Manager agora pode excluir um Programa da caixa de proteção da landing page (por meio do botão de ação rápida no cartão de Programa) ou de dentro do programa.

   Consulte [Excluindo um Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) Sandbox para obter mais detalhes.

* Um usuário do Programa Sandbox no Proprietário *do* Negócio ou na função *Gerenciador* de Implantação no Gerenciador de Nuvem agora pode excluir seu conjunto de ambientes de Produção e Estágio por meio da interface do usuário do Gerenciador de Nuvem. A opção de exclusão agora está disponível no cartão de Ambiente na página Visão geral **dos** Programas, bem como na página **Ambientes** . Selecionar a opção de exclusão em Produção ou Estágio também exclui a outra no conjunto.

   Consulte [Excluindo um Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) Sandbox para obter mais detalhes.

* O treinador marca na landing page para informar e instruir o usuário sobre a navegação básica.

* O treinador marca a página Visão geral **do** Programa para informar e instruir o usuário sobre a navegação básica dentro do Cloud Manager para que ele seja iniciado.

* Uma página **APRENDIZADO** está disponível no Cloud Manager, acessível por meio da navegação superior. Esta página inclui recursos para ajudar os usuários a saber mais sobre os fluxos de trabalho usados com mais frequência, conforme relevante para suas funções atribuídas no Cloud Manager.

* Os Programas Sandbox agora são identificados por meio de um emblema **Sandbox** que será exibido no cartão do programa na landing page, bem como ao lado do nome do programa na página Visão geral **do** Programa.

* Um usuário na função SysAdmin agora tem acesso de um clique ao local no Admin Console de onde as funções ou permissões do usuário para o Cloud Manager podem ser gerenciadas. Um botão **Gerenciar acesso** agora está disponível na landing page ao lado do botão **Adicionar Programa** .

   Consulte [SysAdmin Tarefa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) para obter mais detalhes.

* Um usuário na função SysAdmin agora tem acesso de um clique à instância do autor diretamente do Gerenciador de nuvem.

   Consulte [Gerenciamento de acesso à instância](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) do autor para obter mais detalhes.

* O log de compilação agora inclui a lista de artefatos descobertos, incluindo pacotes de conteúdo ignorados.

* A etapa Criar agora valida que todos os pacotes de conteúdo gerados incluem todas as propriedades obrigatórias - nome, grupo e versão.

* A etapa de compilação agora valida que a compilação produziu pelo menos um pacote de conteúdo.

### Correções de erros {#bug-fixes-cm}

* Em determinadas situações, os ícones na caixa de diálogo **Criar Programa** estavam desalinhados.

* O identificador de versão do AEM não era exibido consistentemente na página Visão geral **dos** Programas.

* Ao configurar o pipeline de produção, a opção Implantação **** agendada não estava visível para alguns clientes.

### Problemas conhecidos {#known-issues-cm}

* Ambientes em um programa Sandbox serão hibernados quando nenhuma atividade for detectada por um determinado período. Esse status não será observado no Cloud Manager. No entanto, o status pode ser observado pelo Console do desenvolvedor. Isso será abordado em uma versão futura.

* O link para o Console do desenvolvedor diretamente do Gerenciador de nuvem não exibirá a opção de cancelar a hibernação/hibernar um ambiente do Programa do Sandbox. Para resolver isso, uma vez no Console do desenvolvedor, adicione o padrão `#release-cm-p1234-e5678` ao final do url, onde *1234* é a ID do Programa e *5678* é a ID do Ambiente. Isso será abordado em uma versão futura.

## Novidades da versão [!DNL Adobe Experience Manager Assets] {#aem-assets}

**Experiência do usuário guiada para Tags inteligentes aprimoradas, capacitada pelo Adobe Sensei**

As Tags inteligentes aprimoradas permitem que as organizações treinem modelos de marcação inteligentes para reconhecer imagens com base em tags comerciais específicas do cliente, além de tags inteligentes genéricas.

Com esta versão, há uma nova experiência guiada do usuário que ajuda a configurar o treinamento de tags inteligentes para conjuntos de tags específicas do cliente e treiná-las com ativos, que devem ser reconhecidos e marcados com eles no futuro. Esta é uma experiência mais intuitiva.
Treinar Tags inteligentes aprimoradas para obter mais um treinamento intuitivo para Tags inteligentes. Consulte [como adicionar tags inteligentes a ativos](/help/assets/smart-tags.md) e [configurar tags](/help/assets/smart-tags-configuration.md)inteligentes.

**Suporte para ingestão, pré-visualização e delivery de conteúdo 3D**

As organizações agora podem armazenar e usar arquivos 3D em AEM Assets. O usuário pode carregar, pré-visualização e aproveitar uma variedade de arquivos 3D principais, incluindo arquivos .obj, .stl, .gltf e .glb. Com a adição de [!DNL Dynamic Media], as experiências 3D podem ser configuradas e entregues por URLs agnósticos ou visualizadores. Isso inclui um Visualizador de experiência [!DNL Dynamic Media] 3D, o componente Visualizador 3D do Sites e a capacidade de fornecer arquivos 3D via [!DNL Dynamic Media] (AR/VR). Consulte [Trabalhar com ativos 3D no Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Suporte do Adobe Asset Link para Adobe XD**

Com a versão mais recente, [!DNL Experience Manager Assets] fornece suporte para um novo [!DNL Adobe Asset Link] plug-in lançado com a [!DNL Adobe XD] v29.3. A integração permite que os designers acessem e usem ativos de [!DNL Experience Manager] seus projetos, sem a necessidade de deixar o [!DNL Adobe XD] aplicativo. Consulte [Adobe Asset Link para a documentação](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html)do Adobe XD.

Com esta versão, os usuários e designers criativos agora podem trabalhar com ativos gerenciados no [!DNL AEM Assets] uso [!DNL Adobe Asset Link] em diversos aplicativos de desktop da Creative Cloud, incluindo [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator]e [!DNL InDesign].

**Aprimoramentos de acessibilidade**

[!DNL Adobe Experience Manager Assets] agora está mais acessível em conformidade com as diretrizes de acessibilidade de conteúdo da Web (WCAG) v2.1. A acessibilidade melhorou nos seguintes casos de uso ou interfaces:

Os elementos da interface do usuário são amigáveis ao leitor de tela, são acessíveis usando um teclado e têm melhor contraste. Veja a seguir uma lista detalhada de melhorias:

* Os indicadores de progresso [!UICONTROL Opções], [!UICONTROL Escopo]e [!UICONTROL Workflows] na página [!UICONTROL Gerenciar publicação] não são lidos pelo leitor de tela como indicadores de progresso. Em vez disso, os usuários de leitores de tela percebem esses indicadores de status como uma lista de guia. (CQ-4273015)

* Ao adicionar tags na página [!UICONTROL Propriedades] de um ativo, os usuários navegam por uma estrutura em árvore de tags. A estrutura em árvore não é acessível, pois os usuários do leitor de tela não ouvem nada ao navegarem por ela. (CQ-4272964)

* Na caixa de diálogo de compartilhamento de links, ao navegar no modo de navegação, o leitor de tela,

   * narra as informações da tabela assim que a caixa de diálogo é carregada.
   * não é possível navegar para todas as sugestões automáticas listadas.
   * não narra as sugestões automáticas exibidas para a caixa de combinação [!UICONTROL Adicionar endereço de email/Pesquisar] . (CQ-4294232)

* A página Editor [!UICONTROL de Schemas de] Metadados e seus elementos agora são acessíveis e amigáveis para o leitor de tela. As opções podem ser usadas usando um teclado. (CQ-4272953) Os usuários podem arrastar os componentes usando o teclado no modo de navegação NVDA. (CQ-4296326)

* Na interface do usuário do Assets, as configurações de visualização não podem ser acessadas pelo teclado. (CQ-4289038)

* A relação de luminosidade é inferior a 3:1 para os ícones de notação de cor amarela. Não é útil para usuários com visão limitada e sem percepção de cor. As estrelas de avaliação são exibidas na guia no ativo ou na visualização do cartão

* A cor e o contraste de alguns elementos da interface do usuário são atualizados para que os usuários com visão limitada ou usuários sem percepção de cor possam distinguir esses elementos da interface do usuário. Por exemplo, a cor dos ícones de classificação de estrelas na seção [!UICONTROL Classificação] da guia [!UICONTROL Avançado] em [!UICONTROL Propriedades] de um ativo e em visualização de cartão é alterada para contraste apropriado. (CQ-4295106)

* O menu pop-up Caixa de lista da caixa de combinação (em vários campos em páginas diferentes) agora exibe as entradas como uma lista de opções que podem ser anunciadas pelos leitores de tela. (CQ-4294017)

* Para aplicar um fluxo de trabalho a um ativo, a seta de divisas na [!UICONTROL Linha do tempo] pode ser acessada usando um teclado. (CQ-4289268)

* Os usuários podem remover tags selecionadas no campo [!UICONTROL Tags] na guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] de um ativo usando `x` símbolo. Sua finalidade agora é anunciada pelos leitores de tela, juntamente com o número de tags selecionadas (CQ-4273033).

* Os campos de formulário somente leitura podem ser focalizados no uso de um teclado. Por exemplo, os campos desativados na guia [!UICONTROL Básico] na página [!UICONTROL Propriedades] de um ativo. (CQ-4273031)

* Acesse as opções para filtrar ativos na barra lateral esquerda usando um teclado agora. (CQ-4273018)

* A finalidade de vários elementos da caixa de combinação, como o campo Caminho e a opção de abrir a caixa de diálogo Seleção na guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] de um ativo, agora são anunciados corretamente pelos leitores de tela. (CQ-4273016)

* Os controles de volume para vídeos são acessíveis usando um teclado. (CQ-4272696)

* Muitas opções acionáveis na interface do usuário do Assets não indicam foco ao usar o teclado. (CQ-4272694)

* Os usuários do leitor de tela agora sabem quando as linhas na visualização da lista são selecionáveis usando um teclado. As informações são anunciadas quando o ponteiro é posicionado sobre as linhas. (CQ-4271824)

* Alguns campos de formulário, como o nome de usuário e os campos de senha na página de logon, dependem dos valores de espaço reservado para fornecer um rótulo acessível. (CQ-4271716)

* Elementos interativos da interface do usuário, como links e opções, como opções de cabeçalho e zoom de página de ativos ou navegação de pastas, agora podem ser acessados usando um teclado. (CQ-4271412)

* Os títulos de todas as páginas navegadas em [!DNL Adobe Experience Manager] Ativos agora são exclusivos. (CQ-4271409)

**Outras melhorias**

A versão oferece os seguintes aprimoramentos adicionais:

* Capacidade de reprocessar ativos com perfis de processamento de ativos, dando aos usuários controle total do processo (executar processamento completo de ativos, apenas aplicar perfis de processamento específicos e decidir se o fluxo de trabalho de pós-processamento deve ser executado).
* Os query de pesquisa retornam os resultados mais rapidamente agora quando a instância de cluster subjacente é reiniciada nos bastidores (a execução de pesquisa inicial pode durar mais tempo nesse caso antes).
* Classifique por &quot;Nome&quot; ao exibir ativos na visualização de lista na interface Ativos e nos resultados da pesquisa. Consulte ativos [de](/help/assets/search-assets.md#sort)pesquisa.
* Classificar em &quot;Criado&quot; (Data) ao exibir ativos na visualização de lista na interface do Assets e nos resultados da pesquisa. Consulte ativos [de](/help/assets/search-assets.md#sort)pesquisa.
* Suporte para converter arquivos EPS em imagens usando microserviços de ativos.

### Correções de erros {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

Além dos novos recursos acima, a versão atual fornece as seguintes correções de erros com base no feedback do cliente para [!DNL Assets].

* Para arquivos de música MP3, o botão reproduzir exibido na miniatura na pré-visualização DAM não funciona. (CQ-4294731)
* Passar o ponteiro sobre a visualização do cartão faz com que a tela role como resultado do foco (automático) nas ações rápidas disponíveis no cartão. (GRANITE-26895)
* A exibição de muitas imagens após a rolagem de um grande número de resultados de pesquisa resulta em falha do navegador. (GRANITE-26432)
* Ao baixar um ativo, se a opção de email estiver selecionada e mesmo se uma ID de email válida for fornecida, a opção de download não estará disponível. (CQ-4296535)
* filtros personalizados salvos como coleções inteligentes não são aplicados corretamente a ativos. (CQ-4294942)
* Vários aprimoramentos de pesquisa e indexação e correções de erros para melhorar o desempenho. (CQ-4286373)
