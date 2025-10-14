---
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 51%

---
# Diretrizes para colaboração na documentação do Adobe Experience Manager

## Filosofia da documentação

Os usuários do Adobe Experience Manager trabalham em ambientes extremamente competitivos, esforçando-se para criar experiências digitais que as destaquem das de seus concorrentes. Portanto, é crucial que, ao oferecer novas ferramentas avançadas no AEM, o Adobe as complemente com documentação precisa e transparente para permitir que o cliente use imediatamente seu investimento em AEM e potencialize o ROI.

O objetivo é colocar a documentação do AEM nas mãos de seus usuários assim que possível. Portanto, a equipe de documentação do AEM prioriza uma documentação precisa e utilizável, e se esforça para atualizá-la e aprimorá-la continuamente.

## Contribuições à documentação

Para melhorar continuamente a documentação do AEM, toda a comunidade de usuários do AEM é bem-vinda para contribuir em sua elaboração. Seja por meio de pull requests ou problemas, as melhorias na documentação podem ser correções, esclarecimentos, expansões e exemplos adicionais.

## Padrões de documentação

Embora a equipe de documentação do Experience Manager receba contribuições para a documentação do Adobe, qualquer contribuição para a documentação do AEM - na forma de um pull request ou um problema - deve estar em conformidade com os padrões de contribuição e documentação da equipe.

As contribuições que não cumprirem esses padrões poderão ser rejeitadas.

### A equipe de documentação do Experience Manager documenta casos de uso padrão.

A documentação do AEM abrange casos de uso padrão. Casos de uso que não se enquadrarem no escopo de instalação e de uso padrão do produto não farão parte da documentação do AEM.

### A equipe de documentação do Experience Manager geralmente não documenta bugs e suas soluções.

A documentação do AEM abrange casos de uso padrão. Por esse motivo, os bugs, seus efeitos e soluções alternativas não são documentados,

As exceções a essa regra aplicam-se às notas de versão, nas quais problemas conhecidos podem ser listados com possíveis soluções que foram aprovadas pelo Gerenciamento de produtos do AEM.

### As contribuições à documentação não se destinam a responder perguntas técnicas.

Quaisquer ideias para melhorar a documentação do AEM são bem-vindas como contribuições. No entanto, comentários, problemas e pull requests destinam-se somente a *contribuições*, não para responder suas perguntas sobre como usar o AEM, implementar seu projeto do AEM ou resolver problemas técnicos.

Quaisquer dúvidas sobre o uso do AEM ou erros técnicos devem ser notificados por meio do processo normal de suporte no [portal de suporte do Experience Manager](https://experienceleague.adobe.com/pt-br?support-solution=Experience+Manager&lang=pt-BR#home) ou discutidos na [comunidade do Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=pt).

***As contribuições à documentação do AEM não substituem o Suporte ao cliente do Adobe*** e quaisquer contribuições que buscam respostas para perguntas relacionadas a suporte são rejeitadas.

### As contribuições devem mencionar claramente as páginas pertinentes à documentação.

Se você criar um problema para sugerir melhorias na documentação, deverá incluir links para as páginas afetadas. Caso crie um problema usando o link **Editar esta página** em uma página de documentação, o problema será criado automaticamente com um link para a página.

Isso não se aplica a pull requests, que já fazem referência às páginas afetadas.

## Diretrizes de documentação

Quaisquer contribuições à documentação do AEM devem seguir determinadas diretrizes de estilo.

Seguir essas diretrizes facilita a revisão de sua contribuição e, portanto, agiliza a integração à documentação do AEM.

### Idioma e estilo

#### Idioma

* A documentação do AEM foi criada e mantida em inglês americano.
* Mantenha as sentenças o mais simples possível.
* Use linguagem clara e concisa.

Lembre-se de que os leitores da documentação do AEM estão espalhados ao redor do mundo, e não espera-se que sejam falantes nativos ou fluentes em inglês. Evite linguagem coloquial, mantendo-a a mais clara e simples possível.

#### Siga o Manual de estilo da Microsoft®

[Manual de estilo da Microsoft®](https://learn.microsoft.com/en-us/style-guide/welcome/) O é um guia de estilo disponível gratuitamente. Ele se concentra na documentação de softwares, e a documentação do AEM o segue sempre que possível.

### Formatação

| Item | Estilo |
|---|---|
| Elemento ou opção da interface do usuário | **negrito** |
| Nome do arquivo, caminho, entrada do usuário, valores de parâmetro | `monospaced` |
| Código, linha de comando | ```Code Block``` |

### Capturas de tela

As capturas de tela devem ser usadas com critério e somente quando uma descrição textual for insuficiente.

Não use marcadores ou outras anotações em capturas de tela (como quadros vermelhos, setas ou texto). Dessa forma, as capturas de tela são mais fáceis de reutilizar ou replicar em versões localizadas da documentação.

### Referências específicas à versão

Evite referências diretas a uma versão específica em todo o conteúdo da documentação, sempre que possível. Isso torna a documentação mais flexível e extensível para versões futuras.

### Uso do Day, AEM, CQ, CRX

O produto sempre deve ser chamado pelo nome completo **Adobe Experience Manager** pela primeira vez num artigo e pode, em seguida, ser referido como **AEM**.

Não use Day, Day Software, CQ e CRX, exceto quando inevitável, como em nomes de classe ou em referência ao histórico do AEM.
