---
title: Perguntas frequentes sobre a integração AEM-Commerce usando o Commerce integration framework
description: Perguntas frequentes sobre a integração AEM-Commerce usando o Commerce integration framework
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
feature: Commerce Integration Framework
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 25%

---


# Perguntas frequentes sobre a integração AEM-Commerce usando o Commerce integration framework

## &#x200B;1. O CIF GraphQL é usado apenas para comércio ou será disponibilizado para consultar conteúdo criado no JCR do AEM? {#faq-1}

A Adobe adotou as APIs do GraphQL da Adobe Commerce como a API oficial para todos os dados relacionados ao comércio. Portanto, a AEM usa o GraphQL para trocar dados de comércio com a Adobe Commerce e com qualquer mecanismo de comércio por meio da I/O Runtime. Essa API do GraphQL é independente da API do GraphQL da AEM para acessar fragmentos de conteúdo.

## &#x200B;2. Os ativos do produto (imagens) podem ser armazenados e referenciados pelo AEM por meio do administrador do Adobe Commerce? Como os ativos do Dynamic Media podem ser consumidos? {#faq-2}

Não há integração oficial entre o AEM Assets e o Adobe Commerce disponível. Há um conector parceiro disponível no [marketplace.](https://commercemarketplace.adobe.com)

Ou, como solução alternativa, você pode armazenar ativos de produtos (imagens) no AEM Assets, mas deve armazenar manualmente os URLs de ativos no Adobe Commerce. O Dynamic Media agora faz parte do AEM Assets e funciona da mesma maneira.

## &#x200B;3. O local de implantação da solução comercial é importante? (No local ou na nuvem) {#faq-3}

Não, não importa onde a solução comercial é implantada. A CIF e a loja da AEM funcionam independentemente do modelo de implantação. No entanto, se a solução for implantada com a arquitetura de referência E2E recomendada, os testes E2E poderão ser executados em KPIs de desempenho que representam um perfil de cliente empresarial típico. Este método fornece informações adicionais que podem ser usadas como referencial.

## &#x200B;4. Como as páginas de catálogo ou de produto são criadas no AEM? Como elas continuam a existir no AEM? {#faq-4}

Páginas de catálogo e páginas de produto são criadas e armazenadas em cache dinamicamente no AEM com base em catálogos genéricos e modelos de página do produto. Nenhum dado de produto ou catálogo é importado e armazenado no AEM.

## &#x200B;5. A atualização dos dados do produto em sua solução comercial é um push em tempo real para o AEM? Ou é um processo em lote? {#faq-5}

O complemento CIF usado com o AEM Cloud Service permite que os dados fluam da solução comercial para o AEM sob demanda. Portanto, não é um processo de push em tempo real ou em lote quando há uma atualização na solução comercial.

## &#x200B;6. Que tamanho de catálogo é compatível com o AEM com CIF? {#faq-6}

Isso depende de alguns aspectos adicionais que você deve considerar. Qual é a taxa de cache de seus dados e páginas de catálogo? Quantas solicitações simultâneas você espera durante as horas de pico? Qual é a escalabilidade das APIs das suas soluções comerciais?

## &#x200B;7. Como o PIM atua nessa estrutura? {#faq-7}

Os dados do PIM são expostos ao AEM e aos clientes por meio de solicitações de GraphQL. Nossa recomendação é integrar o PIM ao mecanismo de comércio (Adobe Commerce ou outros) para que os dados do PIM possam ser recuperados do mecanismo de comércio.

## &#x200B;8. Também é possível armazenar preços e outros dados em cache por meio do Dispatcher? Esse armazenamento gera um desafio frequente de invalidação de cache? {#faq-8}

Dados dinâmicos, como preço ou inventário, não são armazenados em cache no Dispatcher. Os dados dinâmicos são obtidos por via direta no lado do cliente com componentes da Web usando APIs GraphQL. Somente dados estáticos (como dados de produto ou categoria) são armazenados em cache no Dispatcher. Se os dados do produto forem alterados, será necessário invalidar o cache.

## &#x200B;9. Como a invalidação de cache para o AEM Dispatcher funciona com o AEM e o commerce? {#faq-9}

A Adobe recomenda configurar a invalidação do cache com base em TTL para páginas armazenadas em cache na Dispatcher. Para obter informações dinâmicas, como preço ou estoque, a Adobe recomenda renderizar os dados no lado do cliente. Para obter mais informações sobre a invalidação do cache com base em TTL, consulte [Otimização do cache do Dispatcher.](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html)

## &#x200B;10. Há alguma recomendação sobre a pesquisa unificada de conteúdo no AEM com o Commerce? {#faq-10}

É fornecida uma implementação de referência de pesquisa de produto, mas não de pesquisa unificada com conteúdo. Esse recurso é específico do cliente e é melhor encontrar uma solução para cada projeto.

## &#x200B;11. Como a Pesquisa funciona com o AEM e o comércio usando o CIF? {#faq-11}

A CIF fornece os componentes Barra de pesquisa e Resultado da pesquisa. O componente Barra de pesquisa envia uma solicitação GraphQL com o termo de pesquisa para a solução comercial, que retorna uma lista de produtos que inclui nome do produto, preço, SLUG e assim por diante. O componente Resultado da pesquisa exibe os resultados da pesquisa em uma visualização de galeria em uma página de resultados da pesquisa criada no AEM. A Pesquisa aceita pesquisa básica de texto completo. Usamos a chave SLUG/URL para criar uma referência ao PDP.

## &#x200B;12. Como os dados do produto podem ser usados em MSM ou traduções? {#faq-12}

Os dados do produto já estão traduzidos no PIM ou no Adobe Commerce. A Integração AEM - Adobe Commerce oferece suporte à conexão com várias lojas e visualizações de loja da Adobe Commerce. Em uma configuração do MSM, normalmente um site do AEM está vinculado a uma visualização de loja da Adobe Commerce.

## &#x200B;13. Há alguma maneira de aprimorar os dados do produto com texto comercial? Onde é possível fazer isso? No AEM ou na solução comercial? {#faq-13}

A Adobe recomenda gerenciar dados e conteúdo relacionados a marketing no AEM. Decorar dados de produtos a partir de sua solução comercial com atributos adicionais usando Fragmentos de conteúdo ou criar e vincular Fragmentos de experiência para conteúdo não estruturado com seus produtos.

## &#x200B;14. Como é possível garantir a conformidade com o PCI ao usar o AEM para toda a camada de apresentação? {#faq-14}

A Adobe recomenda usar métodos de pagamento abstratos. Dessa forma, o cliente do navegador estabelece comunicação direta com o provedor do gateway de pagamento para que nem a Adobe nem as soluções comerciais retenham ou transmitam os dados do titular do cartão. Essa abordagem requer somente uma conformidade com PCI de nível 3. No entanto, há outros aspectos que devem ser considerados em termos de conformidade com o PCI, como a forma como os funcionários interagem com o sistema e os dados. Para obter mais informações sobre a conformidade do Adobe Commerce com o PCI, consulte [Requisitos de conformidade do PCI.](https://business.adobe.com/products/magento/pci-compliance.html)

## &#x200B;15. Se eu usar as versões em nuvem do AEM e do Adobe Commerce, essa solução conjunta é compatível com o PCI? {#faq-15}

Sim, o Questionário de autoavaliação D e o Atestado de conformidade estão disponíveis mediante solicitação.

## &#x200B;16. Como posso solicitar uma licença de avaliação da I/O Runtime? {#faq-16}

Consulte [Obtendo Acesso](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/) para obter detalhes sobre como solicitar uma licença de avaliação para usar a I/O Runtime.
