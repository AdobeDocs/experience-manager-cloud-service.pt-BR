---
title: Monitoramento de usuário real para Edge Delivery Services para AEM Forms as a Cloud Service
description: O monitoramento real do usuário para Edge Delivery Services para AEM Forms as a Cloud Service envolve o rastreamento e a análise contínuos das interações do usuário com os formulários.
feature: Edge Delivery Services
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 4a534f4335376673c362ef91a877e67a523be560
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---


# Monitoramento de usuário real para Edge Delivery Services para AEM Forms as a Cloud Service

O Monitoramento de usuário real (RUM) possibilita que você obtenha insights reais sobre como os visitantes interagem com seus sites do Adobe Experience Manager (AEM). Essa ferramenta integrada fornece dados valiosos para entender o comportamento do usuário, diagnosticar problemas de desempenho e medir a eficácia dos experimentos do site. O RUM vai além dos testes sintéticos, capturando interações reais do usuário e oferecendo uma imagem mais precisa do desempenho do site.

No entanto, o RUM prioriza a privacidade do visitante. Ele utiliza técnicas de amostragem para coletar dados de um subconjunto representativo de usuários, garantindo que nenhuma informação de identificação pessoal (PII) seja capturada. Além disso, o RUM foi projetado com a minimização de dados em mente, coletando apenas as métricas essenciais necessárias para a análise de desempenho. Essa abordagem permite otimizar seus sites AEM, mantendo a confiança do usuário.


## Pré-requisitos

É possível exibir o painel de monitoramento do Edge Delivery Services para AEM Forms as a Cloud Service acessando o seguinte URL:

https://data.aem.live/?ext=forms

![Tela de logon do RUM para Edge Delivery Services para Forms](/help/edge/assets/rum-login-screen.png)

Para fazer logon no painel de monitoramento do Edge Delivery Services para o AEM Forms as a Cloud Service, digite o seguinte:

* **URL**: o URL é específico do site ou domínio do usuário. Os usuários têm a opção de filtrar o site ou domínio para exibir o painel de acordo com seus requisitos.

* **Chave de domínio**: o usuário gera manualmente a chave do domínio.

Para obter assistência com as chaves de Domínio, consulte a [Autenticação](https://www.aem.live/developer/rum#authentication) documentação.

### Painel de monitoramento do Edge Delivery Services para AEM Forms as a Cloud Service

Depois de inserir o URL e as chaves de domínio na tela de logon, você obtém acesso ao painel de monitoramento do Edge Delivery Services para AEM Forms as a Cloud Service.

A ilustração abaixo demonstra o painel RUM para Edge Delivery Services para o AEM Forms as a Cloud Service:

![Painel do RUM Forms](/help/edge/assets/rum-forms-dashboard.png)

### Métricas principais diferentes do painel do Forms {#different-metrics-rum-dashboard-forms}

Esse painel fornece informações importantes sobre como os visitantes interagem com formulários no site do Adobe Experience Manager (AEM). Ao monitorar essas métricas, é possível identificar áreas de aprimoramento e otimizar seus formulários para obter uma melhor experiência do usuário e taxas de conversão:

* **Exibições de formulário**: rastreia o número total de vezes que os formulários são exibidos
* **Envio de formulários**: rastreia o número total de envios concluídos

* **Maior pintura de conteúdo**: mostra a velocidade na qual o URL é carregado, indicando o tempo necessário para renderizar o maior elemento de conteúdo visível na janela de visualização a partir do momento em que o usuário solicita o URL. Esse maior elemento de conteúdo pode ser uma imagem, vídeo ou um elemento de texto substancial em nível de bloco. As classificações de desempenho para a velocidade de carregamento do URL são categorizadas da seguinte maneira:
   * **Bom**: se o tempo de carregamento for de 2,5 segundos ou menos.
   * **Ok**: se o tempo de carregamento for superior a 2,5 segundos, mas igual ou inferior a 4 segundos.
   * **Ruim**: Se o tempo de carregamento exceder 4 segundos

* **Deslocamento de layout cumulativo**: mede a soma total de todas as pontuações de deslocamento de layout individuais para cada deslocamento de layout inesperado que ocorre durante toda a vida útil da página. Ela desempenha um papel crucial na identificação do desempenho de uma página, pois quando os elementos da página mudam enquanto um usuário está tentando interagir com eles, a experiência do usuário é ruim. Essa pontuação varia de zero a qualquer número positivo: zero indica que não há deslocamento, enquanto um número mais alto significa mais deslocamentos de layout na página. As métricas de desempenho usadas para avaliar as pontuações de deslocamento de layout são categorizadas da seguinte maneira:

   * **Bom**: se a pontuação de deslocamento de layout for 0,1 ou menos.
   * **Ok**: se a pontuação de deslocamento de layout for maior que 0,1, mas 0,25 ou inferior.
   * **Ruim**: se a pontuação de deslocamento de layout exceder 0,25.

* **Interação com o Próximo Pintura**: avalia a rapidez com que uma página reage às interações do usuário, considerando o tempo que leva para a página responder a cliques, toques e entradas do teclado durante a visita de um usuário à página. O valor final é a interação mais longa observada, independentemente de qualquer anomalia. As métricas de desempenho do Interaction to Next Paint são categorizadas da seguinte maneira:
   * **Bom**: se a duração entre as ações do usuário for de 200 milissegundos (ms) ou menos.
   * **Ok**: Se a duração for superior a 200 ms, mas igual ou inferior a 500 ms.
   * **Ruim**: Se a duração exceder 500 ms.

## Insights acionáveis

Ao analisar essas métricas, é possível identificar oportunidades para:

* Simplifique os formulários e reduza o número de campos.
* Melhore a clareza do formulário com instruções e rótulos claros.
* Otimizar o layout do formulário para obter agilidade.
* Resolver problemas técnicos que retardam o carregamento de formulários.

Ao se concentrar nessas áreas, é possível criar formulários mais fáceis de usar e incentivar os visitantes a preenchê-los, resultando em taxas de conversão mais altas.