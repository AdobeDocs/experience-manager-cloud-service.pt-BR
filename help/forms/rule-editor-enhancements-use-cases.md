---
title: Este artigo descreve vários casos de uso para o editor de regras em um Formulário adaptável com base nos Componentes principais.
description: Este artigo explora vários casos de uso para o editor de regras em um Formulário adaptável com base nos Componentes principais. Ela também destaca como as funções personalizadas podem ser usadas para criar regras personalizadas para formulários.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 062ed441-6e1f-4279-9542-7c0fedc9b200
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 0%

---

# Aprimoramentos do editor de regras e casos de uso

<span class="preview"> Estes são recursos de pré-lançamento disponíveis em nosso <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features">canal de pré-lançamento</a>. Essas melhorias também se aplicam ao Edge Delivery Services Forms.

Este artigo apresenta os últimos aprimoramentos feitos ao editor de regras no Adaptive Forms. Essas atualizações foram projetadas para ajudá-lo a definir o comportamento do formulário com mais facilidade, sem escrever código personalizado, e para criar experiências de formulário mais dinâmicas, responsivas e personalizadas.

A tabela abaixo lista as melhorias recentes feitas ao editor de regras no Adaptive Forms, juntamente com uma breve descrição e as principais vantagens de cada recurso:

| Aprimoramento | Descrição | Vantagens |
|---|----|---|
| [Validação usando o método validate()](#validate-method-in-function-list) | Disponível na lista de funções para validar campos individuais, painéis ou o formulário inteiro. | - Validação granular no nível de painel, campo ou formulário <br> - Melhor experiência do usuário com mensagens de erro direcionadas <br> - Impede a progressão com dados incompletos <br> - Reduz erros de envio de formulário |
| [Baixar documento de registro](#download-document-of-record) | Função integrada disponível no editor de regras para baixar o Documento de registro (DoR). | - Não é necessário desenvolvimento personalizado para baixar o DoR <br> - Experiência de download consistente em todos os formulários |
| [Variáveis dinâmicas](#support-for-dynamic-variables-in-rules) | Crie regras usando variáveis que são alteradas com base na entrada do usuário ou em outras condições. | - Habilita condições de regra flexíveis <br> - Reduz a necessidade de lógica duplicada <br> - Elimina a necessidade de criar campos ocultos |
| [Regras personalizadas baseadas em eventos](#custom-event-based-rules-support) | Defina regras que respondam a eventos personalizados além dos acionadores padrão. | - Oferece suporte a casos de uso avançados <br> - Maior controle sobre quando e como as regras são executadas <br> - Melhora a interatividade |
| [Execução do painel repetível com reconhecimento de contexto](#context-based-rule-execution-for-repeatable-panels) | As regras agora são executadas no contexto correto para cada painel repetido, em vez de somente na última instância. | - Aplicativo de regra preciso para cada instância de repetição <br> - Reduz erros nas seções dinâmicas <br> - Melhora a experiência do usuário com conteúdo repetido |
| [Suporte para cadeia de caracteres de consulta, UTM e parâmetros do navegador](#url-and-browser-parameter-based-rules-in-adaptive-forms) | Crie regras que adaptam o comportamento do formulário com base em parâmetros de URL ou valores específicos do navegador. | - Habilita a personalização com base na origem ou no ambiente <br> - Útil para fluxos de marketing ou específicos de rastreamento <br> - Não há necessidade de script extra ou personalização |

>[!NOTE]
>
> As melhorias também se aplicam ao [Editor de regras do Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

Agora vamos explorar cada método detalhadamente com casos de uso específicos para ajudar você a entender como esses recursos podem ser usados para fornecer uma experiência personalizada para os usuários

## Validar Método na Lista de Funções

Recursos de validação aprimorados que permitem que o método **validate()** seja usado na lista de funções para validar painéis, campos ou formulários inteiros. Por exemplo, em um formulário de aplicativo de empréstimo de várias etapas, é necessário validar seções diferentes antes de permitir que os usuários sigam para a próxima etapa.

**Cenário:** uma instituição financeira oferece um formulário de aplicativo de empréstimo em várias etapas, no qual os usuários devem preencher diferentes seções, como:

* Informações pessoais
* Detalhes do Emprego
* Detalhes do empréstimo
* Revisar e enviar

Antes de um usuário mudar de uma etapa para a próxima, o formulário deve validar somente os campos dentro da seção atual. Por exemplo, o usuário não deve ter permissão para continuar com &quot;Detalhes do emprego&quot;, a menos que todos os campos obrigatórios em &quot;Detalhes pessoais&quot; estejam preenchidos corretamente.

**Implementação usando validate() no Editor de Regras**

Um botão **Próximo** em cada painel aciona uma regra usando o método **validate()**. A regra verifica se todos os campos no painel atual são válidos. Se a validação for aprovada, o formulário navegará para o próximo painel. Caso contrário, serão exibidas mensagens de erro orientando o usuário a corrigir a entrada.

A captura de tela abaixo exibe a regra aplicada ao botão **Avançar**:

![Botão Validar Próximo](/help/forms/assets/validate-next.png)

Na regra acima, o botão **Avançar** verifica se os campos na seção **Detalhes Pessoais** são válidos. Se os detalhes não forem válidos, o foco será movido para o campo **Nome** no painel **Detalhes Pessoais**.

![saída](/help/forms/assets/valid-output.png)

>[!NOTE]
>
>Você pode usar o método **validate()** em formulários, fragmentos ou campos individuais. Quando um fragmento é incluído em um formulário, o formulário e o fragmento são exibidos como opções no contexto de validação. Nesse caso, o fragmento se refere aos campos dentro dele, enquanto o formulário se refere ao formulário principal no qual o fragmento é incorporado.

## Baixar documento de registro

Usar a função pronta para uso (OOTB) **DownloadDor()** no Editor de regras permite que o usuário baixe o Documento de registro, se o formulário estiver configurado para gerar o Documento de registro.

>[!NOTE]
>
>Se o formulário não estiver configurado para o Documento de Registro, uma mensagem de erro será exibida quando a regra que usa a função **downloadDoR()** for aplicada ao botão.

**Cenário**: uma agência governamental fornece um formulário de inscrição digital para a emissão de certificados. Depois de enviar o formulário, os candidatos geralmente exigem uma cópia do formulário preenchido para seus registros ou para compartilhar com outro departamento. Para melhorar a experiência do usuário, a agência quer dar aos candidatos a opção de baixar um Documento de Registro (DoR) imediatamente após o envio ou em qualquer estágio antes do envio final.

**Implementação usando DownloadDor() no Editor de Regras**

Um botão **Download** é adicionado ao formulário usando o Editor de Regras. Uma regra é configurada para acionar a função **DownloadDor()** quando o botão é clicado.

A captura de tela abaixo exibe a regra aplicada ao botão **Baixar**:

![Regra do botão Baixar](/help/forms/assets/download-button-rule.png)

>[!NOTE]
>
> O campo **Entrada** permite que o usuário especifique o nome de arquivo para um documento baixável. Esse é um parâmetro opcional.

Se o formulário estiver configurado para geração DoR, essa função gerará e baixará o PDF instantaneamente, sem exigir nenhuma função personalizada.

![Documento de registro](/help/forms/assets/download-dor-output.png)

## Compatibilidade com variáveis dinâmicas em regras

O editor de regras aprimorado é compatível com a criação e o uso de variáveis dinâmicas (temporárias). Essas variáveis podem ser definidas e recuperadas no ciclo de vida do formulário usando as funções internas **Definir Valor da Variável** e **Obter Valor da Variável**.
Estas variáveis:

* Não são enviados com os dados de formulário.
* Pode conter valores intermediários ou calculados.
* Pode ser usado em lógica condicional e ações.

**Cenário**: um formulário de compras online permite que os usuários selecionem um produto, insiram uma quantidade e escolham um país para remessa. O preço do produto é um valor fixo capturado por meio de um campo de formulário, enquanto o encargo de remessa varia dinamicamente, dependendo do país selecionado.

Para evitar a desorganização do formulário com campos ocultos, a empresa decide armazenar o custo de envio em uma variável temporária e usá-lo para cálculos em tempo real.

**Implementação usando as funções Definir Valor da Variável e Obter Valor da Variável no Editor de Regras**

>[!VIDEO](https://video.tv.adobe.com/v/3471607/get-set-variable-final-video/?quality=12&learn=on)

Uma regra é configurada no fragmento **Address** usando a função **Set Variable Value** para atribuir uma variável temporária chamada **extracharge**. O valor dessa variável muda dinamicamente com base no país selecionado. Por exemplo:

* Se o usuário selecionar Estados Unidos, **extracharge** será definido como 500.
* Para qualquer outro país, **extracharge** está definido como 100.

![Definir valor da variável](/help/forms/assets/setvalue.png)

Posteriormente, quando o **Custo Total de Remessa** for calculado, a função **Obter Valor da Variável** será usada para recuperar o valor de **extracharge**. Este valor é adicionado ao **Preço do Produto × Quantidade do Produto** para calcular o valor final a pagar no clique de botão.

![Obter valor de variável](/help/forms/assets/getvalue.png)

O campo **Custo Total da Remessa** é atualizado dinamicamente para refletir o custo do produto e o encargo da remessa conforme o usuário altera o país ou a quantidade.
![saída](/help/forms/assets/getsetvalue-output.png)

>[!NOTE]
>
> Você também pode adicionar a função **Obter valor da variável** na condição Quando.
> &#x200B;> ![Função Get Variable Value em When condition](/help/forms/assets/when-get-variable.png){width=50%,height=50%, align=center}

Essa abordagem permite cálculos dinâmicos em tempo real sem adicionar campos extras ao formulário, mantendo a estrutura limpa e fácil de usar.

## Suporte a regras baseadas em eventos personalizados

O editor de regras aprimorado oferece suporte à manipulação personalizada de eventos usando as funções **Evento de Despacho** e **Evento de Acionamento**. Essas funções permitem que diferentes partes do formulário se comuniquem emitindo e ouvindo eventos personalizados, permitindo uma lógica modular mais limpa sem associar ações firmemente a campos específicos.

**Cenário**: um formulário de logon é criado usando um fragmento de logon reutilizável que contém os campos **Inserir nome de usuário** e **Inserir senha**. Quando um usuário fornece credenciais válidas, o formulário valida a entrada e inicia o processo **Obter OTP**. Depois que o usuário insere um OTP válido, ele é redirecionado para a página apropriada.

Em vez de associar a lógica diretamente aos campos, o formulário usa uma abordagem baseada em eventos com **Evento de Despacho** e **Evento de Acionador** para melhorar a modularidade e a capacidade de manutenção.

**Implementação usando Evento de Despacho e Evento On Trigger**


>[!VIDEO](https://video.tv.adobe.com/v/3471610/dispatch-trigger-final/?quality=12&learn=on)

O fragmento de logon é adicionado ao formulário, contendo campos predefinidos para Nome de usuário e Senha. Uma regra está configurada no botão **Obter OTP** para exibir o **Painel de Validação**, que inclui o campo de entrada para inserir e validar o OTP.

![Obter Regra OTP](/help/forms/assets/get-otp-rule.png)

No **Painel de Validação**, uma regra é configurada no botão Validar. A integração de API é usada para validar o OTP inserido no campo **Inserir OTP**. Se a validação for bem-sucedida, um **Evento de Despacho** chamado **LoggedIn** será acionado com a carga do evento contendo a resposta da API.

![Na regra de evento do gatilho](/help/forms/assets/trigger-event-rule.png)

No nível de formulário, uma regra é configurada para escutar o evento **LoggedIn**. Quando esse evento é acionado, a regra exibe a mensagem de redirecionamento e leva o usuário para a página do painel.

![regra de evento de expedição](/help/forms/assets/dispatch-event-rule.png)

Quando o usuário envia o formulário com as credenciais corretas e um OTP válido, o logon é bem-sucedido e o usuário é redirecionado para o painel.

Suporte para eventos personalizados que permitem aos desenvolvedores criar e acionar eventos personalizados que podem ser usados como condições no editor de regras.

## Execução de regras baseadas em contexto para painéis repetíveis

O Forms adaptável oferece suporte à execução de regras sensíveis ao contexto para painéis repetíveis. Isso permite que as regras sejam aplicadas especificamente à instância do painel em que o usuário interage, em vez de afetar todas as instâncias ou padronizar para a última.

**Cenário**: um formulário de pedido de produto permite que os usuários adicionem vários produtos em painéis separados. Cada painel inclui um campo **Número do Produto** e um campo **Custo Total**. Quando um usuário atualiza a quantidade de um produto, o formulário deve recalcular o preço total, mas somente para esse painel específico, não para todos os outros.

**Implementação usando Regras sensíveis ao contexto no Editor de Regras**

Uma regra é configurada no campo **Número do Produto**, dentro do painel do produto repetível.

A captura de tela abaixo exibe a regra para o campo **Número do Produto** dentro do painel do produto repetível:

![número de regra de produto](/help/forms/assets/number-of-product-rule.png)

Quando a quantidade é alterada, a regra busca o preço unitário do produto selecionado e calcula o custo total somente para esse painel.

![Saída de regra sensível ao contexto](/help/forms/assets/context-aware-rule-output.png)

## Regras baseadas em parâmetros de URL e navegador no Adaptive Forms

O Forms adaptável é compatível com a execução de regras dinâmicas usando parâmetros externos transmitidos pela URL do formulário ou derivados do ambiente de navegador do usuário. Isso permite experiências de formulário personalizadas e com reconhecimento de contexto com base na origem do visitante ou em qual dispositivo ele está usando.

## Tipos de Parâmetros Permitidos

| Tipo de parâmetro | Opções suportadas | Descrição | Exemplo de valor |
| --- | --- | --- | ---|
| Parâmetro da consulta | `ref` (somente valores de cadeia de caracteres) | Par de valor-chave genérico na URL após `?` | `?ref=partner123` |
| Parâmetro UTM | UTM Source<br>UTM Medium<br>UTM Campaign<br>UTM Term<br>UTM Content | Parâmetros de consulta especiais usados para rastreamento da campanha | `?utm_source=google&utm_medium=email` |
| Parâmetro de URL | Nome do host<br>Caminho | Extrai componentes estruturais do URL do formulário | `hostname=www.example.com`, `path=/signup` |
| Parâmetro do Navegador | Agente do Navegador<br>Idioma do Navegador<br>Plataforma do Navegador | Valores derivados do navegador ou dispositivo do usuário | `Browser Agent=Mozilla`, `Language=en-US` |

**Cenário**: um formulário de geração de clientes potenciais precisa ajustar sua mensagem de boas-vindas dependendo da fonte de tráfego. Quando um usuário acessa o formulário por meio de uma campanha de publicidade do Google (usando utm_source=google no URL), o formulário deve mostrar uma saudação personalizada.

**Implementação usando parâmetro UTM**

Uma regra é configurada em um campo de texto que exibe uma mensagem personalizada para usuários do Google e usa o parâmetro **utm_source**.

A captura de tela abaixo exibe a regra configurada na mensagem de texto:

![regra na mensagem de texto](/help/forms/assets/utm-param-rule.png)

Se o valor do parâmetro **utm_source** for igual a &quot;google&quot;, uma mensagem personalizada será exibida como &quot;Olá, usuários do Google, bem-vindos ao Anúncio da campanha!&quot; é exibido.

![utm-param-output](/help/forms/assets/utm-param-output.png)

Isso permite que os profissionais de marketing forneçam conteúdo relevante aos usuários com base na campanha que os trouxe para o formulário sem precisar de entrada manual de campo ou script personalizado.

Esses aprimoramentos expandem significativamente os recursos do Editor de regras do Adaptive Forms, fornecendo aos desenvolvedores ferramentas poderosas para criar formulários mais dinâmicos, interativos e inteligentes. Cada aprimoramento atende a necessidades específicas de negócios, mantendo a facilidade de uso que torna o Editor de regras acessível a usuários técnicos e não técnicos.

## Recursos adicionais

{{see-also-rule-editor}}
