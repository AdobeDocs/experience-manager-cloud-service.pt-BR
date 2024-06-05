---
title: Criação de programas de produção
description: Saiba como usar o Cloud Manager para criar seu próprio programa de produção para hospedar o tráfego direto.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 34%

---


# Criação de programas de produção {#create-production-program}

Um programa de produção deve ser usado por um usuário familiarizado com o AEM e o Cloud Manager e que está pronto para começar a gravar, compilar e testar o código com o objetivo de implantá-lo para hospedar o tráfego direto.

Saiba mais sobre os tipos de programas no documento [Noções sobre programas e tipos de programas.](program-types.md)

## Criação de um programa de produção {#create}

Siga estas etapas para criar um programa de produção. Observe que, dependendo dos direitos da organização, você pode ver [opções adicionais](#options) ao adicionar seu programa.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)** toque ou clique em **Adicionar programa** no canto superior direito da tela.

   ![Página de aterrissagem do Cloud Manager](assets/log-in.png)

1. Selecione **Configurar para produção** no assistente Criar programa para criar um programa de produção e fornecer um nome de programa.

   ![Assistente de criação de programa](assets/create-production-program.png)

1. Ou é possível adicionar uma imagem ao programa arrastando e soltando um arquivo de imagem no público alvo **Adicionar uma imagem de programa** ou clicando nela para selecionar uma imagem de um navegador de arquivos. Selecionar **Continuar**.

1. Na guia **Soluções e complementos**, selecione as soluções a serem incluídas no programa.

   * Se você não tiver certeza se precisa de um ou mais programas para as várias soluções disponíveis, selecione o mais interessante. Você pode ativar soluções adicionais ao [editar o programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) depois. Consulte a [Introdução ao documento Programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obter mais recomendações de configuração do programa.
   * Pelo menos uma solução é necessária para a criação do programa.
   * Se você selecionou a variável **[Ativar Segurança aprimorada](#security)** , você poderá selecionar somente as soluções para as quais houver direitos HIPAA disponíveis.

   ![Selecionar soluções](assets/setup-prod-select.png)

1. Clique na divisa antes dos nomes de solução para exibir os complementos opcionais, como selecionar o **Commerce** opção complementar em **Sites**.

   ![Selecionar complementos](assets/setup-prod-commerce.png)

1. Com as soluções e os complementos selecionados, clique em **Continuar**.

1. Na guia **Data de publicação**, insira a data em que planeja publicar o programa de produção.

   ![Definir data de publicação planejada](assets/set-up-go-live.png)

   * Essa data poderá ser editada a qualquer momento.
   * Essa data é somente para fins informativos e aciona o widget de ativação na [**Visão geral do programa** página](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) para fornecer links no produto para a documentação de práticas recomendadas as a Cloud Service do AEM em tempo hábil, a fim de se alinhar à sua jornada, resultando em uma experiência de ativação bem-sucedida e tranquila.

1. Clique em **Criar**.

Seu programa é criado pelo Cloud Manager e é exibido e pode ser selecionado na página de aterrissagem.

![Visão geral do Cloud Manager](assets/navigate-cm.png)

## Opções adicionais do programa de produção {#options}

Dependendo dos direitos disponíveis para sua organização, talvez você tenha opções adicionais disponíveis ao criar um programa de produção.

### Segurança {#security}

Se você tiver os direitos necessários, a variável **Segurança** será exibida como a primeira guia no **Configurar para produção** diálogo.

A variável **Segurança** fornece as opções para ativar **HIPAA** e/ou **Proteção WAF-DDOS** para seu programa de produção.

O Adobe HIPAA Compliant e o Web Application Firewall (WAF) facilitam a segurança baseada em nuvem como parte de uma abordagem de várias camadas para proteção contra vulnerabilidades.

* **HIPAA** - Essa opção habilita a implementação da solução Adobe pronta para HIPPA.
   * [Saiba mais](https://www.adobe.com/go/hipaa-ready) sobre a solução de implementação pronta para HIPAA da Adobe.
   * O HIPAA não pode ser habilitado ou desabilitado após a criação do programa.
* **Proteção WAF-DDOS** - Essa opção habilita o firewall do aplicativo web por meio de regras para proteger seu aplicativo.
   * Uma vez ativada, a proteção WAF-DDOS pode ser configurada configurando um [pipeline de não produção.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * Consulte o documento [Regras de filtro de tráfego incluindo regras WAF](/help/security/traffic-filter-rules-including-waf.md) para saber como gerenciar regras de filtro de tráfego no repositório para que elas sejam implantadas corretamente.

![Opções de segurança](assets/create-production-program-security.png)

### SLA {#sla}

Se você tiver os direitos necessários, a variável **SLA** será exibida como a segunda ou terceira guia no **Configurar para produção** diálogo.

A AEM Sites oferece um contrato de nível de serviço (SLA) padrão de 99,9%. A variável **Contrato de nível de serviço de 99,99%** permite uma porcentagem mínima de tempo de atividade de 99,99% em seus ambientes de produção.

99,99% do SLA oferece benefícios, incluindo maior disponibilidade e menor latência, e requer um [região de publicação adicional](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) a ser aplicado ao ambiente de produção no programa.

![Opções de SLA](assets/create-production-program-sla.png)

Quando a variável [requisitos](#sla-requirements) para habilitar 99,99% SLA são atendidos, você deve executar um [pipeline de pilha completa](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para ativá-la.

#### Requisitos para 99,99% do SLA {#sla-requirements}

Além dos direitos exigidos, 99,99% do SLA tem requisitos adicionais para uso.

* Tanto o SLA de 99,99% quanto os direitos de região de publicação adicionais devem estar disponíveis para a organização no momento de aplicar o SLA de 99,99% ao programa.
* Para aplicar o SLA de 99,99% ao programa, o Cloud Manager verificará se um item não consumido [região de publicação adicional](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) também está disponível e pode ser aplicado ao programa.
* Ao editar um programa, se ele já contiver um ambiente de produção com pelo menos uma região de publicação adicional, o Cloud Manager verificará apenas a disponibilidade de um direito de SLA de 99,99%.
* Para que o SLA de 99,99% e os relatórios sejam ativados, o [ambiente de produção/preparo](/help/implementing/cloud-manager/manage-environments.md#adding-environments) deve ter sido criada e pelo menos uma região de publicação adicional deve ter sido aplicada no ambiente de produção/preparo.
   * Se estiver usando [rede avançada,](/help/security/configuring-advanced-networking.md) verifique a [Adicionando várias regiões de publicação a um novo ambiente](/help/implementing/cloud-manager/manage-environments.md#adding-regions) documento para obter recomendações para que a conectividade seja mantida em caso de falha regional.
* Pelo menos uma região de publicação adicional deve permanecer em seu programa de SLA de 99,99%. Os usuários não têm permissão para excluir a última região de publicação adicional do seu programa de SLA de 99,99%.
* O SLA de 99,99% é compatível com programas de produção que têm a solução do Sites ativada.
* Você deve executar um [pipeline de pilha completa](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para ativar (ou desativar ao editar um programa) o SLA de 99,99%.

## Acessar o programa {#accessing}

1. Ao ver o cartão do programa na página de aterrissagem, selecione o botão de reticências para exibir as opções de menu disponíveis.

   ![Visão geral do programa](assets/program-overview.png)

1. Selecione **Visão geral do programa** para navegar até a página **Visão geral**.

1. O principal cartão de chamada à ação na página de visão geral orientará você pela criação de um ambiente, um pipeline de não produção e, finalmente, um pipeline de produção.

   ![Visão geral do programa](assets/set-up-prod5.png)

>[!TIP]
>
>Consulte o documento [Navegação na interface do usuário do Cloud Manager](/help/implementing/cloud-manager/navigation.md) para obter detalhes sobre como navegar no Cloud Manager e entender o **Meus programas** console.

>[!NOTE]
>
>Diferentemente de um [programa de sandbox,](introduction-sandbox-programs.md#auto-creation) um programa de produção exigirá que um usuário com a função apropriada do Cloud Manager crie o projeto e adicione um ambiente por meio da interface de usuário de autoatendimento.
