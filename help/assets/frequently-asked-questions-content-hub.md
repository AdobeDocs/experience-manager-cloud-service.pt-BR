---
title: Perguntas frequentes sobre o Content Hub
description: Obtenha respostas para algumas das perguntas mais frequentes do Centro de conteúdo.
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: cc29a94e4193f7563bb83ad39aa459ea0ba9306a
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 1%

---

# Perguntas frequentes sobre o Content Hub {#content-hub-frequently-asked-questions}

![Perguntas frequentes sobre a Content Hub](assets/content-hub-faqs.png)

## O que é o Content Hub? {#what-is-content-hub}

O Content Hub é um recurso do Adobe Experience Manager Assets as a Cloud Service.

O Content Hub permite que equipes maiores descubram facilmente ativos relevantes e aprovados por meio de um portal intuitivo e os adaptem rapidamente às suas necessidades.  Além disso, o Content Hub fornece um mecanismo de assimilação que permite que esses usuários realizem autoatendimento facilmente à medida que fazem upload de ativos para o DAM. Isso atende diretamente à necessidade que as organizações têm de maior velocidade de criação de conteúdo, preservando a consistência da marca e a conformidade com as salvaguardas apropriadas.

## Por que não posso ativar o Content Hub no meu programa/ambiente do Cloud Manager? {#cannot-enable-content-hub}

No momento, o Content Hub está disponível apenas nos programas de produção da AEM Cloud Manager, que incluem uma licença do Assets (Assets Cloud Service, Assets Ultimate, Assets Prime). Quando você clica em [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) para habilitá-lo, ele é implantado e associado ao ambiente de produção do autor do AEM nesse programa. Consulte [Implantar o Content Hub](/help/assets/deploy-content-hub.md) para obter detalhes e pré-requisitos.

## Eu ativei o Content Hub em meu programa/ambiente de produção. É possível desativá-lo? {#can-i-disable-content-hub}

Habilitar o Content Hub em um programa de produção o implanta como parte da infraestrutura de produção. A AEM Cloud Manager não permite remover ou desativar a infraestrutura de produção para minimizar o risco de uso da produção por erros humanos.

Se não quiser fornecer o Content Hub aos usuários após a implantação, não atribua nenhum usuário ao perfil de produto do Content Hub no Admin Console. Consulte [Implantar Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) para obter detalhes.

## Como posso avaliar o Content Hub na minha organização? {#how-can-i-evaluate-content-hub}

O Content Hub é um recurso que o Adobe fornece e mantém, e não tem nenhum código personalizado que exija validação típica via desenvolvimento/preparo/produção. Além disso, o acesso ao recurso para usuários é totalmente controlado pelo administrador, para que você possa avaliá-lo sem expô-lo a todos os usuários.

É possível avaliar o Content Hub sem afetar os usuários/conteúdos de produção gerenciados no AEM as a Cloud Service Assets. Um procedimento de avaliação pode ser semelhante a:

* [Habilitar o Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) no ambiente de produção (programa Cloud Manager)
* [Adicione um usuário Administrador do AEM](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) do autor de produção ao perfil de produto do Content Hub.
* O Administrador do AEM [configura o Content Hub](/help/assets/configure-content-hub-ui-options.md)
* O administrador do AEM ou um usuário do AEM no autor de produção do AEM [aprova vários ativos para o Content Hub](/help/assets/approve-assets-content-hub.md); se você não quiser alterar nenhum conteúdo de produção no DAM, poderá criar uma pasta de avaliação separada na instância de autor do AEM e carregar/marcar ou copiar alguns ativos do DAM para ele.
* O administrador do Admin Console adiciona [alguns usuários selecionados](/help/assets/deploy-content-hub.md#onboard-content-hub-users) ao perfil de produto do Content Hub, para que eles possam iniciar a avaliação.
* Após a conclusão da avaliação, os usuários do AEM na instância do autor podem remover a aprovação de ativos de teste, aprovar ativos de produção para o Content Hub e, em seguida, o administrador do Admin Console pode adicionar todos os usuários que precisam de acesso ao Content Hub e conteúdo aprovado. Parabéns, seu Content Hub está disponível agora.

Há um programa de acesso antecipado ao Content Hub em programas de sandbox e seus ambientes de produção de autor. Para obter mais informações, consulte [Introdução aos programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Para saber mais sobre o programa de acesso antecipado, entre em contato com a equipe de conta da Adobe.

## Por que não vejo nenhum ativo depois de fazer logon no Content Hub? {#no-assets-in-content-hub}

Os ativos marcados como aprovados no Assets as a Cloud Service estão automaticamente disponíveis no Content Hub. Se não conseguir ver nenhum ativo depois de fazer logon no Content Hub, aprove os ativos usando o ambiente de criação do AEM as a Cloud Service para disponibilizá-los no Content Hub. Para obter mais informações, consulte [Aprovar ativos para o Content Hub](/help/assets/approve-assets-content-hub.md).

## Por que não vejo meus ativos que carrego diretamente usando o Content Hub ou os importo de contas do Dropbox ou do OneDrive usando o Content Hub? {#no-assets-uploaded-from-content-hub}

A exibição de ativos carregados com o Content Hub depende de se você habilitou a opção [Aprovação automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub), disponível na interface do usuário de Configuração:

* Se a opção **Aprovação automática** estiver habilitada, os ativos carregados usando o Content Hub estarão automaticamente disponíveis.

* Se a opção **Aprovação automática** estiver desabilitada, os ativos carregados usando o Content Hub não serão exibidos automaticamente. Os ativos estão disponíveis na pasta `hydrated-assets` do seu ambiente do Assets as a Cloud Service. Navegue até a pasta e [edite em massa](/help/assets/approve-assets-content-hub.md) o status desses ativos para `Approved` para que eles sejam exibidos no Content Hub.

## Como localizar rapidamente ativos carregados usando o Content Hub no ambiente do AEM as a Cloud Service? {#find-uploaded-assets-on-aem-cloud}

Você pode encontrar rapidamente ativos carregados usando o Content Hub no ambiente do AEM as a Cloud Service ao:

1. Navegando até a pasta `hydrated-assets`.

1. Clicando em **[!UICONTROL Filtros]** e definindo **[!UICONTROL Sem status]** no campo **[!UICONTROL Status do ativo]**.

1. Classificando ativos usando o campo **[!UICONTROL Data de modificação]**.

## Por que não vejo a opção Editar usando o Adobe Express no meu cartão de ativos para remixar ativos e criar novas variações? {#edit-using-express-not-available}

Para exibir a opção **Editar usando o Adobe Express** no cartão de ativos, o usuário deve ter o direito Adobe Express Enterprise ou Teams (consulte [planos](https://www.adobe.com/express/pricing)), além de privilégios para [usuários do Content Hub com direitos de remixar ativos para novas variações](#onboard-content-hub-users-add-assets).

Existem algumas configurações de como os usuários são atribuídos ao [!DNL Content Hub] e [!DNL Adobe Express]:

1. A organização tem a licença [Assets Ultimate](/help/assets/assets-ultimate-overview.md) ou [Assets Prime](/help/assets/assets-prime.md), e o usuário está atribuído a um dos perfis do Experience Manager no Admin Console que incluem o direito ao Adobe Express (usuário colaborador ou avançado). A integração funciona sem nenhuma configuração adicional.

1. [!DNL Adobe Express] está implantado no mesmo [!DNL Adobe Admin Console] que [!DNL Experience Manager Assets] com [!DNL Content Hub]. A integração funciona sem nenhuma configuração adicional.

1. [!DNL Adobe Express] está implantado em um [!DNL Adobe Admin Console] diferente de [!DNL Experience Manager Assets] com [!DNL Content Hub]. Nesse caso, o administrador [!DNL Assets] pode configurar a integração (consulte [documentação](/help/assets/connect-assets-with-creative-cloud.md)) para que ela funcione.

   >[!NOTE]
   >
   >O usuário atribuído aos perfis de produto Express e Assets em dois Consoles do Administrador precisa ter o mesmo endereço de email e usar uma conta corporativa **Enterprise ou School**, e não a conta **Personal**. A configuração ideal é ter ambos os Admin Consoles configurados como **Federated ID** com uma relação de confiança configurada entre eles, para que o usuário tenha uma experiência de logon único contínua. Alguns dos planos do Express (por exemplo, Equipes do Express) não oferecem suporte ao Federated ID/logon único.

Além dos direitos de produto corretos, a integração do Adobe Express no Content Hub exige que o usuário atribuído tenha pelo menos [!UICONTROL Pode editar] permissões no ambiente de criação do Assets que viabiliza o Content Hub, em pelo menos **[!UICONTROL # /content/dam/hydroated-assets/]** hierarquia de pastas, onde os usuários do Content Hub podem salvar o conteúdo criado com o Express. Consulte [Gerenciamento de permissões](/help/security/touch-ui-principal-view.md) no modo de exibição de Administração (Interface para toque) ou um [gerenciamento de permissões simplificado no modo de exibição de Assets](https://experienceleague.adobe.com/pt-br/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

## Posso configurar o Content Hub para que as diretrizes de marca da minha organização sejam exibidas como um link na página inicial? {#content-hub-setup-brand-guidelines}

É possível adicionar links personalizados como guias separadas, além das guias padrão Todos os Assets, Coleções e Insights na página inicial do Content Hub. Para obter informações sobre como configurá-lo, consulte [Links Personalizados](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## Há algum plano para migrar os clientes existentes do Brand Portal para o Content Hub? {#migration-brand-portal}

O Adobe oferece suporte à migração do Brand Portal para o Content Hub, que pode ser usado ao criar um tíquete de suporte do Adobe.

## Por que não consigo ver a opção Configurações/configurações do produto no Content Hub? {#ui-configuration-option-missing}

Para acessar a [Interface do Usuário de Configuração](/help/assets/configure-content-hub-ui-options.md), você precisa ser um [Administrador do Content Hub](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator). Se você estiver atribuído ao perfil de produto Administradores do AEM na instância do autor de produção no Adobe Admin Console e ainda não conseguir ver a opção de configuração, verifique se o perfil de produto Administradores do AEM não está renomeado. Consulte [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) para obter mais detalhes.

## Como o Content Hub aborda as limitações do Brand Portal? {#content-hub-brand-portal-comparison}


A tabela abaixo descreve as principais diferenças entre as duas soluções:

| Área | Recurso | Centro de conteúdo | Brand Portal |
|---|---|----|----|
| Configuração da experiência de distribuição | Configurar metadados para filtros, detalhes do ativo e adicionar a página de ativos | ✓ | − |
|  | Configurar links externos a partir do portal | ✓ | − |
|  | Configurar mensagens do banner | ✓ | ✓ |
|  | Configurar imagem de banner para identidade visual | ✓ | ✓ |
|  | Configurar as cores primária e secundária para a interface do usuário de acordo com os requisitos de marca | ✓ | − |
| Compartilhamento de ativos do DAM | Compartilhamento de ativos originais aprovados do DAM | ✓ | ✓ |
|  | Alterações aprovadas no ativo sincronizadas automaticamente | ✓ | − |
| Pesquisa e filtros | Filtros dinâmicos (opções são exibidas dinamicamente com base nos ativos exibidos) | ✓ | − |
|  | Pesquisar histórico | ✓ | − |
| Upload de ativo | Unidade local | ✓ | ✓ |
|  | Adicionar metadados configuráveis ao carregar ativos | ✓ | − |
| Download e representações | Baixar ativo original | ✓ | ✓ |
|  | Compartilhar e baixar representações estáticas do DAM | ✓ | ✓ |
|  | Baixar representações dinâmicas (predefinição e cortes inteligentes) | ✓ | ✓ |
|  | Capacidade de restringir a exibição e o download de ativos expirados | ✓ | − |
| Compartilhamento de link e coleções | Compartilhamento de links para usuários conectados | ✓ | ✓ |
|  | Coleções públicas | ✓ | ✓ |
|  | Pesquisar em coleções | ✓ | − |
|  | Compartilhamento de link anônimo | ✓ | ✓ |
|  | Coleções privadas | ✓ | ✓ |
| Permissões | Permissões baseadas em ACL | − | ✓ |
|  | Controle de acesso baseado em atributos | ✓ | − |
| Integração expressa | Editar o Content Hub Assets no Adobe Express e salvar no DAM | ✓ | − |
| Painéis e relatórios | Painel de insights | ✓ | − |
| Extensibilidade da interface | Pontos de extensão personalizados na página de detalhes do ativo | Disponibilidade limitada | − |
| Inovações em breve | Coleções favoritas por usuário | ✓ | − |
|  | Coleções fixadas pelo administrador | ✓ | − |
|  | Pesquisa semântica | ✓ | − |
|  | Pesquisa localizada e exibição de metadados | ✓ | − |

## Como posso selecionar um repositório para exibir ativos somente do ambiente selecionado? {#select-repository-multiple-environments}

Ao configurar o Content Hub para Produção e outros ambientes inferiores para o mesmo Programa, você pode selecionar o repositório e exibir os ativos do ambiente selecionado. Execute as seguintes etapas:

1. Clique no ícone do usuário no painel direito.

1. Na seção **[!UICONTROL Configurações do Produto]**, selecione **[!UICONTROL Selecionar Repositório]**.

1. Selecione o repositório no menu suspenso **[!UICONTROL Repositório]** e clique em **[!UICONTROL OK]** para confirmar.

   O Content Hub agora exibe ativos para o ambiente selecionado.

## Como o Content Hub pode exibir a pré-visualização em miniatura do tipo de arquivo .ZIP? {#thumbnail-preview-zip-file}

Para fornecer uma pré-visualização de miniatura para tipos de arquivo, como .ZIP no Content Hub, você pode adicionar uma representação chamada `cq5dam.preview.jpg` ou `cq5dam.preview.png` à raiz do caminho onde o .ZIP está disponível no ambiente de criação do AEM as a Cloud Service.

A imagem que você adiciona como representação:

* Pode estar no formato JPG, JPEG ou PNG.

* Deve ter menos de 50 MB

Quando disponível, o Content Hub exibe a imagem como a miniatura de visualização do arquivo .ZIP no Content Hub.


