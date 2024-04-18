---
title: Monitoramento de usuários em tempo real para o Edge Delivery Services Forms
description: O monitoramento do usuário em tempo real para o Edge Delivery Services Forms envolve o rastreamento e a análise contínuos das interações do usuário com os formulários.
feature: Edge Delivery Services
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# Monitoramento de usuários em tempo real para o Edge Delivery Services Forms

O Adobe Experience Manager usa o Monitoramento de usuário real (RUM) para entender as interações do visitante com sites orientados pela Adobe Experience Manager. Ele ajuda a diagnosticar os desafios de desempenho e medir a eficácia do experimento. O Monitoramento de usuário real mantém a privacidade do visitante usando as técnicas de amostragem, garantindo que nenhuma informação pessoal seja coletada pelos sites que você está visitando. Não é permitido adicionar dados pessoais à coleção de dados do RUM. O monitoramento de usuário real no Adobe Experience Manager foi projetado para preservar a privacidade do visitante e minimizar a coleta de dados.

## Vantagens de usar o monitoramento de usuário em tempo real para o Edge Delivery Services Forms {#advantages}

O AEM usa monitoramento de usuário em tempo real para o seguinte:

* Para identificar e corrigir gargalos de desempenho nos sites.
* Para estimar o número de exibições de página para sites do cliente
* Para compreender a interação do Adobe Experience Manager com o Analytics, o direcionamento ou as bibliotecas externas na mesma página, melhorando a compatibilidade.

## Pré-requisitos

Você pode exibir o painel de monitoramento do usuário em tempo real para o Edge Delivery Services Forms acessando o seguinte URL: https://data.aem.live/?ext=forms

![Tela de logon do RUM para o Edge Delivery Services Forms ](/help/edge/assets/rum-login-screen.png)

Para fazer logon no painel de monitoramento do usuário em tempo real para o Edge Delivery Services Forms, digite o seguinte:
* **URL**: o URL é específico do site ou domínio do usuário. Os usuários têm a opção de filtrar o site ou domínio para exibir o painel de acordo com seus requisitos.
* **Chave de domínio**: o usuário gera manualmente a chave do domínio. Para obter assistência ou dúvidas, consulte [Gerar Chave de Domínio RUM](https://aemcs-workspace.adobe.com/rum/generate-domain-key) documentação.

### Painel de monitoramento do usuário em tempo real para o Edge Delivery Services Forms

Depois de inserir o URL e a chave de Domínio na tela de logon, você obtém acesso ao painel de monitoramento do usuário em tempo real para o Edge Delivery Services Forms.

A ilustração abaixo demonstra o painel RUM para o Edge Delivery Services Forms:

![Painel do RUM Forms](/help/edge/assets/rum-forms-dashboard.png)

### Métricas principais diferentes do painel de RUM para o Forms {#different-metrics-rum-dashboard-forms}

Você pode avaliar as interações do visitante com sites orientados pela Adobe Experience Manager usando as seguintes métricas principais:

* **Formviews**: é o número total de formulários renderizados para uma URL dentro do intervalo de datas especificado.
* **Formsubmit**: é o número total de formulários enviados para uma URL dentro do intervalo de datas especificado.
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
