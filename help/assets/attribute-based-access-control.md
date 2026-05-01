---
title: Controle de acesso baseado em atributos
description: Saiba como habilitar o controle de acesso baseado em atributos para definir regras baseadas em metadados e definir o nível de acesso aos ativos disponíveis no Content Hub
role: Admin
badgeSaas: label="AEM Assets" type="Positive" tooltip="Aplicável ao AEM Assets)."
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: b736af556c8580d005097c27cceba050b21a57c9
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 0%

---


# Controle de acesso baseado em atributos {#attribute-based-access-control}

O controle de acesso baseado em atributos (ABAC) permite que os administradores do Content Hub definam regras baseadas em metadados para controlar o nível de acesso aos ativos disponíveis no Content Hub.

Os administradores de uma organização definem regras para grupos de usuários, que são mapeados para uma ID de grupo. As regras são uma combinação de [operadores lógicos e de comparação](#supported-rule-constructs), e os administradores podem definir quantas regras forem necessárias para gerenciar o acesso aos ativos no Content Hub.

As regras se baseiam em metadados. Se as condições definidas em uma regra corresponderem aos metadados do ativo, o ativo será exibido para o grupo de usuários. O Content Hub verifica os metadados do ativo, incluindo os metadados personalizados, de todos os ativos disponíveis em **Todas as Assets** e **Coleções** para exibir os resultados aos grupos de usuários.

Por exemplo, PERMITA o acesso a um grupo de usuários com ID de grupo = 1011 quando os metadados do ativo corresponderem &quot;Marca = Marca X&quot; E &quot;Região = EMEA OU Américas&quot;. O Content Hub exibe somente esses ativos para o grupo de usuários com ID = 1011, onde &#39;&#39;Marca = Marca X&#39;&#39; e &#39;&#39;Região = EMEA ou Américas&#39;&#39;.

As regras ABAC no Content Hub podem ser configuradas usando as seguintes abordagens:

* **Configuração de autoatendimento** usando o [Assistente de IA no Content Hub](#configure-abac-using-ai-assistant-in-content-hub), habilitado pelo AEM Governance Agent
* **Configuração baseada em planilha** por meio do [Suporte da Adobe](#configure-abac-using-spreadsheet)

Com o AI Assistant no Content Hub, os administradores podem definir e gerenciar regras do ABAC usando metadados e linguagem natural. Isso permite uma configuração de regra mais rápida e reduz a dependência de workflows de suporte manuais.

Alguns dos principais benefícios do controle de acesso baseado em atributos incluem:

* Elimina a dependência da estrutura de pastas para permissões
* Permite que os administradores façam upload de ativos e determinem retroativamente as estruturas de permissão
* Reduz o número de duplicatas e melhora a integridade do ativo. São necessárias duplicatas em permissões baseadas em pastas quando os mesmos ativos são compartilhados com grupos diferentes.
* Permite acesso granular baseado em regras
* Suporta governança escalável entre marcas e regiões
* Melhora o gerenciamento de ativos

>[!VIDEO](https://video.tv.adobe.com/v/3475413/?learn=on&enablevpops){transcript=true}

## Como ativar o controle de acesso baseado em atributos {#enable-attribute-based-access-control}

As regras ABAC no Content Hub podem ser configuradas usando as seguintes abordagens:

* **Configuração de autoatendimento usando o Assistente de IA no Content Hub (viabilizada pelo AEM Governance Agent)**\
  Os administradores podem definir e gerenciar regras ABAC diretamente usando linguagem natural no Content Hub.

* **Configuração baseada em planilha via Suporte da Adobe**\
  Os administradores podem definir regras ABAC em uma planilha e enviá-las por meio do Suporte da Adobe para configuração.

## Configure o ABAC usando o Assistente de IA no Content Hub

Com o Assistente de IA no Content Hub, viabilizado pelo AEM Governance Agent, você pode criar e gerenciar regras ABAC diretamente no Content Hub, usando linguagem natural.

É possível:
* Pesquisar regras existentes
* Criar regras
* Atualizar regras
* Excluir regras

Isso permite que os administradores criem e gerenciem regras de acesso sem depender de fluxos de trabalho de suporte.

### Antes de começar {#before-you-begin-ai-assistant}

Verifique o seguinte antes de usar o Assistente de IA na configuração da regra ABAC do Content Hub:

* Você está licenciado para o AEM as a Cloud Service
* O Assistente de IA ativado pelo AEM Governance Agent está disponível para sua organização
* Se você ainda não tiver acesso, entre em contato com o representante da Adobe e conclua as etapas de licenciamento necessárias
* Um GenAI Rider não é necessário para o programa try-buy

### Etapas para configurar regras ABAC usando o Assistente de IA {#steps-ai-assistant}

1. Abra o Assistente de IA no Content Hub.

1. Comece com uma instrução simples.

   Por exemplo:

   `Create a new rule in Content Hub`

   O Assistente de IA orienta você sobre as informações necessárias para criar a regra.

1. Defina a regra no idioma natural.

   Por exemplo:

   `Frescopa Web Marketers user group should have access to assets where product equals Frescopa`

1. Selecione o ambiente onde a regra ABAC deve ser aplicada.

1. Revise a regra antes de aplicá-la.

   O Assistente de IA gera uma visualização estruturada da regra. Nada é aplicado automaticamente. Você pode revisar a regra gerada, ajustá-la se necessário ou cancelar a ação antes de aplicá-la.

1. Salve e aplique a regra.

   Depois de salva, a regra é aplicada dinamicamente com base em metadados.

Essa etapa de revisão ajuda a garantir a precisão antes que a regra seja aplicada.

### Gerenciar regras ABAC usando prompts {#manage-abac-rules-using-prompts}

Depois de começar a usar o Assistente de IA, você pode gerenciar as regras ABAC de forma conversacional.

**Descobrir regras**

* Mostrar todas as regras ABAC existentes do Content Hub

**Criar regras**

* Crie uma regra que conceda ao Grupo de marketing do produto acesso a todos os ativos
* Conceder acesso ao grupo de Vendas a ativos em que a região é igual a EMEA

**Atualizar regras**

* Atualizar regra para que o grupo de marketing EMEA inclua APAC

**Excluir regras**

* Excluir a regra do grupo de Marketing do Produto

**Explorar metadados e grupos**

* Mostrar grupos e propriedades de metadados disponíveis para definir regras

## Configurar o ABAC usando planilha

Se o Assistente de IA não estiver ativado para sua organização, você poderá configurar regras ABAC usando o fluxo de trabalho baseado em planilhas.

Clique em **Baixar planilha** para baixar e definir regras em uma planilha. Crie um tíquete de Suporte do Adobe e forneça as regras definidas na planilha ao Adobe.

[!BADGE Baixar Planilha]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}

Defina as regras na planilha usando as diretrizes descritas neste artigo.

>[!IMPORTANT]
>
>Depois de definir as regras, navegue até a guia **Erros de Validação** da planilha e clique em **Executar Validações ABAC**. A mensagem **Todas as validações aprovadas** confirma que você pode fornecer as regras definidas para a Adobe.

### Etapas para configurar regras ABAC usando Planilha {#steps-spreadsheet}

1. Baixe o modelo da planilha ABAC.
1. Defina regras na planilha usando condições baseadas em metadados.
1. Mapeie cada regra para a ID de grupo IMS apropriada.
1. Capture a intenção de negócios da regra nos comentários.
1. Envie um tíquete de Suporte da Adobe e compartilhe a planilha preenchida com a Adobe.
1. O Adobe configura as regras para sua organização.

## Exemplo de caso de uso de controle de acesso baseado em atributos {#example-metadata-based-rules}

Para oferecer suporte a uma implantação de marketing em grande escala, vários membros da equipe em várias regiões e marcas precisam de acesso a ativos digitais. Cada persona tem um escopo específico com base na região e na marca. O ABAC aplica essas regras automaticamente usando metadados de ativos. A tabela a seguir ilustra os perfis para esse caso de uso e as regras aplicadas:

| Perfil | Função | Descrição da função | ID do grupo | Regra ABAC |
|---|---|---|---|---|
| John | Líder de marketing EMEA | Supervisiona a execução de marketing em todas as marcas na EMEA. Precisa de acesso a ativos aprovados para todas as marcas destinadas aos mercados EMEA. | group-emea-marketing | region = &quot;EMEA&quot; |
| Mike | Líder de marketing da APAC | Supervisiona a execução de marketing em todas as marcas na APAC. Precisa de acesso a ativos aprovados para todas as marcas destinadas aos mercados da APAC. | group-apac-marketing | region = &quot;APAC&quot; |
| Sophie | Gerente da Marca X (EMEA) | Gerencia a identidade da Marca X na Europa, no Oriente Médio e na África. Precisa ver somente conteúdo aprovado pela Marca X adaptado aos mercados da EMEA. | group-emea-brandx | region = &quot;EMEA&quot; &amp;&amp; brand = &quot;Brand X&quot; |
| Tom | Gerenciador da Marca Y (APAC) | Gerencia a identidade da Marca Y na APAC. Precisa ver somente o conteúdo aprovado pela Marca Y personalizado para os mercados da APAC. | group-apac-brandy | region = &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

Usando essas regras, os administradores do Content Hub têm:

* **Acesso granular baseado em regras**: os usuários veem somente os ativos relevantes para sua região e marca, sem atribuições de permissão manuais.
* **Colaboração global ininterrupta**: as equipes regionais e de marcas trabalham em paralelo, sem conflitos de acesso.
* **Permissões escalonáveis e que não se tornarão obsoletas**: à medida que novas regiões ou marcas são adicionadas, as regras podem ser atualizadas com base em metadados.

### Cenários adicionais em que o ABAC é útil {#additional-scenarios-abac}

O ABAC também pode ajudar a resolver os seguintes cenários:

* **Marca global e acesso regional**: as equipes veem somente ativos relevantes para sua marca e mercado.
* **Colaboração de agência e parceiro**: agências externas e parceiros podem acessar somente os ativos de campanha relevantes para eles.
* **Acesso com base em funções para equipes diferentes**: equipes como de marketing, vendas e jurídico podem acessar ativos relevantes para sua função.
* **Conformidade legal específica da região**: os usuários podem ser restritos a ativos aprovados para requisitos regulatórios ou regionais específicos.

>[!IMPORTANT]
>
>Por padrão, o acesso é negado a todos os outros grupos de usuários que não estão especificados com nenhuma regra na [planilha](#configure-abac-spreadsheet). Se um usuário não fizer parte de nenhum grupo para o qual as regras ABAC estão definidas, não poderá acessar nenhum ativo. Se alguns usuários precisarem ter acesso a todos os ativos, por exemplo, Administradores, inclua um grupo com uma ID de grupo na planilha e especifique que o grupo requer acesso a todos os ativos para que o Adobe possa configurá-lo adequadamente.

## Construtores de regra compatíveis {#supported-rule-constructs}

* **Operadores lógicos**:
   * AND: todas as condições devem ser verdadeiras
   * OU: pelo menos uma condição deve ser verdadeira

* **Operadores de comparação**:
   * Igual a (=): verifica se um atributo de usuário ou ativo corresponde a um valor
   * Diferente de (!=): verifica se um usuário ou atributo de ativo não corresponde a um valor

Quando os campos de metadados de ativos contêm matrizes, por exemplo, várias regiões ou tags, &quot;Igual&quot; refere-se a contém lógica e &quot;Diferente de&quot; refere-se a não contém lógica.

Isso permite escrever regras simples e expressivas, como ALLOW if region = emea AND assetType != prototype AND tags != confidencial.

## Diretrizes {#guidelines-attribute-based-access-control}

As diretrizes a seguir se aplicam à configuração baseada no Assistente de IA e na planilha:

* As regras ABAC são aplicáveis somente a ativos aprovados para o Content Hub. Para obter mais informações, consulte [Aprovar Assets para Content Hub](/help/assets/approve-assets-content-hub.md).
* Não definir regras de NEGAÇÃO. Sempre converter regras de NEGAÇÃO em regras DE PERMISSÃO. Por exemplo, ALLOW se região = user-region DENY se assetType = prototype AND confidencial = yes pode ser convertido para ALLOW se região = user-region AND (assetType != prototype OR confidencial != yes).
* As regras ABAC são aplicadas a grupos de usuários usando a ID de grupo IMS, que está disponível no Admin Console.
* Você pode definir o [Destino de aprovação](/help/assets/approve-assets-content-hub.md#set-approval-target) para ativos usando o ambiente de autor do AEM as a Cloud Service. As regras ABAC são aplicadas a ativos aprovados com Approval Target = Content Hub, já que Approval Target = Delivery é para ativos disponíveis para Delivery + Content Hub. Assets marcado como destino de aprovação = Entrega estão visíveis para todos no Content Hub.
* Verifique se os esquemas de metadados usados nas regras ABAC estão corretamente definidos e disponíveis no AEM. Forneça o caminho completo do esquema ou esquemas de metadados na AEM que definem as propriedades referenciadas nas regras ABAC. Opcionalmente, é possível criar uma pasta de teste com ativos de amostra que correspondam às condições ABAC para ajudar a verificar o comportamento da regra e avaliar o acesso com precisão.
* Capture a intenção de negócios da regra nos comentários, mesmo que a condição seja gravada corretamente, pois a intenção ajuda a validar e corrigir a lógica, se necessário.
* Garantir que os valores de metadados usados para as regras de acesso, como marca, região e produto, sejam mantidos de forma consistente em todos os ativos.
* Comece com os principais casos de uso, como acesso baseado em marca ou região.
* Use avisos claros ao definir regras com o Assistente de IA. Descreva a intenção no idioma comercial para que o Assistente do AI possa traduzi-la em uma regra estruturada.
* Os arquivos de licença do PDF definidos para DRM devem permanecer visíveis para todos os usuários para que eles possam revisar as informações de licença ao baixar o ativo com a licença.

## Perguntas frequentes {#faqs-attribute-based-access-control-content-hub}

### O que é o ABAC (Attribute-based Access Control, controle de acesso baseado em atributos) no AEM Assets Content Hub?

O controle de acesso baseado em atributos (ABAC) no AEM Assets Content Hub permite que os administradores definam regras baseadas em metadados para controlar o nível de acesso que diferentes grupos de usuários têm aos ativos digitais. O acesso é determinado se os metadados do ativo correspondem às condições especificadas nas regras, permitindo o gerenciamento granular e dinâmico da visibilidade do ativo.

### Como os administradores definem as regras de acesso usando o ABAC no AEM Assets Content Hub?

Os administradores definem regras de acesso criando condições com base nos metadados do ativo, como marca ou região, e vinculando-os a IDs específicas do grupo de usuários. Essas regras usam operadores lógicos e de comparação para especificar exatamente quais ativos estão visíveis para quais grupos de usuários.

### Quais são os principais benefícios de usar o ABAC em relação às permissões tradicionais baseadas em pastas no AEM Assets Content Hub?

O ABAC elimina a dependência de estruturas de pastas para permissões, permite que os administradores façam upload de ativos e atribuam permissões retroativamente e reduz o número de ativos duplicados necessários. Isso melhora a integridade do ativo e simplifica o gerenciamento de permissões, especialmente quando os ativos precisam ser compartilhados com vários grupos.

### Os administradores podem configurar regras ABAC diretamente na interface do AEM Assets Content Hub?

Os administradores podem configurar regras ABAC usando o Assistente de IA no Content Hub, se habilitado para sua organização. Eles também podem continuar a usar o fluxo de trabalho com base em planilhas por meio do Suporte da Adobe.

### Que tipos de condições de metadados podem ser usadas ao configurar regras ABAC no AEM Assets Content Hub?

As regras ABAC no AEM Assets Content Hub podem usar operadores lógicos, como AND e OR, e operadores de comparação, como &quot;é igual&quot; e não &quot;é igual&quot;. As propriedades de metadados usadas nas regras devem ser corretamente definidas e disponibilizadas nos esquemas de metadados do AEM, e podem incluir campos como região, marca, produto, campanha, tipo de ativo ou status de publicação.

### Por que o AEM Assets Content Hub ABAC é particularmente útil para organizações com grandes equipes e diversas necessidades de ativos?

O ABAC é útil para organizações com equipes grandes, pois permite acesso granular e baseado em regras a ativos com base em funções de usuário, regiões, marcas ou necessidades comerciais. Ele garante que os usuários vejam apenas os ativos relevantes para suas responsabilidades, sem atribuições de permissão manuais ou duplicação excessiva de ativos.

### Como os administradores devem preparar a planilha ABAC para o AEM Assets Content Hub antes de enviá-la para o Suporte da Adobe?

Os administradores devem criar grupos de usuários na Adobe Admin Console, anotar suas IDs de grupo, definir claramente as permissões e condições para cada grupo na planilha, garantir que todas as propriedades de metadados sejam mapeadas corretamente para os esquemas apropriados e usar a coluna de comentários para esclarecer a intenção de negócios de cada regra.