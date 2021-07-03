---
title: Práticas recomendadas para integrar com [!DNL Adobe Creative Cloud]
description: As práticas recomendadas integram uma implantação do Experience Manager com o Adobe Creative Cloud para simplificar os fluxos de trabalho de transferência de ativos e obter o máximo de eficiência.
contentOwner: AG
mini-toc-levels: 1
feature: Colaboração, Adobe Asset Link, Aplicativo de desktop
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 18%

---

# Práticas recomendadas de integração de AEM e Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

O Adobe Experience Manager (AEM) Assets é uma solução de gerenciamento de ativos digitais (DAM) que pode se integrar ao Adobe Creative Cloud para ajudar os usuários do DAM a trabalhar junto às equipes de criação, simplificando a colaboração no processo de criação de conteúdo.

A Adobe Creative Cloud fornece às equipes criativas um ecossistema de soluções e serviços para ajudá-las a criar ativos digitais. Ele inclui aplicativos móveis e de desktop, serviços em nuvem como armazenamento com sincronização de desktop ou experiência na Web, além de mercados como o Adobe Stock.

Leia para saber quais integrações devem ser escolhidas entre o desktop e o DAM de nível empresarial com base no seu caso de uso e quais são as práticas recomendadas associadas para os workflows de conexão.

>[!NOTE]
>
>AEM ao compartilhamento de pasta do Creative Cloud agora está obsoleto e não é mais coberto abaixo. O Adobe recomenda recursos mais recentes, como o Adobe Asset Link ou AEM aplicativo de desktop para fornecer aos usuários criativos acesso aos ativos gerenciados no AEM.

## Necessidade de colaboração de criativos, profissionais de marketing e usuários do DAM {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superfícies envolvidas |
|---|---|---|
| Simplifique a experiência para criações no desktop | Simplifique o acesso a ativos de um DAM (AEM Assets) para profissionais criativos ou, de maneira mais ampla, para usuários em desktop que trabalham em aplicativos nativos de criação de ativos. Eles precisam de uma maneira fácil e direta de descobrir, usar (abrir), editar e salvar alterações em AEM, bem como fazer upload de novos arquivos. | Área de trabalho Win ou Mac; Creative Cloud apps |
| Fornecer ativos de alta qualidade e prontos para uso da Adobe Stock | Os profissionais de marketing ajudam a acelerar o processo de criação de conteúdo, auxiliando no fornecimento e descoberta de ativos. Profissionais de criação usam os ativos aprovados diretamente de suas ferramentas criativas. | AEM Assets; Mercado Adobe Stock; campos de metadados |
| Distribuir e compartilhar ativos por organizações | Os departamentos internos/ramificações locais e parceiros externos, distribuidores e agências usam os ativos aprovados compartilhados pela organização pai. A organização deseja compartilhar com segurança e facilidade os ativos criados para reutilização mais ampla. | Brand Portal, Compartilhamento de Ativos Commons |

## Ofertas do Adobe para dar suporte à necessidade de colaboração {#adobe-offerings-to-support-the-collaboration-need}

| Proposta de valor para as personas envolvidas | oferta de Adobe | Superfícies envolvidas |
|---|---|---|
| Os usuários criativos descobrem ativos de AEM, abrem e usam, editam e fazem upload de alterações no AEM, bem como fazem upload de novos arquivos no AEM, sem sair dos aplicativos Creative Cloud. | [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign |
| Os usuários empresariais simplificam a abertura e o uso de ativos, a edição e o upload de alterações no AEM e o upload de novos arquivos no AEM a partir do ambiente de desktop. Eles usam uma integração genérica para abrir qualquer tipo de ativo no aplicativo de desktop nativo, incluindo os não-Adobe. | Aplicativo de desktop do [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en) | AEM aplicativo de desktop no desktop Win e Mac |
| Profissionais de marketing e usuários empresariais descobrem, visualizam, licenciam e salvam e gerenciam os ativos da Adobe Stock a partir do AEM. Os ativos licenciados e salvos fornecem metadados Adobe Stock selecionados para melhor governança. | [Integração do Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | Interface da Web AEM |

Este artigo foca principalmente nos dois primeiros aspectos das necessidades de colaboração. A distribuição e o fornecimento de ativos em escala são brevemente mencionadas como um caso de uso. Para essas necessidades, considere o Adobe Brand Portal ou o Asset Share Commons. Soluções alternativas, como o [Brand Portal do AEM Assets](https://helpx.adobe.com/br/experience-manager/brand-portal/user-guide.html), soluções que podem ser criadas com base nos componentes do [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Compartilhamento de links](share-assets.md), usando a [interface do usuário na Web do AEM Assets](/help/assets/manage-digital-assets.md) devem ser revisadas com base em requisitos específicos.

![Conexões de Creative Cloud para AEM: Decidir qual recurso usar](assets/creative-connections-aem.png)

Decisão sobre qual recurso usar

### Mapeamento de casos de uso e soluções Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso de uso | Adobe Asset Link | Aplicativo de desktop do AEM | Observações ou métodos alternativos |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Discover - procurar AEM pastas | Sim | AEM interface do usuário da Web + ações da área de trabalho | Ao navegar pelo compartilhamento de rede, desative as miniaturas para evitar o download de arquivos binários de ativos. |
| Discover - acesso AEM coleções | Sim | AEM interface do usuário da Web + ações da área de trabalho |  |
| Discover - pesquisar ativos do AEM | Sim | AEM interface do usuário da Web + ações da área de trabalho |  |
| Usar - abrir ativo | Sim | Sim - para qualquer aplicativo | [Abrir do ](/help/assets/manage-digital-assets.md#previewing-assets) interface da Web ou do Finder |
| Usar - colocar ativo de AEM em um documento | Sim - incorporação | Sim - vinculação ou incorporação | AEM aplicativo de desktop fornece acesso a ativos como arquivos no sistema de arquivos local. Esses links nos aplicativos nativos são representados por caminhos locais. |
| Editar - abrir para edição | Sim - Ação de check-out | Sim - Abrir ação (no compartilhamento de rede) | [O check-out no ](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) AAL salva o ativo na conta de armazenamento da creative cloud do usuário (sincronizada pelo aplicativo do Creative Cloud) por padrão. |
| Editar - trabalho em andamento fora do AEM | Sim - Ativo disponível na conta de armazenamento de Creative Cloud do usuário sincronizada com o desktop. | Sim |  |
| Editar - fazer upload de alterações | Sim - [Ação de check-in](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) com comentário opcional | Sim |  |
| Upload - arquivo único | Sim - carrega o documento ativo atual | Sim | [Fazer upload via interface da Web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Upload - vários arquivos / estruturas hierárquicas de pastas | Não | Sim | [Fazer upload via interface](/help/assets/manage-digital-assets.md#uploading-assets) da Web; Ferramenta ou script personalizado |
| Misc - usuário e logon | O usuário Creative Cloud conectado ao aplicativo de desktop Creative Cloud é reconhecido (SSO) | Usuário AEM/logon | Os usuários de ambas as soluções contam com a cota de usuários AEM. |
| Misc - rede e acesso | Requer acesso do desktop do usuário para AEM implantação pela rede | Requer acesso do desktop do usuário para AEM implantação pela rede | O Adobe Asset Link não compartilha o ambiente proxy de rede. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Para suportar casos de uso de distribuição de ativos, outras soluções devem ser consideradas:

* [AEM Assets Brand ](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) Portalpara um complemento configurável do Assets para publicar ativos.

* As soluções personalizadas são criadas com base no código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) base.
* AEM [link compartilhe](/help/assets/share-assets.md) para compartilhar ativos ad hoc usando links.
* [A interface da Web do AEM Assets ](/help/assets/manage-digital-assets.md) com áreas para terceiros externos garantidas pela configuração do Controle de acesso AEM e pelos ajustes necessários de configuração de TI/rede, dando a esses usuários externos acesso ao AEM.

## Principais conceitos e casos de uso {#key-concepts-and-use-cases}

### Glossário de termos comuns {#glossary-of-common-terms}

* **Trabalho em andamento ou trabalho criativo em andamento (WIP)**: uma fase no ciclo de vida do ativo em que um ativo sofre várias alterações e normalmente ainda não está pronto para ser compartilhado com equipes maiores.
* **Ativos prontos para criação**: os ativos que prontos para serem compartilhados com uma equipe maior ou que foram selecionados/aprovados pela equipe criativa para compartilhamento com equipes de marketing ou LOB.

* **Aprovações de ativos**: o processo de aprovação que executa ativos já carregados no DAM, que normalmente inclui aprovações de marca, legais e assim por diante.
* **Ativo final**: um ativo que passou por todas as aprovações/marcações de metadados e está pronto para ser usado pela equipe maior. Esse ativo é armazenado no DAM e disponibilizado a todos os usuários (ou a todos os interessados). Ele pode ser usado em canais de marketing ou por equipes criativas para criar designs.

* **Atualização/alteração de ativos secundários:** uma pequena e rápida mudança em um ativo digital. Geralmente é feito em resposta a uma solicitação de retoque ou edição secundária, revisão de ativos ou aprovação (por exemplo, reposição, alteração do tamanho do texto, ajuste da saturação/brilho, cor e assim em diante).
* **Atualizações/alterações de ativos principais:** uma mudança em um ativo digital que requer trabalho considerável, e às vezes deve ser feita por um período mais longo. Normalmente, inclui várias alterações. O ativo deve ser salvo várias vezes durante a atualização. As atualizações de ativos principais normalmente fazem com que o ativo entre em um estágio WIP.
* **DAM:** Gerenciamento de ativos digitais. Neste documento, ele é sinônimo do AEM Experience Manager Assets, a menos que especificamente mencionado o contrário.
* **Usuário criativo**: um profissional criativo, que cria ativos digitais usando aplicativos e serviços da Creative Cloud. Em alguns casos, um usuário criativo pode ser membro de uma equipe criativa que pode usar a Creative Cloud, mas não cria ativos digitais (como um diretor criativo ou gerente de equipe criativa).
* **Usuário do DAM:** um usuário típico de um sistema DAM. Dependendo da organização, um usuário do DAM pode ser um usuário de marketing ou não, por exemplo, um usuário de Linha de Negócios (LOB), um bibliotecário, um vendedor e assim por diante.

### Considerações ao usar a integração AEM e Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Este é um breve resumo das práticas recomendadas para a integração do AEM &amp; Creative Cloud. Leia o resto deste documento para obter a compreensão detalhada sobre eles.

* **Para usuários criativos, que trabalham no Photoshop, InDesign ou Illustrator:** o do Adobe Asset Link fornece a melhor experiência do usuário, incluindo a manipulação limpa do Trabalho em andamento em ativos tirados do AEM
* **Para simplificar o acesso a ativos do desktop para qualquer formato de arquivo ou aplicativo genérico:** use o aplicativo de desktop do AEM
* **Entenda por que e quando armazenar ativos no DAM:** atualizações a serem disponibilizadas para a equipe maior em sua organização
* **Considere o volume de ativos compartilhados:** se o caso de uso for a distribuição de ativos, a governança e a segurança podem ser os aspectos mais importantes. Considere usar ferramentas criadas para fazer isso em escala, como o Brand Portal.
* **Entenda o ciclo de vida do ativo:** saiba como os ativos são manipulados em sua organização por equipes diferentes
* **Lidar com salvamentos frequentes em ativos com cuidado:** o Adobe Asset Link cuida disso para você com PS, AI, ID. Em outros aplicativos, não realize tarefas em andamento na pasta mapeada/compartilhada, a menos que precise de todas as alterações no DAM

### Acesso aos ativos do Adobe Stock da AEM Assets {#access-to-adobe-stock-assets-from-aem-assets}

[A ](/help/assets/aem-assets-adobe-stock.md) integração do AEM e do Adobe Stock fornece AEM usuários a capacidade de pesquisar, visualizar, licenciar e salvar ativos do Adobe Stock no AEM. Os ativos licenciados e salvos do Adobe Stock selecionaram metadados de Estoque, que podem ser usados para pesquisá-los com filtros extras.

Alguns pontos importantes sobre essa integração:

* Quando os ativos do Adobe stock são salvos em AEM, eles se tornam um AEM Assets comum, com o binário salvo no repositório AEM. Alguns metadados relacionados ao Adobe Stock são salvos para o ativo no AEM, caso contrário, o processo de assimilação será igual ao de qualquer outro arquivo. Por exemplo, se as Tags inteligentes estiverem ativas, as tags serão adicionadas a esses ativos ao salvar.
* O ativo salvo em AEM é uma cópia, não um link de volta ao Adobe Stock.

**Trabalhar com ativos salvos do Adobe Stock em AEM no Creative Cloud**. Essa integração é independente do Adobe Asset Link, mas o Adobe Asset Link reconhece esses ativos salvos do Stock dessa forma e exibe metadados adicionais e ícone de Estoque nesses ativos na interface do usuário da extensão Adobe Asset Link no Photoshop, Illustrator ou InDesign. Os arquivos estão disponíveis para navegação, abertura e assim por diante, porque são ativos de AEM comuns quando salvos em AEM.
Usuários criativos que trabalham em aplicativos Creative Cloud com a extensão Adobe Asset Link presentes, além de terem acesso a ativos já licenciados da Adobe Stock no AEM, também podem usar o painel Bibliotecas Creative Cloud para pesquisar, visualizar e licenciar ativos da Adobe Stock.
Os ativos da Adobe Stock licenciados e salvos em AEM ficam disponíveis para as equipes mais amplas que acessam a implantação do AEM Assets, enquanto os ativos de licenciamento da Adobe Stock por meio do painel Creative Cloud Bibliotecas os disponibilizam somente para si por padrão em sua conta Creative Cloud.

## Sobre o armazenamento de ativos em um DAM {#about-storing-assets-in-a-dam}

Para projetar um fluxo de trabalho eficiente entre equipes de criação e de marketing/linha de negócios (LOB) e escolher os melhores recursos de suporte, é importante entender quando e por que os ativos são armazenados no DAM.

### Por que os ativos são armazenados no DAM {#why-assets-are-stored-in-dam}

Armazenar ativos no DAM os torna facilmente acessíveis e acessíveis. Ela garante que os ativos possam ser aproveitados por vários usuários na organização ou no ecossistema, o que inclui parceiros, clientes e assim por diante.

A maioria das organizações opta por armazenar apenas ativos relevantes para os processos de marketing/LOB de downstream (publicação em canais como canal da Web pelo AEM Sites ou outros canais fornecidos pelo Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e medidos pelo Analytics Cloud, fornecendo a usuários/parceiros e assim por diante). Além disso, as organizações armazenam ativos que podem estar sujeitos a um processo de revisão/aprovação no DAM. Dessa forma, o DAM armazena principalmente ativos que têm altas chances de serem aproveitados e evita o armazenamento de ativos inativos.

O armazenamento de ativos também está sujeito a considerações técnicas e de utilização de recursos. O DAM fornece serviços adicionais sobre ativos armazenados, incluindo extração de metadados, controle de versão, geração de visualizações/transcodificação, gerenciamento de referências e adição de informações de controle de acesso. Esses serviços consomem mais tempo e recursos de infraestrutura.

Geralmente, o armazenamento de todos os ativos e atualizações não é desejável. Por exemplo, se as atualizações de ativos específicos forem de baixa qualidade e consumirem recursos excessivos, os ativos podem não ser armazenados no DAM.

#### Quando os ativos são armazenados no DAM {#when-assets-are-stored-in-dam}

Geralmente, as equipes criativas (e organizações) não estão interessadas em armazenar ativos em cada estágio do ciclo de vida do ativo. Por exemplo, eles evitam armazenar ativos nos seguintes casos:

* Ativos que ainda não foram finalizados ou estão sujeitos a experimentação
* Ativos que não passam no ciclo de análise do criativo/da equipe interna
* Em comparação com o ativo em questão, a equipe tem melhores candidatos para representar seu trabalho para equipes externas

Normalmente, os seguintes ativos de classes são armazenados no DAM:

* Ativos que atingiram um determinado prazo e são considerados prontos para serem partilhados
* Ativos pré-selecionados pela equipe criativa
* Formatos de ativos específicos que podem ser usados ou solicitados pelo marketing, dependendo de um contrato ou contrato específico (por exemplo, arquivos JPG convertidos de arquivos RAW, TIFFs/imagens de originais PSD)

#### Quando as atualizações de ativos são armazenadas no DAM {#when-updates-to-assets-are-stored-in-dam}

Como regra, somente as atualizações de ativos relevantes para o conjunto mais amplo de usuários do DAM devem ser armazenadas no DAM. Isso garante que os usuários (marketing e funções semelhantes) visualizem apenas as versões relevantes na linha do tempo do ativo do DAM.

Normalmente, as alterações estão relacionadas aos marcos principais no ciclo de vida do ativo. Por exemplo, o ativo pronto para marketing ou uma atualização oficial com base na solicitação/revisão fornecida pela equipe criativa deve ser armazenado e ter controle de versão no DAM.

A atualização da equipe criativa para revisão pela equipe de marketing após uma solicitação de alteração do ativo existente no DAM é um exemplo de uma atualização relevante. Ele deve ser armazenado e ter controle de versão no DAM para referência adicional ou para reverter para a versão anterior.

A seguir estão exemplos de atualizações que normalmente não são relevantes:

* Versões anteriores dos ativos carregados antes de estarem prontos para análise de marketing
* Alterações criativas frequentes no ativo na fase de trabalho em andamento antes que as equipes criativas e de marketing decidam que o ativo está pronto

### Acesso do usuário ao DAM {#user-access-to-dam}

O AEM Assets oferece suporte a dois tipos de usuários com base no acesso à implantação do AEM Assets. Normalmente, os usuários dentro da rede corporativa (firewall) têm acesso direto ao DAM. Outros utilizadores fora da rede empresarial não teriam acesso direto. O tipo de usuário determina quais integrações podem ser usadas do ponto de vista técnico.

#### Usuários criativos com acesso direto ao DAM {#creative-users-with-direct-access-to-dam}

Normalmente, as equipes criativas internas ou os profissionais de criação/integrados à rede interna têm acesso à instância do DAM, incluindo AEM logon. AEM e infraestrutura de rede podem ser configuradas para permitir acesso direto a partes externas - geralmente organizações confiáveis como agências que trabalham para um cliente - para ter acesso a AEM pela rede, por exemplo, via VPN ou lista de permissões IP.

Nesses casos, o Adobe Asset Link ou AEM aplicativo de desktop fornece acesso fácil a ativos finais/aprovados e permite salvar ativos prontos para criação no DAM.

#### Usuários criativos sem acesso ao DAM {#creative-users-without-access-to-dam}

Agências externas e independentes sem acesso direto à instância do DAM podem exigir acesso a ativos aprovados ou desejar adicionar seus novos designs ao DAM.

Use as seguintes estratégias para fornecer acesso a ativos finais/aprovados:

* Use o aplicativo de desktop se o Asset Link não funcionar.
* Use [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) para distribuir ativos com segurança para parceiros externos
* Use uma implementação personalizada de um portal de distribuição e fornecimento com base em [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Use o Controle de Acesso configurado em AEM e a infraestrutura de rede necessária (por exemplo, lista de permissões de VPN e IP) para conceder a terceiros acesso a uma área dedicada de conteúdo no DAM. Eles podem usar AEM interface do usuário da Web para obter ativos e carregar novo conteúdo no DAM.

#### Trabalho em andamento em ativos do AEM {#work-in-progress-on-assets-from-aem}

Conforme discutido neste documento, é recomendável realizar atualizações importantes em ativos, às vezes chamados de trabalho em andamento, sem ter todas as edições salvas no arquivo local também enviadas para o AEM como alterações. Isso acelera o trabalho de um usuário de desktop, limita a largura de banda da rede usada e mantém a linha do tempo dos ativos limpa e focada em atualizações importantes e controladas.

O Adobe Asset Link oferece um bom suporte para este caso de uso:

* Quando os usuários do Photoshop, InDesign ou Illustrator pretendem editar um arquivo, eles executam uma operação de Check-out no ativo em questão
* O ativo é baixado em segundo plano, colocado na conta do Creative Cloud de usuários sincronizada ao disco pelo aplicativo de desktop do Creative Cloud e o sinalizador de check-out é alternado no AEM do ativo para minimizar conflitos de edição
* A partir daí, o usuário trabalha em um arquivo armazenado localmente no local sincronizado e pode continuar trabalhando e salvando as alterações necessárias a qualquer frequência necessária
* Além disso, como o ativo está na conta do Creative Cloud, ele também está disponível em outros dispositivos que o usuário pode ter (por exemplo, pode ser aberto ou editado em um aplicativo móvel Creative Cloud dedicado) e pode ser compartilhado com outros usuários do Creative Cloud para fins de colaboração.
* Quando o usuário criativo terminar com as alterações, ele poderá executar uma operação de Check-in nesse arquivo em seu aplicativo Creative Cloud, com um comentário opcional. O ativo correspondente no AEM tem controle de versão e é atualizado para com o novo binário. Usuários AEM como profissionais de marketing ou LOB têm acesso a grandes alterações de ativos ou marcos, por meio AEM interface do usuário da linha do tempo do ativo.

AEM aplicativo de desktop fornece um compartilhamento de rede para ativos abertos no aplicativo nativo. Por padrão, todas as alterações feitas localmente são carregadas para AEM automaticamente após algum tempo. Com tal configuração, salvas frequentes durante a fase de trabalho em andamento seriam todas carregadas em AEM e versão, criando muito tráfego de rede e possíveis desafios de escalabilidade - para não mencionar versões desnecessárias em AEM.

A abordagem recomendada aqui é usar uma opção AEM aplicativo de desktop para desativar atualizações automatizadas e fazer upload de alterações em ativos para AEM manualmente, aproveitando a ação de upload de alterações na interface do usuário de status do ativo do aplicativo.

#### Upload em massa no DAM {#bulk-upload-to-dam}

Você pode ter um requisito para fazer upload simultâneo de um número maior de arquivos no DAM em alguns cenários, por exemplo:

* Upload de resultados de sessão fotográfica ou projetos maiores
* Upload de ativos fornecidos por agências criativas
* Fazer upload dos ativos selecionados de um conjunto maior se a seleção for feita fora do DAM

Observe que esta descrição se refere ao upload de arquivos operacionalmente (por exemplo, toda semana ou com cada sessão fotográfica ), como uma parte normal do fluxo de trabalho do usuário do desktop. As migrações de ativos grandes não são contempladas aqui.

Você pode aproveitar os seguintes recursos de upload:

* Para fazer upload de pastas grandes/hierárquicas em massa, use AEM aplicativo de desktop que fornece a funcionalidade [upload de pasta](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload). Também é possível fazer upload de estruturas hierárquicas de pastas. Os ativos são carregados em segundo plano e, portanto, não estão vinculados a uma sessão do navegador da Web
* Para carregar alguns arquivos de uma única pasta, arraste os arquivos diretamente para a interface da Web ou use a opção Criar na interface da Web do AEM Assets.
* Dependendo dos requisitos de sua empresa, você também pode usar o carregador personalizado.

#### Gerenciamento de ativos digitais diretamente do desktop {#managing-digital-assets-directly-from-desktop}

Se você usar os Compartilhamentos de arquivo de rede para gerenciar ativos digitais, apenas o uso do compartilhamento de rede mapeado por AEM aplicativo de desktop pode ser visto como um substituto conveniente. Ao fazer a transição dos compartilhamentos de arquivos de rede, AEM interface da Web fornece um conjunto avançado de recursos de Gerenciamento de ativos digitais que vão muito além do que é possível em um compartilhamento de rede (pesquisa, coleções, metadados, colaboração, visualizações e assim por diante) e AEM aplicativo de desktop fornece um link útil para conectar o repositório DAM do lado do servidor ao trabalho no desktop.

Evite usar AEM aplicativo de desktop para gerenciar ativos diretamente no compartilhamento de rede do AEM Assets. Por exemplo, evite usar AEM aplicativo de desktop para mover/copiar vários arquivos. Em vez disso, use a interface do usuário da Web do AEM Assets para arrastar as pastas do Localizador/Explorer para o compartilhamento de rede ou usar o recurso de Upload de pasta do AEM Assets.

<!-- 
#### Asset migration {#asset-migration}

To plan and execute asset migrations from existing system to a new system or migration of large volume of assets stored on servers, see the [Migration Guide](/help/assets/assets-migration-guide.md). AEM desktop app and AEM to Creative Cloud integrations do not support such migrations. Due to the large volumes of assets to be ingested, and additional requirements around metadata mapping, transformation, and ingestion, migrations should be handled using different tools and approaches.
-->
