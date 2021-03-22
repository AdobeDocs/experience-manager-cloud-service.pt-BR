---
title: AEM - Perguntas frequentes sobre a integração com o Commerce usando a Commerce Integration Framework
description: AEM - Perguntas frequentes sobre a integração com o Commerce usando a Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 903a78d98082b937128073d5edce23dc70b01a1d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 68%

---


# AEM - Perguntas frequentes sobre a integração com o Commerce usando a Commerce Integration Framework


## 1. O GraphQL da CIF é usado apenas para comércio ou será disponibilizado para consultar conteúdo criado AEM JCR?

A Adobe adotou as APIs GraphQL da Magento como a API oficial para todos os dados relacionados ao comércio. Portanto, o AEM usa GraphQL para trocar dados de comércio com a Magento e com qualquer mecanismo de comércio por meio da I/O Runtime. Essa API GraphQL é independente AEM API GraphQL para acessar os Fragmentos de conteúdo.

## 2. Como o Adobe I/O entra em jogo? O AEM se comunica diretamente com a Magento?

O AEM pode se conectar diretamente à Magento sem uma camada de I/O Runtime. Se for preciso integrar um back-end de comércio que não seja a Magento (solução de terceiros) ao AEM, a plataforma I/O Runtime poderá ser usada para hospedar a camada de mapeamento para conectar as APIs GraphQL da Magento a qualquer API de soluções de terceiros. Para obter mais detalhes, consulte esta [implementação de referência](https://github.com/adobe/commerce-cif-graphql-integration-reference). Para soluções que não sejam a Magento, o AEM seria configurado para indicar o ponto de extremidade da plataforma I/O Runtime.

A plataforma I/O Runtime também pode ser usada para estender ou personalizar os serviços de comércio. Para esses casos de uso, você chamaria o ponto de extremidade da I/O Runtime, que hospeda uma implementação personalizada do serviço respectivo. Casos de uso de integração e extensão podem ser combinados.

## 3. Os ativos do produto (imagens) podem ser armazenados e referenciados pelo AEM via administração da Magento? Como os ativos do Dynamic Media podem ser consumidos?

Atualmente, não existe uma integração entre o AEM Assets e a Magento. Como solução, você pode armazenar ativos de produtos (imagens) no AEM Assets, mas terá que armazenar manualmente os URLs de ativos na Magento. O Dynamic Media agora faz parte do AEM Assets e funcionará da mesma maneira.

## 4. Importa onde a solução comercial é implantada? (No local ou na nuvem)

Não importa onde sua solução comercial é implantada. A integração e a nova loja de referência AEM Venia funcionarão independentemente do modelo de implantação. No entanto, se for implantada com base na arquitetura de referência E2E aprovada, serão executados testes E2E com KPIs de desempenho coletados que representam o perfil de um cliente corporativo. Portanto, haverá informações adicionais que você pode usar como referencial.

## 5. Como as páginas de catálogo ou de produto são criadas no AEM? Como elas continuam a existir no AEM?

Páginas de catálogo e páginas de produto são criadas e armazenadas em cache dinamicamente no AEM com base em catálogos genéricos e modelos de página de produto. Nenhum dado de produto ou catálogo é importado e armazenado no AEM.

## 6. Quando você atualiza os dados do produto em sua solução comercial, isso é um push em tempo real para AEM? Ou é um processo em lote?

O complemento CIF usado com AEM Cloud Service permite que os dados fluam da solução comercial para AEM sob demanda. Portanto, esse não é um processo de push em tempo real ou em lote quando há uma atualização na solução comercial.

## 7. Que tamanho de catálogo AEM com o suporte à CIF?

À medida que os dados do produto e as páginas de catálogo são criados e armazenados em cache dinamicamente, não há limite de tamanho de correção. No entanto, o tamanho do catálogo é apenas um aspecto que você precisa considerar. A taxa de cache, as solicitações de dados simultâneas e a criação de página podem afetar a escalabilidade e o desempenho.

## 8. Como o PIM atua nessa estrutura?

Os dados do PIM são expostos ao AEM e aos clientes por meio de solicitações de GraphQL. Nossa recomendação é integrar o PIM ao mecanismo de comércio (Magento ou outros) para que os dados do PIM possam ser recuperados do mecanismo de comércio.

## 9. Também é possível armazenar preços e outros dados em cache por meio do Dispatcher? Esse armazenamento gera um desafio frequente de invalidação de cache?

Dados dinâmicos, como preço ou inventário, não são armazenados em cache no Dispatcher. Os dados dinâmicos são obtidos por via direta no lado do cliente com componentes da Web usando APIs GraphQL. Somente dados estáticos (como dados de produto ou categoria) são armazenados em cache no Dispatcher. Se os dados do produto forem alterados, será preciso invalidar o cache.

## 10. Como a invalidação de cache para AEM Dispatcher funciona com AEM e comércio?

Recomendamos configurar a invalidação do cache com base em TTL para páginas armazenadas em cache no Dispatcher. Para obter informações dinâmicas, como preço ou estoque, recomendamos renderizar a data no lado do cliente. Para obter mais informações sobre a invalidação do cache com base em TTL, consulte [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 11. Há alguma recomendação sobre a pesquisa unificada de conteúdo no AEM com o Commerce?

É fornecida uma implementação de referência de pesquisa de produto, mas não de pesquisa unificada com conteúdo. Geralmente, esse recurso depende muito do cliente e é melhor encontrar uma solução para cada projeto.

## 12. Como a pesquisa funciona com AEM e comércio usando a CIF?

A CIF fornece os componentes Barra de pesquisa e Resultado da pesquisa. O componente Barra de pesquisa envia uma solicitação GraphQL com o termo de pesquisa para a solução de comércio, que retorna uma lista de produtos que inclui nome do produto, preço, SLUG, etc. O componente Resultado da pesquisa exibe os resultados da pesquisa em uma visualização de galeria em uma página de resultados da pesquisa criada no AEM. A Pesquisa aceita pesquisa básica de texto completo. Usamos a chave SLUG/URL para criar uma referência ao PDP.

## 13. Como os dados do produto podem ser usados em MSM ou traduções?

Os dados do produto geralmente já são traduzidos no PIM ou na Magento. A integração AEM–Magento suporta a conexão com várias lojas e visualizações de loja da Magento. Geralmente, em uma configuração MSM um site do AEM está vinculado a uma visualização da loja da Magento.

## 14. Como a CIF funciona com plataformas de comércio que não são Magento?

A integração com soluções de terceiros, como outras soluções de comércio (diferentes da Magento), é feita por meio da plataforma I/O Runtime. Criamos uma [implementação de referência](https://github.com/adobe/commerce-cif-graphql-integration-reference) para demonstrar como isso é feito. Você pode reutilizar o [Conector de nuvem CIF do AEM](https://github.com/adobe/commerce-cif-connector) e os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) indicando a API GraphQL da Magento em qualquer plataforma de comércio de terceiros. Para oferecer o máximo de flexibilidade e escalabilidade, essa camada de integração é implantada na plataforma sem servidor [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html).

## 15. Há alguma maneira de aprimorar os dados do produto com texto comercial? Onde é possível fazer isso? No AEM ou na solução comercial?

Recomendamos gerenciar dados e conteúdo de marketing relacionados no AEM. Decorre dados de produtos de sua solução comercial com atributos adicionais usando Fragmentos de conteúdo ou crie e vincule Fragmentos de experiência para conteúdo não estruturado com seus produtos.

## 16. A integração AEM–Magento muda quando a plataforma Adobe I/O Runtime é usada?

Os clientes que desejam estender os serviços de comércio podem usar as mesmas sequências de ação de integração e gravação hospedadas na plataforma I/O Runtime para injetar a lógica de negócios e enriquecer os serviços de comércio.

## 17. A loja do aplicativo de página única funcionará com o editor de aplicativo de página única do AEM?

O AEM pode ser usado como ferramenta de criação para qualquer tipo de loja. Atualmente, a renderização do lado do servidor e do cliente (híbrida) é usada AEM loja. Lançaremos o suporte ao PWA para criação de conteúdo headless e headful posteriormente em 2021.


## 18. Como podemos garantir a conformidade com o PCI ao usar o AEM para a camada de apresentação inteira?

Recomendamos usar métodos de pagamento abstratos. Isso coloca o cliente do navegador em comunicação direta com o provedor do gateway de pagamento para que nem o Adobe nem as soluções de comércio retenham ou transmitam os dados do titular do cartão. Esta abordagem requer apenas uma conformidade PCI de nível 3. No entanto, há outros aspectos que devem ser considerados em termos de conformidade com o PCI, como o modo como os funcionários interagem com o sistema e os dados. Para obter mais informações sobre a conformidade da Magento com o PCI, consulte https://magento.com/pci-compliance

## 19. Se eu usar versões de nuvem de AEM e Magento, esta solução conjunta é compatível com PCI?

Sim, o questionário de autoavaliação D e o certificado de conformidade estão disponíveis a pedido.


## 20. Como posso solicitar uma licença de avaliação da I/O Runtime?

Você pode solicitar uma licença de avaliação para usar a I/O Runtime [aqui](https://adobeio.typeform.com/to/obqgRm).
