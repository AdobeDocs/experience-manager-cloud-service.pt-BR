---
title: AEM - Integração do Magento usando Perguntas frequentes sobre a estrutura de integração do Commerce
description: AEM - Integração do Magento usando Perguntas frequentes sobre a estrutura de integração do Commerce
translation-type: tm+mt
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# AEM - Integração do Magento usando Perguntas frequentes sobre a estrutura de integração do Commerce


## 1. O GraphQL é usado apenas para Magento ou estará disponível para consultar conteúdo criado AEM JCR?

A Adobe adotou as APIs GraphQL da Magento como sua API de comércio oficial para todos os dados relacionados ao comércio. Portanto, AEM usa o GraphQL para trocar dados de comércio com o Magento e com qualquer mecanismo de comércio por meio do I/O Runtime.

## 2. Como a E/S do Adobe entra em jogo? AEM fala diretamente com a Magento?

AEM pode se conectar diretamente ao Magento sem uma camada de tempo de execução de E/S. Se houver necessidade de integrar um backend de comércio não-Magento (solução de terceiros) ao AEM, a plataforma I/O Runtime poderá ser usada para hospedar a camada de mapeamento para conectar as APIs Magento GraphQL a qualquer APIs de soluções de terceiros. Para obter mais detalhes, consulte esta implementação [de](https://github.com/adobe/commerce-cif-graphql-integration-reference)referência. Para soluções que não sejam de Magento, AEM seria configurado para apontar para o ponto final de I/O Runtime.

A plataforma I/O Runtime também pode ser usada para estender ou personalizar os serviços de comércio. Para esses casos de uso, você chamaria o terminal I/O Runtime que hospedará uma implementação personalizada do respectivo serviço. Casos de uso de integração e extensão podem ser combinados.

## 3. Os ativos do Produto (imagens) podem ser armazenados e referenciados a partir de AEM via Magento admin? Como os ativos da Dynamic Media podem ser consumidos?

Não há atualmente um AEM Assets - integração Magento. Como solução, você pode armazenar ativos de produtos (imagens) em AEM Assets, mas precisará armazenar manualmente os URLs de ativos no Magento. A Dynamic Media agora faz parte dos AEM Assets e vai funcionar da mesma maneira.

## 4. Importa onde o Magento é implantado? (No local ou na nuvem)

Não importa onde o Magento é implantado. A integração e a nova loja AEM Venia funcionarão independentemente do modelo de implantação. No entanto, se for implantado com base na arquitetura de referência E2E aprovada, os testes E2E serão executados em relação aos KPIs de desempenho coletados que representam o perfil de um cliente da empresa. Portanto, isso fornecerá a você informações adicionais que você pode usar como referência.

## 5. Como as páginas de catálogo ou de produto são criadas no AEM? Como eles persistem em AEM?

Páginas de catálogo e páginas de produto são criadas e armazenadas em cache dinamicamente em AEM com base em catálogos genéricos e modelos de página de produto. Nenhum dado de Produto ou Catálogo é importado e armazenado em AEM.

## 6. Você também armazena o preço em cache e outros dados via Dispatcher. Isso levanta um desafio frequente de invalidação do cache?

Dados dinâmicos, como preço ou inventário, não são armazenados em cache no Dispatcher. Os dados dinâmicos são obtidos no cliente com componentes da Web diretamente por meio de APIs GraphQL. Somente dados estáticos (como dados de produto ou categoria) são armazenados em cache no Dispatcher. Se os dados do produto forem alterados, haverá necessidade de invalidação do cache.

## 7. Como a invalidação de cache para AEM Dispatcher funciona com AEM-Magento?

Recomendamos configurar a invalidação de cache baseada em TTL para páginas armazenadas em cache no Dispatcher. Para obter informações dinâmicas, como preço ou ações, recomendamos renderizar a data no cliente. Para obter mais informações sobre a invalidação do cache baseado em TTL, consulte [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 8. Por que você não está usando We.Retail?

O tema Venia (desenvolvido por Magento) é utilizado, primeiro móvel e alinhado com o PWA de Magento. O tema Venia representa os mais recentes termos de estilo CSS e componentes principais AEM.

## 9. Quando você atualiza os dados do produto no Magento, isso é um push em tempo real para AEM? Ou é um processo em lote?

O complemento CIF usado com AEM Cloud Service permite que os dados fluam de Magento para AEM sob demanda. Portanto, este não é um processo de push em tempo real ou em lote quando há uma atualização no Magento.

## 10. Há alguma recomendação sobre a pesquisa unificada AEM conteúdo com Comércio?

Uma implementação de referência de pesquisa de produto é fornecida, mas não há pesquisa unificada com conteúdo. Esse recurso é geralmente muito específico do cliente e melhor resolvido em um nível específico do projeto.

## 11. Como o Search funciona com o AEM-Magento usando o CIF?

O CIF fornece a barra de pesquisa e os componentes de Resultados da pesquisa. O componente da barra de pesquisa envia uma solicitação GraphQL com o termo de pesquisa para Magento. O Magento retorna uma lista de produto que inclui nome de produto, preço, SLUG etc. O componente de Resultado da pesquisa exibe os resultados da pesquisa em uma visualização da galeria em uma página de resultados da pesquisa criada no AEM. A Pesquisa suporta pesquisa básica de texto completo. Usamos a chave SLUG/url para criar uma referência ao PDP.

## 11. Como os dados do produto podem ser usados em MSM ou traduções?

Os dados do produto geralmente já são traduzidos no PIM ou no Magento. A integração AEM - Magento suporta a conexão com várias visualizações de Magento e loja. Em uma configuração de MSM, normalmente um site AEM está vinculado a uma visualização da loja de Magento.

## 13. Como o CIF funciona com outras plataformas comerciais?

A integração com soluções de terceiros, como outras soluções de comércio (não-Magento), é feita por meio da plataforma I/O Runtime.  Criámos uma implementação [de](https://github.com/adobe/commerce-cif-graphql-integration-reference) referência para demonstrar como é que isto é feito. Isso permite a reutilização do [AEM CIF Cloud Connector](https://github.com/adobe/commerce-cif-connector) e dos componentes [principais CIF](https://github.com/adobe/aem-core-cif-components) AEM expondo a API Magento GraphQL sobre qualquer plataforma de comércio de terceiros. Para oferta da máxima flexibilidade e escalabilidade, essa camada de integração é implantada na plataforma [](https://www.adobe.io/apis/experienceplatform/runtime.html)Adobe I/O Runtime sem servidor.

## 14. Há alguma maneira de aprimorar os dados do produto com o texto comercial? Onde você faz isso? No AEM ou no Magento?

Existem várias maneiras de conseguir isso e isso dependerá do caso de uso. Uma maneira seria trabalhar com atributos personalizados. Permita que os autores AEM alterem esses campos no editor de produtos AEM e sincronizem os dados de volta ao PIM. Outra opção seria aproveitar AEM Fragmentos de experiência que são inseridos nas páginas do produto.

## 15. A integração entre AEM-Magento muda quando a plataforma Adobe I/O Runtime é usada?

Os clientes que desejam estender os serviços de comércio podem usar as mesmas sequências de ação de integração e gravação hospedadas na plataforma I/O Runtime para injetar a lógica comercial e enriquecer os serviços de comércio.

## 16. Como AEM cria páginas de produtos e catálogos dinamicamente com base em um modelo genérico em AEM, o que eu veria se fosse abrir o CRXDE Lite e verificar o conteúdo? Eu veria uma árvore de produtos inteira baseada nos produtos em Magento? Em caso negativo, como um autor melhoraria essas páginas?

Não há mais páginas de produtos ou catálogos JCR. Ver pergunta 12.

## 17. A SPA armazenará o trabalho principal com AEM editor SPA?

AEM pode ser usado como uma ferramenta de criação para qualquer tipo de frente de loja. Atualmente, a renderização híbrida é usada para a nova frente de loja. No futuro, AEM será usado para criação com SPA e PWA.

## 18. Como o PIM atua nessa estrutura?

Os dados do PIM são expostos a AEM e clientes por meio de solicitações do GraphQL. Nossa recomendação é integrar o PIM ao mecanismo de comércio (Magento ou outro) para que os dados do PIM possam ser recuperados do mecanismo de comércio.

## 19. Como podemos garantir a conformidade do PCI ao usar AEM para a camada de apresentação inteira?

Ao usar AEM na implantação da nuvem do AMS e do Magento, é obrigatório usar métodos de pagamento abstratos. Isso coloca o cliente do navegador em comunicação direta com o provedor do gateway de pagamento para que nenhuma nuvem de Adobe ou Magento segure ou passe os dados do titular do cartão. Esta abordagem oferece cobertura para a conformidade PCI para pilhas técnicas e data centers. No entanto, há outros aspectos que devem ser considerados como totalmente compatíveis com a PCI, como o modo como os funcionários interagem com o sistema e os dados. Para obter mais informações sobre a conformidade com PCI Magento, consulte https://magento.com/pci-compliance

## 20. Como posso solicitar uma licença de avaliação de I/O Runtime?

Você pode solicitar uma licença de avaliação para usar o I/O Runtime [aqui](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md).



