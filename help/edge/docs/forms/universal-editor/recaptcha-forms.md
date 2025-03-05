---
title: Proteja seu Forms com o reCAPTCHA - Um Guia Visual
description: Saiba como adicionar facilmente o Google reCAPTCHA aos formulários do Edge Delivery Services para impedir envios de spam e bot
feature: Edge Delivery Services
keywords: reCAPTCHA em formulários, Uso do reCAPTCHA no Universal Editor, Adição do reCAPTCHA em formulários, segurança de formulários, proteção contra spam
role: Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---


# Proteja seu Forms contra spam com o Google reCAPTCHA

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da sua organização GitHub e o nome do repositório.</span>



## Por que usar reCAPTCHA em seus formulários?

| ![Segurança](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Proteção de bot](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Experiência do usuário](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Segurança aprimorada** | **Prevenção contra spam e bot** | **Experiência de usuário perfeita** |
| Proteja seus formulários contra atividades fraudulentas e ataques mal-intencionados | Impeça que bots automatizados inundem seus formulários com conteúdo irrelevante ou prejudicial | O reCAPTCHA invisível funciona nos bastidores sem interromper os usuários legítimos |

Por exemplo, um formulário de cálculo de imposto com informações financeiras sensíveis precisa de proteção contra uso indevido. O reCAPTCHA verifica se os envios vêm de usuários genuínos, não de sistemas automatizados.

## Escolha sua solução reCAPTCHA

O Edge Delivery Services Forms é compatível com duas opções de reCAPTCHA do Google:

| ![reCAPTCHA Empresa](/help/edge/docs/forms/universal-editor/assets/enterprise.svg) | ![Padrão do reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/standard.svg) |
|:-------------:|:-------------:|
| [**reCAPTCHA Empresa**](#set-up-recaptcha-enterprise) | [**Padrão do reCAPTCHA**](#set-up-recaptcha-standard) |
| Detecção de fraudes premium de nível empresarial com recursos adicionais e personalização | Serviço gratuito com detecção baseada em pontuação que opera de forma invisível em segundo plano |
| Melhor para: grandes organizações com necessidades complexas de segurança | Ideal para: projetos de pequeno a médio porte com necessidades básicas de proteção |

Ambas as opções usam a detecção baseada em pontuação (0,0 a 1,0) para identificar interações humanas versus de bot sem interromper a experiência do usuário.

## Configurar o reCAPTCHA Enterprise

### Etapa 1: Obtenha suas credenciais da Google Cloud

Antes de configurar o reCAPTCHA Enterprise, você precisará:

- Um [projeto do Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) com sua [ID do Projeto](https://support.google.com/googleapi/answer/7014113)
- [reCAPTCHA Enterprise API habilitada](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) para o seu projeto
- Uma [chave de API](https://console.cloud.google.com/apis/credentials) para autenticação
- Uma [chave do site](https://console.cloud.google.com/security/recaptcha) para o seu domínio

### Etapa 2: criar um contêiner de configuração da nuvem

![Configuração de nuvem passo a passo](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Faça logon na instância de autor do AEM
2. Navegue até **Ferramentas** > **Geral** > **Navegador de Configuração**
3. Localize o formulário e selecione **Propriedades**
4. Habilitar **Configurações de Nuvem** na caixa de diálogo
5. Salve e publique sua configuração

### Etapa 3: Configurar o Serviço Corporativo reCAPTCHA

![tela de configuração corporativa do reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Acesse **Ferramentas** > **Serviços na Nuvem** > **reCAPTCHA**
2. Navegue até o formulário e clique em **Criar**
3. Na caixa de diálogo:
   - Selecionar versão **ReCAPTCHA Enterprise**
   - Insira um Título e Nome
   - Adicione a ID do projeto, a chave do site e a chave da API
   - Selecione **Chave do site baseada em pontuação** como Tipo de chave
   - Definir uma pontuação de limite (0-1) para distinguir humanos de bots
4. Clique em **Criar** e publique sua configuração

## Configurar o reCAPTCHA Standard

### Etapa 1: Obtenha suas chaves de API

Antes de iniciar, [obtenha um par de chaves da API reCAPTCHA](https://www.google.com/recaptcha/admin) (Chave do site e Chave secreta) do Console do Google reCAPTCHA.

>[!IMPORTANT]
>
>O Edge Delivery Services Forms só oferece suporte à versão **reCAPTCHA Score based**.

### Etapa 2: criar um contêiner de configuração da nuvem

Siga as mesmas etapas da versão Enterprise para criar e publicar um contêiner de configuração de nuvem.

### Etapa 3: Configurar o Serviço Padrão reCAPTCHA

![Tela de configuração padrão do reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Acesse **Ferramentas** > **Serviços na Nuvem** > **reCAPTCHA**
2. Navegue até o formulário e clique em **Criar**
3. Na caixa de diálogo:
   - Selecionar versão **ReCAPTCHA v2**
   - Insira um Título e Nome
   - Adicionar a chave do site e a chave secreta
4. Clique em **Criar** e publique sua configuração

## Adicionar reCAPTCHA ao formulário

Agora que você configurou o reCAPTCHA, é hora de adicioná-lo ao formulário:

![Adicionando o componente reCAPTCHA a um formulário](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

1. Abra o formulário no Universal Editor
2. Navegue até a seção Formulário adaptável na árvore Conteúdo
3. Clique no ícone **Adicionar** e selecione **Captcha (Invisível)** na lista de Componentes de Formulário Adaptáveis
   - *Como alternativa, arraste e solte o componente no seu formulário*
4. Clique em **Publicar** para atualizar seu formulário com a proteção reCAPTCHA

Seu formulário agora está protegido! Exibir em:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name>`

![Formulário com proteção reCAPTCHA habilitada](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Validação da integração do reCAPTCHA

Depois de adicionar o reCAPTCHA ao formulário, é essencial verificar se ele está funcionando corretamente. Veja como validar sua implementação:

### Verificação visual

Embora o reCAPTCHA v2 (baseado em pontuação) opere de forma invisível, você pode confirmar sua presença ao:

1. **Inspecionar a origem da página**: clique com o botão direito do mouse na página do formulário e selecione &quot;Exibir Source da Página&quot;
   - Procure a inclusão do script reCAPTCHA com a chave do site
   - Exemplo: `<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>`

2. **Verificar Solicitações de Rede**: Usando ferramentas de desenvolvedor de navegador (F12)
   - Envie seu formulário e procure solicitações de rede para `google.com/recaptcha`
   - Essas solicitações indicam que o reCAPTCHA está ativo no formulário

### Teste funcional

Para verificar se o reCAPTCHA está realmente protegendo seu formulário:

1. **Teste de Envio Normal**:
   - Preencha o formulário com dados válidos
   - Enviar o formulário em um ritmo humano normal
   - Verificação do envio do formulário com êxito

2. **Teste de comportamento semelhante a bot**:
   - Abra o formulário em uma janela de navegação incógnita/privada
   - Preencher o formulário extremamente rapidamente (comportamento automatizado)
   - Enviar várias vezes em sequência rápida
   - Se o reCAPTCHA estiver funcionando, esses envios podem ser bloqueados ou sinalizados

3. **Verificar registros de envio de formulário**:
   - Revisar os dados de envio do formulário
   - Cada envio deve incluir uma pontuação reCAPTCHA
   - Pontuações próximas a 1,0 indicam usuários humanos prováveis
   - Pontuações próximas a 0,0 indicam atividade potencial do bot

### Uso do Admin Console do Google reCAPTCHA

Para usuários corporativos, o Google Cloud Console fornece análises detalhadas:

1. Vá para o [Google Cloud Console](https://console.cloud.google.com/)
2. Navegue até **Segurança** > **reCAPTCHA**
3. Selecione a chave do site
4. Revisar os gráficos e as estatísticas de avaliação
5. Procure por:
   - Padrões de tráfego
   - Distribuições de pontuação
   - Atividades potencialmente fraudulentas

Para usuários do reCAPTCHA Padrão, estatísticas básicas estão disponíveis no [reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin/).

### Ajustar sua implementação

Com base nos resultados da validação:

- Se usuários legítimos estiverem sendo bloqueados, considere reduzir sua pontuação de limite
- Se você ainda estiver recebendo spam, considere aumentar sua pontuação limite
- Para problemas persistentes, revise a configuração do reCAPTCHA e verifique se todas as chaves foram inseridas corretamente

Lembre-se de que o reCAPTCHA usa o aprendizado de máquina para melhorar com o tempo, de modo que sua eficácia pode aumentar à medida que ele aprende os padrões de tráfego do site.

## Solução de problemas e perguntas frequentes

| ![Pergunta](/help/edge/docs/forms/universal-editor/assets/question.svg) | ![Resposta](/help/edge/docs/forms/universal-editor/assets/answer.svg) |
|:-------------:|:-------------:|
| **E se eu não criar uma configuração do reCAPTCHA?** | O sistema procurará uma configuração no Contêiner global. Se não houver nenhum, você receberá um erro. |
| **E se eu criar várias configurações?** | O sistema usa automaticamente a primeira configuração criada. |
| **Por que minhas alterações não estão visíveis na URL publicada?** | Certifique-se de republicar o formulário depois de fazer as alterações. |
| **Quais serviços reCAPTCHA têm suporte?** | O Edge Delivery Services Forms só oferece suporte a serviços reCAPTCHA baseados em pontuação. |

## Próximas etapas

Agora que você protegeu seu formulário com o reCAPTCHA:

- **Validar sua implementação**: siga as [etapas de validação](#-validating-your-recaptcha-integration) para garantir que o reCAPTCHA esteja funcionando corretamente
- **Monitorar desempenho**: verifique regularmente se há atividades suspeitas no painel do Google reCAPTCHA e distribuições de pontuação
- **Ajuste as configurações**: ajuste sua pontuação limite com base nas suas necessidades de segurança e feedback de experiência do usuário
- **Mantenha-se atualizado**: mantenha sua implementação do reCAPTCHA atualizada com as últimas recomendações de segurança da Google
- **Prepare sua equipe**: compartilhe conhecimento sobre como o reCAPTCHA funciona e como interpretar as análises
- **Coletar feedback**: Monitore a experiência do usuário para garantir que usuários legítimos não estejam bloqueados

Lembre-se de que a proteção eficaz de formulários é um processo contínuo que requer monitoramento e ajustes regulares.


