---
title: Práticas recomendadas para integrar com o  [!DNL Adobe Creative Cloud]
description: As práticas recomendadas integram uma implantação do Experience Manager com o Adobe Creative Cloud para simplificar os fluxos de trabalho de transferência de ativos e alcançar a eficiência máxima.
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration, Adobe Asset Link, Desktop App
role: User, Developer, Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3438'
ht-degree: 14%

---

# Práticas recomendadas de integração do Adobe Experience Manager e do Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

O Adobe Experience Manager Assets é uma solução de gerenciamento de ativos digitais (DAM) que pode se integrar ao Adobe Creative Cloud para ajudar os usuários do DAM a trabalhar em conjunto com equipes criativas, simplificando a colaboração no processo de criação de conteúdo.

A Adobe Creative Cloud fornece às equipes criativas um ecossistema de soluções e serviços para ajudá-las a criar ativos digitais. Ele inclui aplicativos móveis e de desktop, serviços em nuvem, como armazenamento com sincronização de desktop ou experiência da Web, e mercados como o Adobe Stock.

Leia para saber quais integrações escolher entre o desktop e o DAM de nível empresarial com base no seu caso de uso e quais são as práticas recomendadas associadas para os fluxos de trabalho de conexão.

>[!NOTE]
>
>O compartilhamento de pastas do Experience Manager para o Creative Cloud agora está obsoleto e não é mais abordado abaixo. A Adobe recomenda recursos mais recentes, como o Adobe Asset Link ou o aplicativo de desktop Experience Manager, para fornecer aos usuários criativos acesso aos ativos gerenciados no Experience Manager.

## A Collaboration precisa de profissionais de criação, profissionais de marketing e usuários do DAM {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superfícies envolvidas |
|---|---|---|
| Simplifique a experiência para profissionais criativos no desktop | Simplifique o acesso ao ativo a partir de um DAM ([!DNL Assets]) para profissionais de criação ou, de modo mais amplo, usuários no desktop que trabalham em aplicativos nativos de criação de ativos. Eles precisam de uma maneira fácil e direta de descobrir, usar (abrir), editar e salvar alterações no Experience Manager e fazer upload de novos arquivos. | Desktop Win ou Mac; aplicativos Creative Cloud |
| Forneça ativos prontos para uso de alta qualidade do [!DNL Adobe Stock] | Os profissionais de marketing ajudam a acelerar o processo de criação de conteúdo, auxiliando na origem e descoberta de ativos. Os profissionais da Creative usam os ativos aprovados diretamente de suas ferramentas criativas. | [!DNL Assets]; [!DNL Adobe Stock] marketplace; campos de metadados |
| Distribuir e compartilhar ativos por organizações | Departamentos internos/filiais locais e parceiros externos, distribuidores e agências usam os ativos aprovados compartilhados pela organização principal. A organização deseja compartilhar com segurança e perfeição os ativos criados para reutilização mais ampla. | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| Gerar automaticamente variações predefinidas de ativos carregados | Processar ativos automaticamente usando a tecnologia exclusiva de manipulação e transformação de mídia do Adobe para ações predefinidas. Crie uma lógica personalizada para definir suas próprias ações usando APIs e microsserviços de ativos. | Interface do usuário do [!DNL Assets] |

## Ofertas da Adobe para atender à necessidade de colaboração {#adobe-offerings-to-support-the-collaboration-need}

| Proposta de valor para os perfis envolvidos | Oferta do Adobe | Superfícies envolvidas |
|---|---|---|
| Os usuários do Creative descobrem ativos de [!DNL Experience Manager], abrem e os usam, editam e carregam alterações no [!DNL Experience Manager] e carregam novos arquivos no [!DNL Experience Manager], sem sair do aplicativo [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign. |
| Usuários empresariais simplificam a abertura e o uso de ativos, a edição e o carregamento de alterações no [!DNL Experience Manager] e o carregamento de novos arquivos no [!DNL Experience Manager] a partir do ambiente de desktop. Eles usam uma integração genérica para abrir qualquer tipo de ativo no aplicativo de desktop nativo, incluindo aqueles que não são da Adobe. | Aplicativo de desktop do [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | aplicativo de desktop do Experience Manager no desktop do Win e Mac |
| Profissionais de marketing e usuários empresariais descobrem, visualizam, licenciam e salvam e gerenciam os ativos da Adobe Stock de dentro da Experience Manager. Os ativos licenciados e salvos fornecem metadados selecionados do Adobe Stock para melhorar o controle. | [Integração do Experience Manager e do Adobe Stock](aem-assets-adobe-stock.md) | Interface Web do [!DNL Experience Manager] |
| Melhore a colaboração entre designers de produtos digitais e profissionais de marketing. Permita que os designers usem os ativos digitais nos modelos de design e wireframe na tela do Adobe XD. | [[!DNL Adobe Asset Link] para [!DNL Adobe XD]](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| Os profissionais de marketing podem criar variações e derivações automaticamente com base nos ativos carregados e nas ações predefinidas criadas usando a personalização. Use essa automação para melhorar a velocidade do conteúdo e reduzir o esforço manual. | [Automação de conteúdo](/help/assets/cc-api-integration.md) | Interface Web do [!DNL Experience Manager Assets] |

Este artigo foca principalmente nos dois primeiros aspectos das necessidades de colaboração. A distribuição e o fornecimento de ativos em escala são brevemente mencionadas como um caso de uso. Para essas necessidades, considere o Adobe Brand Portal ou o Asset Share Commons. Soluções alternativas, como o [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), soluções que podem ser criadas com base nos componentes do [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/), [Link Share](share-assets.md), usando a [Interface do usuário para Web do Experience Manager Assets](/help/assets/manage-digital-assets.md), devem ser revisadas com base em requisitos específicos.

![Conexões do Creative Cloud para Experience Manager: decisão sobre qual recurso usar](assets/creative-connections-aem.png)

Decisão sobre qual recurso usar

### Mapeamento de casos de uso e soluções da Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso de uso | Adobe Asset Link | aplicativo de desktop do Experience Manager | Observações ou métodos alternativos |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Descobrir - procurar pastas | Sim | Interface do usuário da Web do Experience Manager + ações da área de trabalho | Ao navegar pelo compartilhamento de rede, desative as miniaturas para evitar o download de arquivos binários de ativos. |
| Descobrir - acessar coleções | Sim | Interface do usuário da Web do Experience Manager + ações da área de trabalho |  |
| Discover - pesquisar ativos | Sim | Interface do usuário da Web do Experience Manager + ações da área de trabalho |  |
| Usar - abrir ativo | Sim | Sim - para qualquer aplicativo | [Abrir da interface da Web](/help/assets/manage-digital-assets.md#previewing-assets) ou do Localizador |
| Usar - colocar ativo do Experience Manager em um documento | Sim - incorporação | Sim - vinculação ou incorporação | O aplicativo de desktop do Experience Manager dá acesso aos ativos como arquivos no sistema de arquivos local. Esses links nos aplicativos nativos são representados por caminhos locais. |
| Editar - abrir para edição | Sim - Ação de check-out | Sim - Abrir ação (no compartilhamento de rede) | O [Check-out no AAL](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) salva o ativo na conta de armazenamento da creative cloud do usuário (sincronizada pelo aplicativo Creative Cloud) por padrão. |
| Editar - trabalho em andamento fora do Experience Manager | Sim - ativo disponível na conta de armazenamento Creative Cloud do usuário sincronizado com o desktop. | Sim |  |
| Editar - fazer upload de alterações | Sim - [Ação de check-in](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) com comentário opcional | Sim |  |
| Upload - único arquivo | Sim - carrega o documento ativo atual | Sim | [Carregar via interface da Web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Upload - vários arquivos/estruturas de pastas hierárquicas | Não | Sim | [Carregar via interface da Web](/help/assets/manage-digital-assets.md#uploading-assets); ferramenta ou script personalizado |
| Diversos - usuário e logon | O usuário do Creative Cloud conectado ao aplicativo de desktop do Creative Cloud é reconhecido (SSO) | Usuário/logon do Experience Manager | Os usuários de ambas as soluções são contabilizados em relação à cota de usuários da Experience Manager. |
| Diversos - rede e acesso | Requer acesso do desktop do usuário à implantação do Experience Manager pela rede | Requer acesso do desktop do usuário à implantação do Experience Manager pela rede | O Adobe Asset Link não compartilha o ambiente proxy de rede. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Para suportar casos de uso de distribuição de ativos, considere as seguintes opções:

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obter um complemento configurável do Assets para publicar ativos.

* As soluções personalizadas são criadas com base no código [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/).
* [compartilhamento de links](/help/assets/share-assets.md) do Experience Manager para compartilhar ativos sob demanda usando links.
* [Interface Web do Assets](/help/assets/manage-digital-assets.md) com áreas para participantes externos protegidas pela configuração do Controle de Acesso da Experience Manager e com os ajustes necessários de configuração de TI/rede, dando a esses usuários externos acesso ao Experience Manager.

## Principais conceitos e casos de uso {#key-concepts-and-use-cases}

### Glossário de termos comuns {#glossary-of-common-terms}

* **Trabalho em andamento ou trabalho criativo em andamento (WIP)**: uma fase no ciclo de vida do ativo em que um ativo sofre várias alterações e normalmente ainda não está pronto para ser compartilhado com equipes maiores.
* **Ativos prontos para criação**: os ativos que prontos para serem compartilhados com uma equipe maior ou que foram selecionados/aprovados pela equipe criativa para compartilhamento com equipes de marketing ou LOB.

* **Aprovações de ativos**: o processo de aprovação que executa ativos já carregados no DAM, que normalmente inclui aprovações de marca, legais e assim por diante.
* **Ativo final**: um ativo que passou por todas as aprovações/marcações de metadados e está pronto para ser usado pela equipe maior. Esse ativo é armazenado no DAM e disponibilizado a todos os usuários (ou a todos os interessados). Ele pode ser usado em canais de marketing ou por equipes criativas para criar designs.

* **Atualização/alteração de ativos secundários:** uma pequena e rápida mudança em um ativo digital. Geralmente é feito em resposta a uma solicitação de retoque ou edição secundária, revisão de ativos ou aprovação (por exemplo, reposição, alteração do tamanho do texto, ajuste da saturação/brilho, cor e assim em diante).
* **Atualizações/alterações de ativos principais:** uma mudança em um ativo digital que requer trabalho considerável, e às vezes deve ser feita por um período mais longo. Normalmente, inclui várias alterações. O ativo deve ser salvo várias vezes durante a atualização. As atualizações de ativos principais normalmente fazem com que o ativo entre em um estágio WIP.
* **DAM:** Gerenciamento de ativos digitais. Neste documento, ele é sinônimo de Experience Manager Assets, a menos que especificamente mencionado o contrário.
* **Usuário criativo**: um profissional criativo, que cria ativos digitais usando aplicativos e serviços da Creative Cloud. Em alguns casos, um usuário criativo pode ser membro de uma equipe criativa que pode usar a Creative Cloud, mas não cria ativos digitais (como um diretor criativo ou gerente de equipe criativa).
* **Usuário do DAM:** um usuário típico de um sistema DAM. Dependendo da organização, um usuário do DAM pode ser um usuário de marketing ou não, por exemplo, um usuário de Linha de Negócios (LOB), um bibliotecário, um vendedor e assim por diante.

### Considerações ao usar a integração do Experience Manager e do Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Este é um breve resumo das práticas recomendadas para a integração do Experience Manager e do Creative Cloud. Leia o restante deste documento para obter a compreensão detalhada desses itens.

* **Para usuários criativos, que trabalham no Photoshop, InDesign ou Illustrator:** o Adobe Asset Link fornece a melhor experiência do usuário, incluindo a manipulação limpa do Trabalho em andamento em ativos tirados do Experience Manager
* **Para simplificar o acesso a ativos do desktop para qualquer formato de arquivo ou aplicativo genérico:** use o aplicativo de desktop do Experience Manager
* **Entenda por que e quando armazenar ativos no DAM:** atualizações a serem disponibilizadas para a equipe maior em sua organização
* **Considere o volume de ativos compartilhados:** se o caso de uso for a distribuição de ativos, a governança e a segurança podem ser os aspectos mais importantes. Considere usar ferramentas criadas para fazer isso em escala, como o Brand Portal.
* **Entenda o ciclo de vida do ativo:** saiba como os ativos são manipulados em sua organização por equipes diferentes
* **Lidar com salvamentos frequentes em ativos com cuidado:** o Adobe Asset Link cuida disso para você com PS, AI, ID. Para outros aplicativos, não realize tarefas em andamento na pasta mapeada/compartilhada, a menos que precise de todas as alterações no DAM

### Acesso aos ativos do Adobe Stock pelo Experience Manager Assets {#access-to-adobe-stock-assets-from-aem-assets}

A [integração do Experience Manager e do Adobe Stock](/help/assets/aem-assets-adobe-stock.md) fornece aos usuários do Experience Manager a capacidade de pesquisar, visualizar, licenciar e salvar ativos do Adobe Stock na Experience Manager. Os ativos licenciados e salvos do Adobe Stock selecionaram metadados do Stock, que podem ser usados para pesquisá-los com filtros extras.

Alguns pontos importantes sobre essa integração:

* Quando os ativos do estoque do Adobe são salvos no Experience Manager, eles se tornam um Experience Manager Assets comum, com o binário salvo no repositório do Experience Manager. Alguns metadados relacionados ao Adobe Stock são salvos para o ativo no Experience Manager, caso contrário, o processo de assimilação será o mesmo de qualquer outro arquivo. Por exemplo, se as Tags inteligentes estiverem ativas, as tags serão adicionadas a esses ativos ao salvar.
* O ativo salvo no Experience Manager é uma cópia, não um link de volta para o Adobe Stock.

**Trabalhando com ativos salvos do Adobe Stock no Experience Manager no Creative Cloud**. Essa integração não depende do Adobe Asset Link, mas o Adobe Asset Link reconhece esses ativos salvos do Stock dessa maneira e exibe metadados adicionais e ícone do Stock nesses ativos na interface de extensão do Adobe Asset Link no Photoshop, Illustrator ou InDesign. Os arquivos estão disponíveis para navegação, abertura etc., pois são ativos comuns do Experience Manager quando salvos no Experience Manager.
Os usuários do Creative que trabalham em aplicativos do Creative Cloud com a extensão Adobe Asset Link presentes, além de terem acesso a ativos já licenciados do Adobe Stock para o Experience Manager, também podem usar o painel do Creative Cloud Libraries para pesquisar, visualizar e licenciar ativos do Adobe Stock.
O Assets do Adobe Stock licenciado e salvo no Experience Manager fica disponível para as equipes mais amplas que acessam a implantação do Experience Manager Assets, enquanto os ativos de licenciamento criativos do Adobe Stock por meio do painel do Creative Cloud Libraries os tornam disponíveis somente para si mesmos por padrão em sua conta do Creative Cloud.

## Sobre o armazenamento de ativos em um DAM {#about-storing-assets-in-a-dam}

Para projetar um fluxo de trabalho eficiente entre as equipes de criação e marketing/linha de negócios (LOB) e escolher os melhores recursos de suporte, é importante entender quando e por que os ativos são armazenados no DAM.

### Por que os ativos são armazenados no DAM {#why-assets-are-stored-in-dam}

Armazenar ativos no DAM facilita o acesso e a localização. Ele garante que os ativos possam ser usados por vários usuários em toda a organização ou ecossistema, o que inclui parceiros, clientes e assim por diante.

A maioria das organizações opta por armazenar somente ativos que são relevantes para os processos de marketing/LOB de downstream (publicação em canais como o canal da Web por meio do Experience Manager Sites ou outros canais atendidos pela Adobe Experience Cloud — Marketing Cloud, Advertising Cloud e medidos pelo Analytics Cloud, fornecimento para usuários/parceiros etc.). Além disso, as organizações armazenam ativos que podem estar sujeitos a um processo de revisão/aprovação no DAM. Dessa forma, o DAM armazena principalmente ativos que têm altas chances de serem usados e evita o armazenamento de ativos ociosos.

O armazenamento de ativos também está sujeito a considerações técnicas e de utilização de recursos. O DAM fornece serviços adicionais sobre ativos armazenados, incluindo extração de metadados, controle de versão, geração de visualizações/transcodificação, gerenciamento de referências e adição de informações de controle de acesso. Esses serviços consomem mais tempo e recursos de infraestrutura.

Geralmente, armazenar todos os ativos e atualizações não é desejável. Por exemplo, se as atualizações de ativos específicos forem de baixa qualidade e consumirem recursos excessivos, os ativos podem não ser armazenados no DAM.

#### Quando os ativos são armazenados no DAM {#when-assets-are-stored-in-dam}

As equipes (e organizações) da Creative geralmente não estão interessadas em armazenar ativos em cada estágio do ciclo de vida do ativo. Por exemplo, eles evitam armazenar ativos nos seguintes casos:

* Assets que ainda não foram finalizados ou estão sujeitos a experimentação
* Assets que não passam no ciclo de revisão criativa/interna da equipe
* Em comparação ao ativo em questão, a equipe tem melhores candidatos para representar seu trabalho para equipes externas

Normalmente, as seguintes classes de ativos são armazenadas no DAM:

* Assets que atingiram uma certa maturidade e são considerados prontos para serem compartilhados
* Assets que foram pré-selecionados pela equipe criativa
* Formatos de ativos específicos que podem ser usados ou solicitados por marketing, dependendo de um contrato ou contrato específico (por exemplo, arquivos JPG convertidos de arquivos RAW, TIFFs/imagens de originais do PSD)

#### Quando as atualizações de ativos são armazenadas no DAM {#when-updates-to-assets-are-stored-in-dam}

Como regra, somente as atualizações de ativos que são relevantes para o conjunto mais amplo de usuários do DAM devem ser armazenadas no DAM. Ele garante que os usuários (marketing e funções semelhantes) vejam apenas as versões relevantes na linha do tempo do ativo DAM.

Normalmente, alterações relacionadas aos principais marcos no ciclo de vida do ativo. Por exemplo, o ativo pronto para marketing inicial ou uma atualização oficial com base na solicitação/revisão fornecida pela equipe criativa deve ser armazenado e ter a versão atualizada no DAM.

A atualização da equipe criativa para análise pela equipe de marketing após uma solicitação de alteração no ativo existente no DAM é um exemplo de atualização relevante. Ele deve ser armazenado e ter sua versão atualizada no DAM para referência adicional ou para reverter para a versão anterior.

Veja a seguir exemplos de atualizações que normalmente não são relevantes:

* Versões anteriores de ativos carregados antes de estarem prontos para revisão de marketing
* Alterações criativas frequentes no ativo na fase de trabalho em andamento antes que as equipes de criação e marketing decidam que o ativo está pronto

### Acesso do usuário ao DAM {#user-access-to-dam}

O Experience Manager Assets oferece suporte a dois tipos de usuários com base em seu acesso à implantação do Experience Manager Assets. Normalmente, os usuários dentro da rede corporativa (firewall) têm acesso direto ao DAM. Outros usuários fora da rede corporativa não teriam acesso direto. O tipo de usuário determina quais integrações podem ser usadas do ponto de vista técnico.

#### Usuários do Creative com acesso direto ao DAM {#creative-users-with-direct-access-to-dam}

Normalmente, as equipes de criação internas ou as agências/profissionais de criação integrados à rede interna têm acesso à instância do DAM, incluindo o logon do Experience Manager. O Experience Manager e a infraestrutura de rede podem ser configurados para permitir o acesso direto a terceiros, geralmente organizações confiáveis, como agências que trabalham para um cliente, para ter acesso ao Experience Manager pela rede, por exemplo, via VPN ou lista de permissões IP.

Nesses casos, o Adobe Asset Link ou o aplicativo de desktop Experience Manager fornece acesso fácil a ativos finais/aprovados e permite salvar ativos prontos para criação no DAM.

#### Usuários do Creative sem acesso ao DAM {#creative-users-without-access-to-dam}

Agências externas e freelancers sem acesso direto à instância do DAM podem exigir acesso a ativos aprovados ou adicionar seus novos designs ao DAM.

Use as seguintes estratégias para fornecer acesso aos ativos finais/aprovados:

* Use o aplicativo de desktop se o Asset Link não funcionar.
* Use o [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para distribuir ativos com segurança para parceiros externos
* Use uma implementação personalizada de um portal de distribuição e fornecimento com base em [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Use o Controle de acesso configurado no Experience Manager e a infraestrutura de rede necessária (por exemplo, VPN e lista de permissões de IP) para conceder a terceiros acesso a uma área dedicada de conteúdo em seu DAM. Eles podem usar a interface da Web do Experience Manager para obter ativos e fazer upload de novo conteúdo para o seu DAM.

#### Trabalho em andamento em ativos do Experience Manager {#work-in-progress-on-assets-from-aem}

Conforme discutido neste documento, é recomendável realizar grandes atualizações nos ativos, às vezes chamadas de trabalho em andamento, sem que todas as edições salvas no arquivo local também sejam carregadas no Experience Manager como alterações. Isso acelera o trabalho de um usuário de desktop, limita a largura de banda de rede usada e mantém a linha do tempo dos ativos limpa e concentrada em atualizações importantes e controladas.

O Adobe Asset Link oferece um bom suporte para esse caso de uso:

* Quando os usuários no Photoshop, InDesign ou Illustrator pretendem editar um arquivo, eles executam uma operação de Check-out no ativo especificado
* O ativo é baixado em segundo plano, é colocado na conta do Creative Cloud dos usuários sincronizada ao disco pelo aplicativo de desktop do Creative Cloud e o sinalizador de check-out é alternado no Experience Manager no ativo para minimizar os conflitos de edição
* A partir daí, o usuário trabalha em um arquivo armazenado localmente no local sincronizado e pode continuar trabalhando e salvando as alterações necessárias a qualquer frequência necessária
* Além disso, como o ativo está na conta do Creative Cloud, ele também está disponível em outros dispositivos que o usuário pode ter (por exemplo, pode ser aberto ou editado em um aplicativo móvel dedicado do Creative Cloud) e pode ser compartilhado com outros usuários do Creative Cloud para fins de colaboração.
* Quando o usuário criativo conclui as alterações, ele pode executar uma operação de Check-in nesse arquivo no aplicativo Creative Cloud com um comentário opcional. O ativo correspondente no Experience Manager tem a versão e é atualizado para com o novo binário. Usuários do Experience Manager, como profissionais de marketing ou usuários de LOB, têm acesso a grandes alterações de ativos, ou marcos, por meio da interface do usuário da linha do tempo do ativo do Experience Manager.

O aplicativo de desktop do Experience Manager fornece um compartilhamento de rede para ativos abertos no aplicativo nativo. Por padrão, todas as alterações feitas localmente são carregadas no Experience Manager automaticamente após um breve período. Com essa configuração, salvamentos frequentes durante a fase de trabalho em andamento seriam carregados no Experience Manager e teriam suas versões alteradas, criando uma grande quantidade de tráfego de rede e possíveis desafios de escalabilidade, sem mencionar as versões desnecessárias no Experience Manager.

A abordagem recomendada aqui é usar uma opção no aplicativo de desktop do Experience Manager para desativar atualizações automatizadas e fazer upload de alterações em ativos para o Experience Manager manualmente, usando a ação fazer upload de alterações na interface do usuário de status do ativo do aplicativo.

#### Upload em massa para DAM {#bulk-upload-to-dam}

Você pode ter um requisito para carregar simultaneamente um número maior de arquivos no DAM em alguns cenários, por exemplo:

* Carregamento de resultados de sessão de fotos para projetos maiores
* Upload de ativos fornecidos por agências de criação
* Fazer upload de ativos selecionados de um conjunto maior se a seleção for feita fora do DAM

Essa descrição se refere ao upload de arquivos operacionalmente (por exemplo, toda semana ou com cada sessão de fotos ), como uma parte normal do fluxo de trabalho do usuário do desktop. As migrações de ativos grandes não são contempladas aqui.

Você pode usar os seguintes recursos de upload:

* Para carregar pastas grandes/hierárquicas em massa, use o aplicativo de desktop do Experience Manager que fornece a funcionalidade de [carregamento de pasta](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets). Também é possível fazer upload de estruturas hierárquicas de pastas. O Assets é carregado em segundo plano e, portanto, não está vinculado a uma sessão do navegador da Web
* Para fazer upload de alguns arquivos de uma única pasta, arraste os arquivos diretamente para a interface da Web ou use a opção Criar na interface da Web do Experience Manager Assets.
* Dependendo das necessidades da sua empresa, também é possível usar o carregador personalizado.

#### Gerenciamento de ativos digitais diretamente do desktop {#managing-digital-assets-directly-from-desktop}

Se você usa compartilhamentos de arquivos de rede para gerenciar ativos digitais, usar o compartilhamento de rede mapeado pelo aplicativo de desktop do Experience Manager pode ser visto como um substituto conveniente. Ao fazer a transição de compartilhamentos de arquivos de rede, a interface da Web do Experience Manager fornece um conjunto avançado de recursos de Gerenciamento de ativos digitais que vão muito além do que é possível em um compartilhamento de rede (pesquisa, coleções, metadados, colaboração, visualizações e assim por diante), e o aplicativo de desktop do Experience Manager fornece um link útil para conectar o repositório DAM do lado do servidor ao trabalho no desktop.

Evite usar o aplicativo de desktop do Experience Manager para gerenciar ativos diretamente no compartilhamento de rede do Experience Manager Assets. Por exemplo, evite usar o aplicativo de desktop do Experience Manager para mover/copiar vários arquivos. Em vez disso, use a interface da Web do Experience Manager Assets para arrastar as pastas do Finder/Explorer para o compartilhamento de rede ou use o recurso Upload de pasta do Experience Manager Assets.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
