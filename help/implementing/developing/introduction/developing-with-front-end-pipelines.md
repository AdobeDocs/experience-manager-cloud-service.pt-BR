---
title: Desenvolver sites com o pipeline front-end
description: O pipeline de front-end melhora a independência do desenvolvedor e acelera o processo de desenvolvimento. Este artigo descreve as principais considerações do processo de build de front-end para garantir desempenho e eficiência ideais.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Developer
recommendations: noDisplay, noCatalog
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---


# Desenvolver sites com o pipeline de front-end {#developing-site-with-front-end-pipeline}

{{traditional-aem}}

O [pipeline de front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) oferece aos desenvolvedores de front-end maior independência e acelera significativamente o desenvolvimento. Este artigo explica como o processo funciona e destaca as principais considerações para ajudar você a aproveitar ao máximo.

>[!TIP]
>
>Se você ainda não estiver familiarizado com como usar o pipeline de front-end e seus benefícios, consulte o guia da [Jornada de Criação rápida de sites](/help/journey-sites/quick-site/overview.md). Ele fornece um exemplo de como implantar um novo site rapidamente e personalizar seu tema independentemente do desenvolvimento de back-end.

## Entender a configuração do pipeline de front-end e o processo de criação no AEM Cloud Manager {#front-end-build-contract}

Semelhante ao [ambiente de compilação de pilha completa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md), o pipeline de front-end tem seu próprio ambiente. Os desenvolvedores têm alguma flexibilidade com esse pipeline, desde que sigam o contrato de build de front-end.

O pipeline de front-end requer que o projeto `Node.js` de front-end use a diretiva de script `build` para gerar a compilação que ele implanta. Este requisito existe porque a Cloud Manager usa o comando `npm run build` para gerar o projeto implantável para a compilação de front-end.

O conteúdo resultante da pasta `dist` é o que o Cloud Manager finalmente implanta, servindo-os como arquivos estáticos. Esses arquivos são hospedados externamente para o AEM, mas são disponibilizados por meio de uma URL `/content/...` no ambiente implantado.

## Versões compatíveis da Node.js {#node-versions}

O ambiente de compilação front-end oferece suporte às seguintes `Node.js` versões:

* 23
* 22
* 20
* 18
* 16
* 14 (padrão)
* 12

Você pode usar a `NODE_VERSION` [variável de ambiente](/help/implementing/cloud-manager/environment-variables.md) para definir a versão desejada.

## Práticas recomendadas para nomear e gerenciar pipelines de front-end no AEM {#single-source-of-truth}

Uma prática recomendada para implantações do AEM é manter uma fonte única e clara da verdade. O Cloud Manager foi projetado para reforçar esse princípio. No entanto, como o pipeline de front-end permite que partes do código sejam dissociadas, a configuração correta é essencial. Para evitar conflitos, verifique se vários pipelines de front-end não são implantados no mesmo site no mesmo ambiente.

Por isso, e especialmente quando vários pipelines de front-end são criados, a Adobe recomenda que você mantenha uma convenção de nomenclatura sistemática. Você pode usar as seguintes recomendações:

* O nome do módulo front-end, definido pela propriedade `name` do arquivo `package.json`, deve conter o nome do site ao qual se aplica. Por exemplo, para um site localizado em `/content/wknd`, o nome do módulo de front-end seria algo como `wknd-theme`.
* Quando um módulo de front-end compartilha o mesmo repositório Git com outros módulos, o nome da pasta deve ser igual ou conter o mesmo nome do módulo de front-end. Por exemplo, se o módulo de front-end for nomeado como `wknd-theme`, o nome da pasta de delimitação seria algo como `wknd-theme-sources`.
* O nome do pipeline de front-end do Cloud Manager também deve conter o nome do módulo de front-end e adicionar o ambiente no qual ele é implantado (produção ou desenvolvimento). Por exemplo, para o módulo de front-end chamado `wknd-theme`, o pipeline pode ser nomeado como `wknd-theme-prod`.

Essa convenção evita os seguintes erros de implantação:

* Aplicando um módulo front-end ao site errado.
* Criar vários módulos de front-end que apliquem o mesmo site, o que substituiria os outros.
* Criar vários pipelines de front-end para as mesmas fontes, o que pode causar condições de corrida, não garantindo a ordem das implantações.

## Coordenar o desenvolvimento de front-end e back-end para estabilidade no AEM {#separation-of-concerns}

Uma prática recomendada importante para qualquer separação de interesses é projetar e gerenciar o contrato cuidadosamente, o que define os limites entre eles. No pipeline de front-end, esse contrato é a saída HTML e JSON renderizada pelo site. Manter a estabilidade dessa saída garante que o pipeline de front-end forneça valor máximo, permitindo que a equipe de front-end trabalhe de forma independente.

No momento, não há nenhum recurso integrado para executar o pipeline de pilha completa de forma síncrona com os pipelines de front-end. Portanto, ao separar o desenvolvimento de front-end do pipeline de pilha completa, é crucial gerenciar o contrato cuidadosamente, o que define seus limites. Normalmente, esse contrato consiste na HTML ou JSON, ou ambos, renderizados pela Experience Manager. Quaisquer alterações a este contrato devem ser cuidadosamente coordenadas entre equipes que gerenciam diferentes pipelines para garantir uma transição suave e o sequenciamento adequado de atualizações.

As etapas a seguir geralmente são recomendadas ao fazer alterações na saída do HTML ou JSON, especialmente quando ambas as áreas são afetadas.

1. A equipe de back-end primeiro configura um ambiente de desenvolvimento com a nova saída HTML ou JSON.
   1. Por meio do pipeline de pilha completa, eles implantam o código necessário para renderizar a nova saída do HTML ou JSON, ou ambos, que são desejados.
   1. Se isso for para um ambiente ao qual a equipe de front-end não tinha acesso anteriormente, as etapas a seguir deverão ser executadas.
      1. URL: a equipe de front-end deve saber o URL desse ambiente de desenvolvimento.
      1. ACL: a equipe de front-end deve receber um usuário local do AEM com algo semelhante aos direitos de &quot;Contribuidores&quot;.
      1. Git: a equipe de front-end deve ter um local Git separado para o módulo de front-end que direciona especificamente esse ambiente de desenvolvimento.

         Uma prática comum é criar uma ramificação `dev` para gerenciar alterações feitas no ambiente de desenvolvimento. Essa prática permite uma mesclagem mais fácil de volta na ramificação `main`, que é usada para implantação no ambiente de produção.

      1. Pipeline: a equipe de front-end deve ter um pipeline de front-end que seja implantado no ambiente de desenvolvimento. Esse pipeline implantaria o módulo de front-end que normalmente está localizado na ramificação `dev`, conforme descrito no ponto anterior.
1. A equipe de front-end faz com que o código CSS e JS funcione com a saída antiga e a nova.
   1. Como de costume, para desenvolver localmente, faça o seguinte:
      1. O comando `npx aem-site-theme-builder proxy` inicia um servidor proxy que recupera conteúdo de um ambiente AEM. Ele substitui os arquivos CSS e JS do módulo front-end por esses arquivos da pasta local `dist`.
      1. A configuração da variável `AEM_URL` no arquivo oculto `.env` permite que você controle de qual ambiente do AEM o servidor proxy local consome o conteúdo.
      1. Alterar o valor de `AEM_URL`, portanto, permite que você alterne entre os ambientes de produção e desenvolvimento para ajustar o CSS e o JS para que se encaixem em ambos os ambientes.
      1. Ele deve funcionar com o ambiente de desenvolvimento que renderiza a nova saída e com o ambiente de produção que renderiza a saída antiga.
   1. O trabalho de front-end é concluído quando o módulo de front-end atualizado funciona para ambos os ambientes e é implantado em ambos.
1. A equipe de back-end pode atualizar o ambiente de produção implantando o código que renderiza a nova saída do HTML ou JSON, ou ambos, por meio do pipeline de pilha completa.
1. A equipe de front-end pode limpar o CSS e o JS, remover elementos necessários somente para a saída antiga e implantar a atualização final na produção usando o pipeline de front-end.

## Recursos adicionais {#additional-resources}

* Saiba como temas de site do AEM podem ser usados para personalizar o estilo e o design do site.

  Consulte [Temas de Site](/help/sites-cloud/administering/site-creation/site-themes.md).

* A Adobe fornece um Criador de temas de site do AEM como um conjunto de scripts para criar novos temas de site.

  Consulte [Criador de temas de site do AEM](https://github.com/adobe/aem-site-theme-builder)



