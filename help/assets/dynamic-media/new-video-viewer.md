---
title: Novo visualizador de vídeo
description: O Novo visualizador de vídeo no Dynamic Media oferece uma experiência aprimorada de reprodução de vídeo com desempenho, acessibilidade e capacidade de configuração aprimorados.
role: User
source-git-commit: f069e2cfaaa3c82a1d2391403b23f1ccf1ec2866
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 2%

---


# Novo visualizador de vídeo no Dynamic Media {#new-video-viewer-dynamic-media}

O novo visualizador de vídeo do Dynamic Media fornece uma experiência de reprodução de vídeo modernizada no Adobe Experience Manager (AEM). Ele oferece uma experiência de exibição consistente e extensível em ambientes de criação, visualização e Sites, enquanto continua a trabalhar com os fluxos de trabalho existentes do Dynamic Media.

Os visualizadores de vídeo existentes no Dynamic Media são compatíveis com os principais requisitos de reprodução, mas fornecem extensibilidade limitada e integração no nível do evento para análises e cenários de integração modernos

O novo visualizador de vídeo lida com essas limitações ao:

* Fornecendo uma experiência de reprodução mais consistente
* Permitir seleção explícita do visualizador
* Emitir eventos de reprodução estruturados para consumo programático
* Suporte à integração com análises e sistemas externos

O visualizador está disponível como uma opção adicional e requer seleção explícita, quando suportado. Ele não substitui automaticamente os visualizadores de vídeo existentes.

O novo visualizador de vídeo destina-se a organizações que exigem uma experiência de vídeo aprimorada e extensível sem interromper as implementações existentes.

> **OBSERVAÇÃO**
>
> O Novo visualizador de vídeo é um recurso de disponibilidade limitada. Você pode habilitá-lo criando um [tíquete de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).


## Como funciona o novo visualizador de vídeo {#how-it-works}

O Novo visualizador de vídeo funciona da seguinte maneira:

1. Um ativo de vídeo é assimilado em uma pasta sincronizada com o Dynamic Media.
2. O vídeo pode ser visualizado na página de detalhes do ativo usando o **Vídeo (novo)**.
3. O Novo Visualizador de Vídeo pode ser selecionado no componente de **Dynamic Media** ao criar páginas de Sites.
4. Durante a reprodução, o visualizador emite eventos estruturados para a janela principal.
5. Modificadores opcionais do visualizador podem ser usados para controlar o comportamento de reprodução.

## Principais diferenças em relação ao visualizador de vídeo existente {#key-differences}

| Área | Descrição |
|------|-------------|
| Disponibilidade do visualizador | Aparece como uma nova opção chamada **Vídeo (novo)** |
| Seleção do visualizador | Deve ser explicitamente selecionado |
| Extensibilidade | Emite eventos de reprodução estruturados |
| Integração | Continua a trabalhar com os fluxos de trabalho atuais do Dynamic Media |

## Pré-requisitos {#prerequisites}

Antes de usar o Novo visualizador de vídeo, verifique se os seguintes pré-requisitos foram atendidos:

| Requisito | Descrição |
|------------|-------------|
| Sincronização com o Dynamic Media | A pasta do ativo deve ser sincronizada com o Dynamic Media. |
| Perfil de vídeo | Um perfil de vídeo deve ser aplicado à pasta. |
| Ativo de vídeo  | Um vídeo deve ser assimilado na pasta. |

O Novo Visualizador de Vídeo está disponível a partir do **AEM as a Cloud Service versão 2025.7.0**.

Para ativar ou desativar o Novo visualizador de vídeo, entre em contato com o Atendimento ao cliente da Adobe.

## Visualizar o novo visualizador de vídeo {#preview}

Execute as seguintes etapas para visualizar o Novo visualizador de vídeo na página de detalhes do ativo:

1. Navegue até **Assets** > **Arquivos** e abra a pasta que contém o ativo de vídeo.
2. Clique no ativo de vídeo para abrir a página de detalhes do ativo.
3. No painel esquerdo, clique em **Visualizadores**.
4. No painel **Visualizadores**, selecione **Vídeo (novo)**.
5. Clique em **URL** para copiar o link de visualização.
   ![Copiar URL](/help/assets/assets/Copy-url1.jpg)

## Usar o novo visualizador de vídeo no Sites {#use-in-sites}

O Novo Visualizador de Vídeo está disponível por meio do componente **Dynamic Media** existente no AEM Sites.

### Adicionar o componente de Mídia dinâmica

Execute as seguintes etapas para adicionar um vídeo usando o componente de Dynamic Media:

1. Abra a página no **editor de sites**.
2. Arraste o componente **Dynamic Media** para o local desejado na página.
3. Selecione o componente **Dynamic Media** na página.
4. Clique no componente para abrir o seletor de ativos.
5. Selecione um ativo de vídeo.

![Arrastar o componente do Dynamic Media](/help/assets/assets/drag-component.jpeg)

### Configurar o visualizador

Execute as seguintes etapas para configurar a predefinição do visualizador:

1. Selecione o componente **Dynamic Media** na página.
2. Clique em **Configurar** na barra de ferramentas do componente.
   ![Abrir configurações do Dynamic Media](/help/assets/assets/configure-asset.png)

3. Na **caixa de diálogo de configurações do Dynamic Media**, selecione **Vídeo (novo)** na lista suspensa **Predefinição do visualizador**.
   ![Selecionar predefinição do visualizador de vídeo (novo)](/help/assets/assets/viewer-preset.jpeg)

4. Insira todos os modificadores necessários no campo **Modificadores do visualizador** (por exemplo, `autoplay=true&muted=true`).
   ![Modificadores do visualizador](/help/assets/assets/additional-modifiers.jpeg)

5. Salve as alterações.

O vídeo é carregado na página usando o Novo visualizador de vídeo.

> **Observação:** o Novo Visualizador de Vídeo não substitui automaticamente os vídeos existentes. Os usuários devem selecionar manualmente o **Vídeo (novo)** na **Predefinição do Visualizador** ao usar o componente do Dynamic Media ou atualizar as URLs diretas para apontar para o Novo Visualizador de Vídeo onde necessário.

### Migração de vídeos usando URLs diretos

Se os vídeos forem acessados por URLs diretos, em vez do componente de Mídia dinâmica, você poderá alterná-los para o Novo visualizador de vídeo, atualizando o URL. Por exemplo: `https://s7d1.scene7.com/dmviewers/html5/VideoViewer.html?asset=<video-asset>`

## Modificadores do visualizador {#viewer-modifiers}

Os modificadores do visualizador permitem controlar o carregamento de ativos, o comportamento de reprodução, a seleção do formato de transmissão e a apresentação do visualizador.

| Modificador | Descrição |
|--------|-------------|
| `asset` | Especifica a ID do ativo do vídeo ou do Conjunto de vídeos adaptados. |
| `posterimage` | Especifica a imagem exibida antes do início da reprodução. |
| `serverurl` | Especifica o caminho raiz do Servidor de imagens. |
| `contenturl` | Especifica o caminho raiz do conteúdo. |
| `videoserverurl` | Especifica o caminho raiz do servidor de vídeo. |
| `sources.dash` | Especifica o URL do manifesto DASH para reprodução. |
| `sources.hls` | Especifica o URL do manifesto do HLS para reprodução. |
| `autoplay=true` | Inicia a reprodução automaticamente quando o vídeo é carregado. |
| `controls=true/false` | Mostra ou oculta os controles de reprodução de vídeo. |
| `loop=true` | Reinicia a reprodução automaticamente após o vídeo terminar. |
| `muted=true` | Inicia a reprodução em estado de mudo ativado. |
| `playbackrates` | Especifica as opções de velocidade de reprodução disponíveis. |
| `playback` | Especifica o formato de fluxo (automático, hls, traço ou progressivo). |
| `progressivebitrate` | Especifica a taxa de bits para a reprodução progressiva. |
| `initialbitrate` | Especifica a taxa de bits inicial para a transmissão adaptável. |
| `isletterboxed=true/false` | Controla se o vídeo é ampliado ou letterbox. |
| `customcss` | Especifica um arquivo CSS personalizado para o estilo do visualizador. |
| `transition` | Especifica o comportamento de transição mostrar ou ocultar para controles do visualizador. |

Os modificadores são especificados como parâmetros de consulta no campo **Modificadores do visualizador**.

## Eventos compatíveis {#supported-events}

O Novo visualizador de vídeo emite os seguintes eventos durante a reprodução:

| Tipo de evento | Descrição |
|-----------|-------------|
| play | O vídeo começa a ser executado |
| pause | O vídeo está pausado |
| buscar | O usuário busca no vídeo |
| carregar | O vídeo está carregado |
| fechar | O player está fechado |
| metadados | Metadados como duração |
| marco | Marco de reprodução atingido |
| current_time | Posição de reprodução periódica |
| fullscreen | Entrar na tela cheia |
| un_fullscreen | Sair da tela cheia |

## Manipular eventos na janela principal {#handling-events}

O Novo visualizador de vídeo envia mensagens relacionadas à reprodução para a página principal durante as interações do vídeo.

Para lidar com esses eventos, o aplicativo pai deve acompanhar os eventos de mensagem do navegador e validar a origem da mensagem antes de processar os dados.

A carga útil do evento inclui informações como tipo de evento, estado da reprodução, tempo de reprodução atual e metadados adicionais. Esses eventos podem ser usados para oferecer suporte ao rastreamento de análises, interações personalizadas ou integração com sistemas externos.

A Adobe recomenda validar a origem da mensagem para garantir que os eventos sejam processados somente de domínios confiáveis do Dynamic Media.

## Relatório de engajamento com o vídeo para o novo visualizador de vídeo {#video-engagement-report}

O Relatório de engajamento com o vídeo fornece métricas de análise para vídeos reproduzidos usando o Novo visualizador de vídeo no Dynamic Media. O relatório fornece dados de desempenho agregados para o mês especificado e suporta relatórios mensais.

Os relatórios são gerados mediante solicitação. Para solicitar um relatório, crie um [tíquete de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) e forneça os seguintes detalhes:

* Mês do relatório - especifique o mês para o qual o relatório é necessário (por exemplo, janeiro de 2026).
* Endereço de email de entrega - Endereço de email do grupo (recomendado) ou indivíduo para entregar o relatório

O relatório fornece métricas de envolvimento por vídeo, incluindo exibições, impressões, tempo de observação, taxa de conclusão e pontuação de engajamento.

### Formato do relatório

* Os relatórios são entregues em formato CSV.
* Cada linha representa um único vídeo.
* As métricas são agregadas para o período de relatório selecionado.
* Os ativos excluídos são excluídos do relatório.
* Suporta filtragem por `tenant_name`.

### Campos de relatório

O Relatório de engajamento com o vídeo inclui os seguintes campos:

| Texto | Descrição | Cálculo |
|-------|------------|-------------|
| `video_id` | Identificador de vídeo exclusivo. | ND |
| `video_name` | Nome do ativo de vídeo. | ND |
| `video_created_date` | Data de criação do vídeo. | ND |
| `duration_in_seconds` | Duração do vídeo em segundos. | ND |
| `video_views` | Número total de eventos de reprodução de vídeo durante o período de relatório selecionado. | ND |
| `video_impressions` | Número total de vezes que o vídeo foi carregado. | ND |
| `video_watched_seconds` | Total de segundos assistidos em todos os eventos de reprodução. | Soma de segundos assistidos em todos os eventos de reprodução |
| `play_rate` | Porcentagem de reprodução de vídeo em relação a cargas de vídeo. | (`video_views` ÷ `video_impressions`) × 100 |
| `avg_time_watched_in_seconds` | Média de segundos observados por visualização. | `video_watched_seconds` ÷ `video_views` |
| `avg_completion_rate` | Porcentagem de exibições que atingiram a conclusão completa do vídeo. | (Exibições concluídas ÷ `video_views`) × 100 |
| `engagement_score` | Percentual médio de observação em todos os eventos de reprodução. | (Porcentagem total de linhas do tempo de vídeo visualizadas em todas as sessões ÷ `video_views`). |
| `tenant_name` | Identificador da empresa ou locatário associado aos dados. | ND |

## Perguntas frequentes {#faq-video-engagement}

+++Se um vídeo estiver definido para reprodução automática, ele é contado como uma exibição automaticamente ou somente depois que o usuário assiste por uma duração mínima?

A reprodução automática é contabilizada como visualização de vídeo. A reprodução iniciada automaticamente é registrada como uma visualização.

+++

+++Se um usuário assistir apenas parte de um vídeo (por exemplo, os primeiros 2 segundos e os últimos 2 segundos de um vídeo de 10 segundos), ele será contado como uma exibição concluída?

Uma visualização é contabilizada como concluída quando a reprodução atinge o fim da linha do tempo do vídeo, mesmo se partes do vídeo foram ignoradas.

+++

+++Se um usuário movimentar-se para trás e assistir novamente partes do vídeo, isso aumenta a contagem de video_views, a pontuação de envolvimento ou ambos?

Assistir novamente a partes do vídeo não aumenta a contagem de video_views. A reprodução adicional contribui para a engagement_score.

+++

+++Se o mesmo usuário assistir ao mesmo vídeo várias vezes sem recarregar a página, como video_views e engagement_score são calculados?

A reprodução repetida sem recarregar a página não aumenta a contagem de video_views. A reprodução adicional contribui para a engagement_score.

+++

+++Pausar e retomar um vídeo afeta o rastreamento do engajamento ou o cálculo da taxa de conclusão?

Pausar e retomar a reprodução não afeta o rastreamento do engajamento ou o cálculo da taxa de conclusão.

+++
