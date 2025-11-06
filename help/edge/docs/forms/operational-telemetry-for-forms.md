---
title: Telemetria operacional do Edge Delivery Services para o AEM Forms as a Cloud Service
description: A Telemetria operacional do Edge Delivery Services para AEM Forms as a Cloud Service envolve o rastreamento e a análise contínuos das interações do usuário com formulários.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Developer
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# Telemetria operacional do Edge Delivery Services para o AEM Forms as a Cloud Service

A Telemetria operacional permite que você obtenha insights do mundo real sobre como os visitantes interagem com seus sites do Adobe Experience Manager (AEM). Essa ferramenta integrada fornece dados valiosos para entender o comportamento do usuário, diagnosticar problemas de desempenho e medir a eficácia dos experimentos do site. A Telemetria Operacional vai além do teste sintético, capturando as interações de Uso Real, oferecendo uma imagem mais precisa do desempenho do seu site.

No entanto, a Telemetria operacional prioriza a privacidade do visitante. Ele utiliza técnicas de amostragem para coletar dados de um subconjunto representativo de usuários, garantindo que nenhuma informação de identificação pessoal (PII) seja capturada. Além disso, a Telemetria Operacional foi projetada tendo em mente a minimização de dados, coletando apenas as métricas essenciais necessárias para a análise de desempenho. Essa abordagem permite otimizar os sites do AEM, mantendo a confiança do usuário.


## Pré-requisitos

Você pode exibir o painel de monitoramento do Edge Delivery Services para AEM Forms as a Cloud Service acessando o seguinte URL:

https://data.aem.live/?ext=forms

![Tela de Logon de Telemetria Operacional para Edge Delivery Services para Forms](/help/edge/assets/rum-login-screen.png)

Para fazer logon no painel de monitoramento do Edge Delivery Services para AEM Forms as a Cloud Service, digite o seguinte:

- **URL**: a URL é específica para o site ou domínio do usuário. Os usuários têm a opção de filtrar o site ou domínio para exibir o painel de acordo com seus requisitos.

- **Chave de Domínio**: o usuário gera manualmente a chave de domínio. Para obter chaves de domínio para seus formulários, entre em contato com o representante da Adobe.

### Painel de monitoramento do Edge Delivery Services para AEM Forms as a Cloud Service

Depois de inserir o URL e as chaves do domínio na tela de logon, você obtém acesso ao painel de monitoramento do Edge Delivery Services para AEM Forms as a Cloud Service.

A ilustração abaixo demonstra o painel do Edge Delivery Services para AEM Forms as a Cloud Service:

![Painel de Telemetria Operacional do Forms](/help/edge/assets/rum-forms-dashboard.png)

### Métricas principais diferentes do painel do Forms {#different-metrics-operational-telemetry-dashboard-forms}

Esse painel fornece os principais insights sobre como os visitantes interagem com formulários no site do Adobe Experience Manager (AEM). Ao monitorar essas métricas, é possível identificar áreas de aprimoramento e otimizar seus formulários para obter uma melhor experiência do usuário e taxas de conversão:

- **Exibições de formulário**: controle o número total de vezes que os formulários são exibidos
- **Envios de formulário**: rastreia o número total de envios concluídos

- **Maior Pintura de Conteúdo**: mostra a velocidade com que a URL é carregada, indicando o tempo necessário para renderizar o maior elemento de conteúdo visível na janela de visualização a partir do momento em que o usuário solicita a URL. Esse maior elemento de conteúdo pode ser uma imagem, vídeo ou um elemento de texto substancial em nível de bloco. As classificações de desempenho para a velocidade de carregamento do URL são categorizadas da seguinte maneira:
   - **Bom**: se o tempo de carregamento for 2,5 segundos ou menos.
   - **OK**: se o tempo de carregamento for superior a 2,5 segundos, mas igual ou inferior a 4 segundos.
   - **Incorreto**: se o tempo de carregamento exceder 4 segundos

- **Deslocamento de layout cumulativo**: mede a soma total de todas as pontuações de deslocamento de layout individuais para cada deslocamento de layout inesperado que ocorre durante toda a vida útil da página. Ela desempenha um papel crucial na identificação do desempenho de uma página, pois quando os elementos da página mudam enquanto um usuário está tentando interagir com eles, a experiência do usuário é ruim. Essa pontuação varia de zero a qualquer número positivo: zero indica que não há deslocamento, enquanto um número mais alto significa mais deslocamentos de layout na página. As métricas de desempenho usadas para avaliar as pontuações de deslocamento de layout são categorizadas da seguinte maneira:

   - **Bom**: se a pontuação de deslocamento de layout for 0,1 ou menos.
   - **OK**: se a pontuação de deslocamento de layout for maior que 0,1, mas igual ou inferior a 0,25.
   - **Incorreto**: se a pontuação de deslocamento de layout exceder 0,25.

- **Interação com a Próxima Pintura**: avalia a rapidez com que uma página reage às interações do usuário, considerando o tempo necessário para a página responder a cliques, toques e entradas de teclado durante a visita de um usuário à página. O valor final é a interação mais longa observada, independentemente de qualquer anomalia. As métricas de desempenho do Interaction to Next Paint são categorizadas da seguinte maneira:
   - **Bom**: se a duração entre as ações do usuário for 200 milissegundos (ms) ou menos.
   - **OK**: se a duração for superior a 200 ms, mas igual ou inferior a 500 ms.
   - **Incorreto**: se a duração exceder 500 ms.

## Insights acionáveis

Ao analisar essas métricas, é possível identificar oportunidades para:

- Simplifique os formulários e reduza o número de campos.
- Melhore a clareza do formulário com instruções e rótulos claros.
- Otimizar o layout do formulário para obter agilidade.
- Resolver problemas técnicos que retardam o carregamento de formulários.

Ao se concentrar nessas áreas, é possível criar formulários mais fáceis de usar e incentivar os visitantes a preenchê-los, resultando em taxas de conversão mais altas.


