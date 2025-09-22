---
title: Controle de acesso baseado em atributos
description: Saiba como habilitar o controle de acesso baseado em atributos para definir regras baseadas em metadados e definir o nível de acesso aos ativos disponíveis no Content Hub
role: Admin
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: 0833e31d37c473d37e16ee037823e61611622322
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Controle de acesso baseado em atributos {#attribute-based-access-control}

O controle de acesso baseado em atributos (ABAC) permite que os administradores do Content Hub definam regras baseadas em metadados para definir o nível de acesso aos ativos disponíveis no Content Hub.

Os administradores de uma organização definem regras para grupos de usuários, que são mapeados para uma ID de grupo. As regras são uma combinação de [operadores lógicos e de comparação](#supported-rule-constructs), e os administradores podem definir quantas regras precisarem para gerenciar o acesso aos ativos no Content Hub.

As regras se baseiam em metadados e se as condições definidas na regra corresponderem aos metadados do ativo, o ativo será exibido para o grupo de usuários. O Content Hub verifica os metadados do ativo, incluindo os metadados personalizados de todos os ativos disponíveis em **Todas as Assets** e **Coleções** para exibir os resultados aos grupos de usuários.

Por exemplo, PERMITA acesso ao grupo de usuários com ID de grupo = 1011, quando os metadados do ativo corresponderem a &quot;Marca = Marca X&quot; E &quot;Região = EMEA OU Américas&quot;. O Content Hub exibe somente esses ativos para o grupo de usuários com ID = 1011 onde Marca = `Brand X` e Região = `EMEA` ou `Americas`.

Alguns dos principais benefícios do controle de acesso baseado em atributos incluem:

* Elimina a dependência da estrutura de pastas para permissões

* Permite que os administradores façam upload de ativos e determinem retroativamente as estruturas de permissão

* Reduz o número de duplicatas - melhora a integridade do ativo. São necessárias duplicatas em permissões baseadas em pastas quando os mesmos ativos são compartilhados com grupos diferentes.

## Como ativar o controle de acesso baseado em atributos? {#enable-attribute-based-access-control}

A partir de agora, você não poderá criar regras de controle de acesso baseadas em atributos por conta própria usando a Interface do usuário do Content Hub.

Clique em **Baixar planilha** para baixar e definir regras em uma planilha. Crie um tíquete de suporte do Adobe e forneça as regras definidas na planilha ao Adobe.

[!BADGE Baixar Planilha]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}


Defina as regras na planilha usando as diretrizes definidas neste artigo.

>[!IMPORTANT]
>
> Depois de definir as regras, navegue até a guia **Erros de Validação** da planilha e clique em **Executar Validações ABAC**. **Todas as validações transmitidas** confirmam que você pode fornecer as regras definidas para a Adobe.

## Exemplo de caso de uso de Controle de acesso baseado em atributo {#example-metadata-based-rules}

Para oferecer suporte a uma implantação de marketing em grande escala, vários membros da equipe em várias regiões e marcas precisam de acesso a ativos digitais. Cada persona tem um escopo específico com base na região e na marca. O ABAC aplica essas regras automaticamente por meio dos metadados do ativo. A tabela a seguir ilustra os diferentes tipos de personalidades para esse caso de uso e as regras aplicadas:

| Perfil | Função | Descrição da função | ID do grupo | Regra ABAC |
|---------------------|----------------|-----------------|------------|------------|
| John | Líder de marketing EMEA | Supervisiona a execução de marketing em todas as marcas na EMEA. Precisa de acesso a ativos aprovados para todas as marcas destinadas aos mercados EMEA. | group-emea-marketing | region = &quot;EMEA&quot; |
| Mike | Líder de marketing da APAC | Supervisiona a execução de marketing em todas as marcas na APAC. Precisa de acesso a ativos aprovados para todas as marcas destinadas aos mercados da APAC. | group-apac-marketing | region = &quot;APAC&quot; |
| Sophie | Gerente da Marca X (EMEA) | Gerencia a identidade da Marca X na Europa, no Oriente Médio e na África. Precisa ver somente conteúdo aprovado pela Marca X adaptado aos mercados da EMEA. | group-emea-brandx | region = &quot;EMEA&quot; &amp;&amp; brand = &quot;Brand X&quot; |
| Tom | Gerenciador da Marca Y (APAC) | Gerencia a identidade da Marca Y na APAC. Precisa ver somente o conteúdo aprovado pela Marca Y personalizado para os mercados da APAC. | group-apac-brandy | region = &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

Usando essas regras, os administradores do Content Hub têm:

* **Acesso granular baseado em regras**: os usuários veem somente os ativos relevantes para sua região e marca, sem atribuições de permissão manuais.

* **Colaboração global ininterrupta**: as equipes regionais e de marcas trabalharam em paralelo, sem conflitos de acesso.

* **Permissões escalonáveis e que não se tornarão obsoletas**: à medida que novas regiões ou marcas são adicionadas, as regras podem ser atualizadas com base em metadados.

>[!IMPORTANT]
>
> Por padrão, o acesso é negado a todos os outros grupos de usuários, que não estão especificados com nenhuma regra na [planilha](#enable-attribute-based-access-control). Se um usuário não fizer parte de nenhum grupo para o qual as regras ABAC estão definidas, não será possível acessar nenhum ativo. Se alguns usuários precisarem ter acesso a todos os ativos (por exemplo, Administradores), um grupo com uma ID de grupo deverá ser mencionado na planilha com os detalhes de que esse grupo específico precisa acessar todos os ativos, e o Adobe irá configurá-lo para você.


## Construtores de regra compatíveis {#supported-rule-constructs}

* **Operadores lógicos**:
   * AND: todas as condições devem ser verdadeiras
   * OU: pelo menos uma condição deve ser verdadeira
* **Operadores de comparação**:
   * Igual a (=): verifica se um atributo de usuário ou ativo corresponde a um valor
   * Não é igual a (!=): verifica se um atributo de usuário ou ativo não corresponde a um valor

Quando os campos de metadados de ativos contêm matrizes (por exemplo, várias regiões ou marcas), `Equals` refere-se à lógica `contains` e `Not Equals` refere-se à lógica `does not contain`.

Isso permite escrever regras simples e expressivas, como: ALLOW if region = emea AND assetType != prototype AND tags != confidencial.

## Diretrizes {#guidelines-attribute-based-access-control}

* As regras ABAC são aplicáveis somente a ativos aprovados para o Content Hub. Para obter mais informações, consulte [Aprovar Assets para Content Hub](/help/assets/approve-assets-content-hub.md).

* Não forneça regras de NEGAÇÃO. Em vez disso, sempre converta NEGAR em regra DE PERMISSÃO. Por exemplo, `ALLOW if region = <user-region> DENY if assetType = prototype AND confidential = yes` pode ser convertido para `ALLOW if region = <user-region> AND (assetType != prototype OR confidential != yes)`.

* As regras ABAC são aplicadas a grupos de usuários usando a ID de grupo IMS, que está disponível no Admin Console.


* Você pode definir o [Destino de aprovação](/help/assets/approve-assets-content-hub.md#set-approval-target) para ativos usando o ambiente de autor do AEM as a Cloud Service. As regras ABAC são aplicadas a ativos aprovados com Destino de Aprovação = `Content Hub`, pois o Destino de Aprovação = `Delivery` é para ativos disponíveis para `Delivery` + `Content Hub`. Assets marcados como Destino de Aprovação = `Delivery` estão visíveis para todos no Hub de conteúdo.

* Verifique se os esquemas de metadados usados nas regras ABAC estão corretamente definidos e disponíveis no AEM. Forneça o caminho completo dos esquemas de metadados no AEM que definem as propriedades referenciadas nas regras ABAC. Opcionalmente, é possível criar uma pasta de teste com alguns ativos de amostra com valores de metadados que correspondam às condições ABAC. Isso ajuda a verificar o comportamento da regra e avaliar o acesso com precisão.

* Capture a intenção de negócios da regra no comentário, independentemente da condição ter sido gravada corretamente, pois a intenção nos ajuda a validar e corrigir a lógica, se necessário.

* Os arquivos de licença do PDF, que são definidos para DRM, precisam estar visíveis para todos, para que os usuários possam vê-los ao baixar o ativo com a licença.
