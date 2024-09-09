---
title: Lista de verificação de ativação
description: Saiba mais sobre todos os elementos que precisam estar em vigor para ter uma ativação bem-sucedida com o AEM as a Cloud Service.
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Lista de verificação de ativação {#Go-Live-Checklist}

Revise esta lista de atividades para garantir que você execute uma ativação tranquila e bem-sucedida.

* Execute um pipeline de produção completo com testes funcionais e de interface do usuário para garantir uma experiência do produto AEM **always current**. Consulte os recursos a seguir.
   * [Atualizações de versão do AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Teste funcional personalizado](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Teste de interface](/help/implementing/cloud-manager/ui-testing.md)
* Se estiver migrando do AEM 6.5, você deve migrar o conteúdo para produção e garantir que um subconjunto relevante esteja disponível nos estágios para teste.
   * As práticas recomendadas de DevOps para AEM implicam que o código passa do desenvolvimento para o ambiente de produção, enquanto o conteúdo passa dos ambientes de produção.
* Programar um período de congelamento do código e do conteúdo.
   * Consulte também a seção [Linhas do tempo de congelamento de código e conteúdo da migração](#code-content-freeze)
* Faça a complementação do conteúdo final.
* Validar configurações do Dispatcher.
   * Usar um validador local do Dispatcher que facilite a configuração, validação e simulação do Dispatcher localmente
      * [Configurar as ferramentas locais do Dispatcher](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites).
   * Analise cuidadosamente a configuração do host virtual.
      * A solução mais fácil (e padrão) é incluir `ServerAlias *` em seu arquivo de host virtual no `/dispatcher/src/conf.d/available_vhostsfolder`. Isso permite que os aliases de host usados pelos testes funcionais do produto, a invalidação do cache do Dispatcher e os clones funcionem.
      * No entanto, se `ServerAlias *` não for aceitável, pelo menos as `ServerAlias` entradas a seguir deverão ser permitidas além de seus domínios personalizados:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configure CDN, SSL e DNS.
   * Se você estiver usando seu próprio CDN, insira um tíquete de suporte para configurar o roteamento apropriado.
      * Consulte a seção [CDN do cliente aponta para o CDN gerenciado por AEM](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) na documentação do CDN para obter detalhes.
      * Configure o SSL e o DNS de acordo com a documentação do fornecedor do CDN.
   * Se você não estiver usando um CDN adicional, gerencie o SSL e o DNS de acordo com a seguinte documentação:
      * Gerenciar certificados SSL
         * [Introdução ao gerenciamento de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Gerenciar nomes de domínio personalizados (DNS)
         * Certifique-se de que a transferência de DNS não cause problemas inesperados. Crie um subdomínio de teste para conectar sua instância de produção ao antes de entrar em funcionamento e fazer uma rodada de testes UAT. Portanto, se o domínio for example.com, você poderá criar um subdomínio test.example.com e aplicá-lo à produção. Durante os testes UAT do domínio, procure itens como redirecionamento adequado de link, armazenamento em cache e configurações do Dispatcher.
         * [Introdução a nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Gerenciar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Lembre-se de validar o TTL definido para seu registro DNS.
      * O TTL é o tempo que um registro DNS permanece em um cache antes de solicitar uma atualização ao servidor.
      * Se você tiver um TTL muito alto, as atualizações do registro DNS levarão mais tempo para se propagar.
* Execute testes de desempenho e segurança que atendam aos requisitos e objetivos de sua empresa.
   * Realizar testes em um ambiente de preparo.  Ele tem o mesmo tamanho da produção.
   * Ambientes de desenvolvimento não têm o mesmo tamanho que preparo e produção.
* Transfira e verifique se a ativação real é realizada sem nenhuma nova implantação ou atualização de conteúdo.
* Criar Perfis De Notificação De Usuário Do Admin Console. Consulte [Perfis de notificação](/help/journey-onboarding/notification-profiles.md)
* Considere a configuração das Regras de filtro de tráfego para controlar qual tráfego não deve ser permitido em seu site.
   * Regras de filtro de tráfego de limite de taxa podem ser uma ferramenta eficaz contra ataques de DDoS. Uma categoria especial de Regras de filtro de tráfego, chamada de Regras do WAF (Web Application Firewall), requer uma licença separada.
   * Consulte a documentação para algumas [regras de início sugeridas](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Você sempre pode consultar a lista caso precise recalibrar suas tarefas durante a ativação.
