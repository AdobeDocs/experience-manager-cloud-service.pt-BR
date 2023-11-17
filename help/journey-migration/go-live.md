---
title: Publicação
description: Saiba como executar a migração depois que o código e o conteúdo estiverem prontos para nuvem
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 4%

---

# Publicação {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparo para a ativação"
>abstract="Para garantir uma ativação tranquila e bem-sucedida do AEM as a Cloud Service, você deve planejar períodos de congelamento de código e conteúdo, iterações de teste, atualizações de conteúdo, testes de desempenho, testes de segurança e muito mais."

Nesta parte da jornada, você aprenderá a planejar e executar a migração assim que o código e o conteúdo estiverem prontos para serem transferidos para o AEM as a Cloud Service. Além disso, você aprenderá quais são as práticas recomendadas e as limitações conhecidas ao executar a migração.

## A história até agora {#story-so-far}

Nas fases anteriores da jornada:

* Você aprendeu como começar a migrar para o AEM as a Cloud Service na [Introdução](/help/journey-migration/getting-started.md) página.
* Determinado se sua implantação está pronta para ser movida para a nuvem lendo o [Fase de preparação](/help/journey-migration/readiness.md)
* Familiarizou-se com as ferramentas e o processo pelos quais é possível preparar seu código e sua nuvem de conteúdo com o [Fase de implementação](/help/journey-migration/implementation.md).

## Objetivo {#objective}

Este documento ajuda você a entender como executar a migração para o AEM as a Cloud Service depois de conhecer as etapas anteriores da jornada. Você aprenderá a executar a migração de produção inicial e as práticas recomendadas a serem seguidas ao migrar para o AEM as a Cloud Service.

## Migração de produção inicial {#initial-migration}

Antes de executar a migração de produção, siga as etapas de ajuste e prova de migração descritas na seção [Estratégia e cronograma de migração de conteúdo](/help/journey-migration/implementation.md##strategy-timeline) seção do [Fase de implementação](/help/journey-migration/implementation.md).

* Inicie a migração da produção com base na experiência adquirida durante a migração do estágio de AEM as a Cloud Service executada em clones:
   * Autor-Autor
   * Publish-Publish

* Valide o conteúdo assimilado nos níveis de criação e publicação as a Cloud Service do AEM.
* Instrua a equipe de criação de conteúdo a evitar mover o conteúdo na origem e no destino até que a assimilação seja concluída
* O novo conteúdo pode ser adicionado, editado ou excluído, mas evite movê-lo. Isso se aplica tanto à origem quanto ao destino.
* Registre o [tempo decorrido](/help/journey-migration/implementation.md#gathering-data) para que a extração e a assimilação completas tenham uma estimativa dos cronogramas de migração complementar futuros.
* Criar um [planejador de migração](/help/journey-migration/implementation.md#migration-plan) para autor e publicação.

## Complementos incrementais {#top-up}

Após a migração inicial da produção, você deve realizar atualizações complementares incrementais para garantir que seu conteúdo seja atualizado na instância da nuvem. Por causa disso, recomenda-se seguir estas práticas recomendadas:

* Colete dados sobre a quantidade de conteúdo. Por exemplo: por uma semana, duas semanas ou um mês.
* Certifique-se de planejar as atualizações complementares de forma a evitar mais de 48 horas de extração e assimilação de conteúdo. Isso é recomendado para que as atualizações complementares de conteúdo se encaixem em um intervalo de tempo de fim de semana.
* Planeje o número de atualizações necessárias e use essas estimativas para planejar a data de ativação.

## Identificar os cronogramas de congelamento de código e conteúdo para a migração {#code-content-freeze}

Como mencionado anteriormente, será necessário agendar um código e um período de congelamento do conteúdo. Use as seguintes perguntas para ajudá-lo a planejar o período de congelamento:

* Por quanto tempo preciso congelar as atividades de criação de conteúdo?
* Por quanto tempo devo solicitar que minha equipe de entrega pare de adicionar novos recursos?

Para responder à primeira pergunta, considere o tempo necessário para executar execuções de avaliação em ambientes não relacionados à produção. Para responder à segunda pergunta, você precisa de uma colaboração estreita entre a equipe que está adicionando novos recursos e a equipe que está refatorando o código. O objetivo é garantir que todo o código adicionado à implantação existente também seja adicionado, testado e implantado na ramificação dos serviços em nuvem. Geralmente, significa que a quantidade de congelamento do código é menor.

Além disso, você precisa planejar um congelamento de conteúdo quando a atualização final do conteúdo for agendada.

## Práticas recomendadas {#best-practices}

Ao planejar ou executar a migração, você deve considerar as seguintes diretrizes:

* Migrar de Autor para Autor e Publicar para Publicação
* Solicite um clone de produção que possa ser usado para:
   * Capturar estatísticas do repositório
   * Prova de atividades de migração
   * Preparar o plano de migração
   * Identificar requisitos de congelamento de conteúdo
   * Identificar quaisquer necessidades de upsizing na produção ao fazer a migração da produção

**Práticas recomendadas da ferramenta Transferência de conteúdo**

Ao entrar em funcionamento, certifique-se de executar a migração de conteúdo na produção em vez de em um clone. Uma boa abordagem é usar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para a migração inicial e, em seguida, executar extrações complementares com frequência (mesmo diariamente) para extrair partes menores e evitar qualquer carga de longo prazo no AEM de origem.

Ao executar a migração de produção, você deve evitar a execução da ferramenta Transferência de conteúdo a partir de um clone, pois:

* Se um cliente solicitar que as versões de conteúdo sejam migradas durante as migrações complementares, a execução da ferramenta Transferência de conteúdo de um clone não migrará as versões. Mesmo que o clone seja recriado frequentemente a partir de um autor ativo, cada vez que um clone é criado, os pontos de verificação usados pela ferramenta Transferência de conteúdo para calcular os deltas são redefinidos.
* Como um clone não pode ser atualizado como um todo, o pacote de Consulta ACL deve ser usado para empacotar e instalar o conteúdo que está sendo adicionado ou editado de produção para clone. O problema dessa abordagem é que qualquer conteúdo excluído na instância de origem nunca chegará ao clone, a menos que seja excluído manualmente da origem e do clone. Isso introduz a possibilidade de que o conteúdo excluído na produção não seja excluído no clone e no AEM as a Cloud Service.

**Otimização da carga na origem do AEM ao executar a migração de conteúdo**

Lembre-se, a carga na fonte AEM é maior durante a fase de extração. Você deve estar ciente de que:

* A Ferramenta de transferência de conteúdo é um processo Java externo que usa um Heap JVM de 4 GB
* A versão que não é do AzCopy baixa binários, armazena em um espaço temporário no autor AEM de origem, consumindo E/S de disco e faz upload no contêiner do Azure que consome largura de banda de rede
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) transfere blobs diretamente do armazenamento de blobs para o contêiner do Azure, o que salva a E/S de disco e a largura de banda da rede. A versão do AzCopy ainda usa o disco e a largura de banda da rede para extrair e carregar os dados do armazenamento de segmentos no container do Azure
* O processo da ferramenta Transferência de conteúdo é mais leve nos recursos do sistema durante a fase de assimilação, pois apenas transmite logs de assimilação e não há muita carga na instância de origem no que diz respeito à E/S de disco ou à largura de banda da rede.

## Limitações conhecidas {#known-limitations}

Leve em consideração que toda a assimilação falhará se qualquer uma das seguintes limitações for encontrada como parte do conjunto de migração extraído:

* Um Nó JCR que tem um nome com mais de 150 caracteres
* Um Nó JCR com mais de 16 MB
* Qualquer usuário/grupo com `rep:AuthorizableID` sendo assimilado que já está presente no AEM as a Cloud Service
* Se qualquer ativo extraído e assimilado for movido para um caminho diferente na origem ou no destino antes da próxima iteração da migração.

## Integridade do ativo {#asset-health}

Em comparação à seção acima da assimilação **não** falha devido às seguintes preocupações com ativos. No entanto, é altamente recomendável que você siga as etapas apropriadas nestes cenários:

* Qualquer ativo que tenha a representação original ausente
* Qualquer pasta que tenha um ausente `jcr:content` nó.

Ambos os itens acima são identificados e relatados na variável [Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) relatório.

## Lista de verificação de ativação {#Go-Live-Checklist}

Revise esta lista de atividades para garantir que você execute uma migração tranquila e bem-sucedida.

* Execute um pipeline de produção completo com testes funcionais e de interface do usuário para garantir uma **sempre atual** Experiência do produto AEM. Consulte os seguintes recursos.
   * [Atualizações de versão do AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Teste funcional personalizado](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Teste de interface](/help/implementing/cloud-manager/ui-testing.md)
* Migre o conteúdo para produção e verifique se um subconjunto relevante está disponível no ambiente de preparo para testes.
   * As práticas recomendadas de DevOps para AEM implicam que o código passa do desenvolvimento para o ambiente de produção, enquanto o conteúdo passa dos ambientes de produção.
* Programar um período de congelamento do código e do conteúdo.
   * Consulte também a seção [Cronogramas de congelamento de código e conteúdo para a migração](#code-content-freeze)
* Faça a complementação do conteúdo final.
* Validar configurações do dispatcher.
   * Usar um validador de dispatcher local que facilite a configuração, validação e simulação do dispatcher localmente
      * [Configurar as ferramentas do dispatcher local.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * Analise cuidadosamente a configuração do host virtual.
      * A solução mais fácil (e padrão) é incluir `ServerAlias *` em seu arquivo de host virtual no `/dispatcher/src/conf.d/available_vhostsfolder`.
         * Isso permitirá que os aliases de host usados pelos testes funcionais do produto, invalidação do cache do dispatcher e clones funcionem.
      * No entanto, se `ServerAlias *` não é aceitável, pelo menos, o seguinte: `ServerAlias` as entradas devem ser permitidas além dos domínios personalizados:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configure CDN, SSL e DNS.
   * Se você estiver usando seu próprio CDN, insira um tíquete de suporte para configurar o roteamento apropriado.
      * Consulte a seção [O CDN do cliente aponta para o CDN gerenciado pelo AEM](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) na documentação da CDN para obter detalhes.
      * Configure o SSL e o DNS de acordo com a documentação do fornecedor do CDN.
   * Se você não estiver usando um CDN adicional, gerencie o SSL e o DNS de acordo com a seguinte documentação:
      * Gerenciar certificados SSL
         * [Introdução ao gerenciamento de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Gerenciar o certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Gerenciar nomes de domínio personalizados (DNS)
         * Para garantir que a transferência de DNS não cause problemas inesperados, é melhor criar um subdomínio de teste para conectar sua instância de produção ao antes de entrar em funcionamento e realizar uma rodada de testes UAT. Portanto, se o domínio for example.com, você poderá criar um subdomínio test.example.com e aplicá-lo à produção. Durante os testes UAT do domínio, você deverá procurar itens como redirecionamento adequado de link, armazenamento em cache e configurações do dispatcher.
         * [Introdução a nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Gerenciar nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Lembre-se de validar o TTL definido para seu registro DNS.
      * O TTL é o tempo que um registro DNS permanece em um cache antes de solicitar uma atualização ao servidor.
      * Se você tiver um TTL muito alto, as atualizações do seu registro DNS levarão mais tempo para se propagar.
* Execute testes de desempenho e segurança que atendam aos requisitos e objetivos de sua empresa.
* Transfira e verifique se a ativação real é realizada sem nenhuma nova implantação ou atualização de conteúdo.
* Criar perfis de notificação de usuário Admin Console. Consulte [Perfis de notificação](/help/journey-onboarding/notification-profiles.md)

Você sempre pode consultar a lista caso precise recalibrar suas tarefas ao executar a migração.

## O que vem a seguir {#what-is-next}

Depois de entender como executar a migração para o AEM as a Cloud Service, você pode verificar o [Pós-ativação](/help/journey-migration/post-go-live.md) página para manter sua instância em execução sem problemas.
