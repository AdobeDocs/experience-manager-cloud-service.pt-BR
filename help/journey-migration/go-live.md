---
title: Publicação
description: Saiba como executar a migração assim que o código e o conteúdo estiverem prontos para a nuvem
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 30acb844ee4021b3e14011b548825c864de8903d
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 2%

---

# Publicação {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparação ao vivo"
>abstract="Para garantir um lançamento tranquilo e bem-sucedido AEM as a Cloud Service, você deve planejar períodos de congelamento de código e conteúdo, iterações de teste, atualizações de conteúdo, testes de desempenho, testes de segurança e muito mais."

Nesta parte da jornada, você aprenderá a planejar e executar a migração assim que o código e o conteúdo estiverem prontos para serem transferidos para AEM as a Cloud Service. Além disso, você aprenderá quais são as práticas recomendadas e as limitações conhecidas ao executar a migração.

## A história até agora {#story-so-far}

Nas fases anteriores da jornada:

* Você aprendeu a começar a mudança para AEM as a Cloud Service na [Introdução](/help/journey-migration/getting-started.md) página.
* Determinado se sua implantação está pronta para ser movida para a nuvem ao ler o [Fase de preparação](/help/journey-migration/readiness.md)
* Familiarizou-se com as ferramentas e o processo através dos quais você pode preparar o código e a nuvem de conteúdo com o [Fase de implementação](/help/journey-migration/implementation.md).

## Objetivo {#objective}

Este documento ajudará você a entender como executar a migração para o AEM as a Cloud Service depois de conhecer as etapas anteriores da jornada. Você aprenderá a executar a migração de produção inicial, bem como as práticas recomendadas a serem seguidas ao migrar para AEM as a Cloud Service.

## Migração de produção inicial {#initial-migration}

Antes de executar a migração de produção, siga as etapas de instalação e prova da migração descritas na seção [Estratégia e cronograma da migração de conteúdo](/help/journey-migration/implementation.md##strategy-timeline) da seção [Fase de implementação](/help/journey-migration/implementation.md).

* Inicie a migração da produção com base na experiência adquirida durante a migração do estágio as a Cloud Service de AEM realizada em clones:
   * Autor-autor
   * Publicar-Publicar

* Valide o conteúdo assimilado nos níveis de autor e publicação as a Cloud Service AEM.
* Instrua a equipe de criação de conteúdo a evitar mover o conteúdo na origem e no destino até que a assimilação seja concluída
* O novo conteúdo pode ser adicionado, editado ou excluído, mas evite movê-lo. Isso se aplica tanto à origem quanto ao destino.
* Registre o [tempo](/help/journey-migration/implementation.md#gathering-data) para extração e assimilação completas para ter uma estimativa de futuras linhas do tempo de migração complementar.
* Crie um [planejador de migração](/help/journey-migration/implementation.md#migration-plan) para autor e publicação.

## Top-Ups Incrementais {#top-up}

Após a migração inicial da produção, você deve executar atualizações adicionais para garantir que seu conteúdo seja atualizado na instância da nuvem. Por causa disso, é recomendável seguir as práticas recomendadas a seguir:

* Colete dados sobre a quantidade de conteúdo. Por exemplo: por uma semana, duas semanas ou um mês.
* Certifique-se de planejar as atualizações principais de forma que você evite mais de 48 horas de extração e ingestão de conteúdo. Isso é recomendado para que os upups de conteúdo caibam em um período de fim de semana.
* Planeje o número de top ups necessários e use essas estimativas para planejar a data de ativação.

## Identificar o código e as linhas do tempo de congelamento de conteúdo para a migração {#code-content-freeze}

Como mencionado anteriormente, você precisará programar um período de código e congelamento de conteúdo. Use as seguintes perguntas para ajudá-lo a planejar o período de congelamento:

* Por quanto tempo tenho que congelar as atividades de criação de conteúdo?
* Por quanto tempo devo solicitar que minha equipe de entrega pare de adicionar novos recursos?

Para responder a primeira pergunta, considere o tempo necessário para executar execuções de avaliação em ambientes não relacionados à produção. Para responder a segunda pergunta, você precisa de uma estreita colaboração entre a equipe que está adicionando novos recursos e a equipe que refatora o código. O objetivo deve ser garantir que todo o código adicionado à implantação existente também seja adicionado, testado e implantado na ramificação de serviços em nuvem. Em geral, isso significa que a quantidade de congelamento do código será menor.

Além disso, você precisa planejar um congelamento de conteúdo quando a complementação de conteúdo final estiver programada.

## Práticas recomendadas     {#best-practices}

Ao planejar ou executar a migração, você deve considerar as seguintes diretrizes:

* Migrar de autor para autor e publicar para publicação
* Solicitar um clone de produção que possa ser usado para:
   * Capturar estatísticas do repositório
   * Prova das atividades de migração
   * Preparar o plano de migração
   * Identificar requisitos de congelamento de conteúdo
   * Identifique quaisquer necessidades de redimensionamento na produção ao fazer a migração da produção

**Práticas recomendadas da ferramenta Transferência de conteúdo**

Certifique-se de que, ao entrar em funcionamento, você execute a migração de conteúdo na produção em vez de um clone. Uma boa abordagem é utilizar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para a migração inicial e, em seguida, execute extrações adicionais frequentemente (até diariamente) para extrair partes menores e evitar qualquer carga de longo prazo no AEM de origem.

Ao executar a migração de produção, você deve evitar executar a ferramenta Transferência de conteúdo a partir de um clone, pois:

* Se um cliente exigir que versões de conteúdo sejam migradas durante as migrações de complemento, a execução da ferramenta Transferência de conteúdo de um clone não migra as versões. Mesmo que o clone seja recriado com frequência do autor ao vivo, sempre que um clone for criado, os pontos de verificação que serão usados pela ferramenta Transferência de conteúdo para calcular o deltas serão redefinidos.
* Como um clone não pode ser atualizado como um todo, o pacote Consulta ACL deve ser usado para empacotar e instalar o conteúdo que está sendo adicionado ou editado da produção para clonar. O problema com essa abordagem é que qualquer conteúdo excluído na instância de origem nunca chegará ao clone a menos que seja excluído manualmente da origem e do clone. Isso introduz a possibilidade de o conteúdo excluído na produção não ser excluído no clone e AEM as a Cloud Service.

**Otimização da carga na fonte de AEM ao executar a migração de conteúdo**

Lembre-se, a carga na fonte de AEM será maior durante a fase de extração. Você deve estar ciente de que:

* A ferramenta Transferência de conteúdo é um processo Java externo que usa um heap da JVM de 4 GB
* A versão que não é AzCopy baixa binários, armazena em um espaço temporário no autor do AEM de origem, consumindo E/S de disco, e então carrega no contêiner do Azure que consome largura de banda da rede
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) O transfere blobs diretamente do armazenamento de blobs para o contêiner do Azure, que salva a E/S do disco e a largura de banda da rede. A versão do AzCopy ainda usa o disco e a largura de banda da rede para extrair e carregar os dados do armazenamento de segmentos no contêiner do Azure
* O processo da ferramenta Transferência de conteúdo é mais leve nos recursos do sistema durante a fase de assimilação, já que ele apenas transmite logs de assimilação e não há muita carga na instância de origem no que diz respeito à E/S de disco ou à largura de banda da rede.

## Limitações conhecidas {#known-limitations}

Considere que toda a assimilação falha se alguma das limitações a seguir for encontrada como parte do conjunto de migração extraída:

* Um Nó JCR que tem um nome com mais de 150 caracteres
* Um Nó JCR maior que 16 MB
* Qualquer usuário/grupo com `rep:AuthorizableID` ser assimilado que já está presente em AEM as a Cloud Service
* Se qualquer ativo extraído e assimilado for movido para um caminho diferente na origem ou no destino antes da próxima iteração da migração.

## Integridade do ativo {#asset-health}

Comparativamente à seção acima da ingestão **não** falha devido às seguintes preocupações com o ativo. No entanto, é altamente recomendável que você siga as etapas apropriadas nesses cenários:

* Qualquer ativo que tenha a representação original ausente
* Qualquer pasta que esteja ausente `jcr:content` nó .

Ambos os itens acima serão identificados e reportados na variável [Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) relatório.

## Lista de verificação ao vivo {#Go-Live-Checklist}

Revise esta lista de atividades para garantir que você realize uma migração tranquila e bem-sucedida.

* Execute um pipeline de produção completo com teste funcional e de interface do usuário para garantir uma **sempre atual** AEM experiência com o produto. Consulte os seguintes recursos.
   * [Atualizações de versão do AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Teste funcional personalizado](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Teste de interface](/help/implementing/cloud-manager/ui-testing.md)
* Migre o conteúdo para produção e verifique se um subconjunto relevante está disponível no armazenamento temporário para testes.
   * Observe que as práticas recomendadas do DevOps para AEM implicam que o código avance do ambiente de desenvolvimento para o de produção, enquanto o conteúdo desaparece dos ambientes de produção.
* Programe um período de congelamento de código e conteúdo.
   * Consulte também a seção [Linhas do tempo de congelamento de código e conteúdo para a migração](#code-content-freeze)
* Realize a complementação do conteúdo final.
* Validar configurações do dispatcher.
   * Usar um validador de dispatcher local que facilite a configuração, validação e simulação do dispatcher localmente
      * [Configure as ferramentas locais do dispatcher.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * Revise a configuração do host virtual cuidadosamente.
      * A solução mais fácil (e padrão) é incluir `ServerAlias *` no arquivo de host virtual no `/dispatcher/src/conf.d/available_vhostsfolder`.
         * Isso permitirá que os aliases do host usados pelos testes funcionais do produto, a invalidação do cache do dispatcher e os clones funcionem.
      * No entanto, se `ServerAlias *` não é aceitável, pelo menos `ServerAlias` As entradas devem ser permitidas além dos domínios personalizados:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configure CDN, SSL e DNS.
   * Se estiver usando seu próprio CDN, insira um tíquete de suporte para configurar o roteamento apropriado.
      * Consulte a seção [A CDN do cliente aponta para AEM CDN gerenciada](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) na documentação da CDN para obter detalhes.
      * Você precisará configurar o SSL e o DNS de acordo com a documentação do seu fornecedor de CDN.
   * Se você não estiver usando um CDN adicional, gerencie o SSL e o DNS de acordo com a seguinte documentação:
      * Gerenciar certificados SSL
         * [Introdução ao gerenciamento de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Gerenciar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Gerenciando nomes de domínio personalizados (DNS)
         * Para garantir que o contêiner de DNS não apresente problemas inesperados, é melhor criar um subdomínio de teste para conectar sua instância de produção ao antes de entrar em funcionamento e realizar um ciclo de teste de UAT. Portanto, se o domínio for example.com, você poderá criar um subdomínio test.example.com e aplicá-lo à produção. Durante o teste de UAT do domínio, você desejará procurar por coisas como redirecionamento de link adequado, armazenamento em cache e configurações do dispatcher.
         * [Introdução a nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Gerenciar nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Lembre-se de validar o TTL definido para seu registro DNS.
      * O TTL é o tempo que um registro DNS permanece em um cache antes de solicitar uma atualização ao servidor.
      * Se você tiver um TTL muito alto, as atualizações no registro DNS levarão mais tempo para serem propagadas.
* Execute testes de desempenho e segurança que atendam às necessidades e objetivos de sua empresa.
* Recorte e certifique-se de que o lançamento real seja executado sem qualquer nova implantação ou atualização de conteúdo.
* Crie perfis de notificação do usuário do Admin Console. Consulte [Perfis de notificação](/help/journey-onboarding/notification-profiles.md)

Você sempre pode fazer referência à lista caso precise recalibrar suas tarefas ao executar a migração.

## O que vem a seguir {#what-is-next}

Assim que entender como executar a migração para AEM as a Cloud Service, você poderá verificar a variável [Pós-ativação](/help/journey-migration/post-go-live.md) para manter sua instância em execução sem problemas.
