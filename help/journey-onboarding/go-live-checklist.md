---
title: Lista de verificação de ativação
description: Saiba mais sobre todos os elementos que precisam estar em vigor para ter uma ativação bem-sucedida com o AEM as a Cloud Service
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 4%

---

# Lista de verificação de ativação {#Go-Live-Checklist}

Revise esta lista de atividades para garantir que você execute uma ativação tranquila e bem-sucedida.

* Execute um pipeline de produção completo com testes funcionais e de interface do usuário para garantir uma **sempre atual** Experiência do produto AEM. Consulte os recursos a seguir.
   * [Atualizações de versão do AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Teste funcional personalizado](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Teste de interface](/help/implementing/cloud-manager/ui-testing.md)
* Se estiver migrando do AEM 6.5, você deve migrar o conteúdo para produção e garantir que um subconjunto relevante esteja disponível nos estágios para teste.
   * As práticas recomendadas de DevOps para AEM implicam que o código passa do desenvolvimento para o ambiente de produção, enquanto o conteúdo passa dos ambientes de produção.
* Programar um período de congelamento do código e do conteúdo.
   * Consulte também a seção [Cronogramas de congelamento de código e conteúdo para a migração](#code-content-freeze)
* Faça a complementação do conteúdo final.
* Validar configurações do dispatcher.
   * Usar um validador de dispatcher local que facilite a configuração, validação e simulação do dispatcher localmente
      * [Configurar as ferramentas do dispatcher local.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)
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
   * Realizar testes no ambiente de preparo.  Ele tem o mesmo tamanho da produção.
   * Ambientes de desenvolvimento não têm o mesmo tamanho que preparo e produção.
* Transfira e verifique se a ativação real é realizada sem nenhuma nova implantação ou atualização de conteúdo.
* Criar perfis de notificação de usuário Admin Console. Consulte [Perfis de notificação](/help/journey-onboarding/notification-profiles.md)
* Considere a configuração das Regras de filtro de tráfego para controlar qual tráfego não deve ser permitido em seu site.
   * As regras de filtro de tráfego de limite de taxa podem ser uma ferramenta eficaz contra ataques de DDoS. Uma categoria especial de regras de filtro de tráfego, chamada de regras WAF, requer uma licença separada.
   * Consulte a documentação para obter alguns [regras de início sugeridas](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Você sempre pode consultar a lista caso precise recalibrar suas tarefas durante a ativação.
