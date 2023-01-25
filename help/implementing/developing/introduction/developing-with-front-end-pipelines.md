---
title: Desenvolvimento de Sites com o pipeline front-end
description: Com o pipeline front-end, mais independência é dada aos desenvolvedores front-end e o processo de desenvolvimento pode ganhar uma velocidade substancial. Este documento descreve algumas considerações específicas do processo de build front-end que devem ser fornecidas.
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
source-git-commit: 2afdd0682d1baf39d737ee7a5721657e639739a7
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---


# Desenvolvimento de Sites com o pipeline front-end {#developing-site-with-front-end-pipeline}

[Com o pipeline front-end,](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) é dada mais independência aos desenvolvedores front-end e o processo de desenvolvimento pode ganhar uma velocidade substancial. Este documento descreve como esse processo funciona, além de algumas considerações que devem ser levadas em consideração para aproveitar todo o potencial desse processo.

>[!TIP]
>
>Se ainda não estiver familiarizado com o uso do pipeline front-end e os benefícios que ele pode trazer, verifique o [Jornada Rápida de Criação de Site](/help/journey-sites/quick-site/overview.md) para obter um exemplo de como implantar rapidamente um novo site e personalizar seu tema completamente independente do desenvolvimento de back-end.

## Contrato de construção de front-end {#front-end-build-contract}

Semelhante ao [ambiente de criação de pilha completa,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) o pipeline front-end tem seu próprio ambiente. Os desenvolvedores têm alguma flexibilidade neste pipeline, desde que o seguinte contrato de construção de front-end seja observado.

O pipeline de front-end requer o projeto Node.js de front-end para usar o `build` diretiva de script para gerar a build que será implantada pelo pipeline front-end. Ou seja, o Cloud Manager usa o comando `npm run build` para gerar o projeto implantável no `dist` pasta.

O conteúdo da `dist` é o que é implantado em AEM as a Cloud Service no pipeline do Cloud Manager.

### Versões de nó {#node-versions}

Por padrão, o pipeline de front-end usa o Nó 14, mas 12 e 16 também estão disponíveis.

Você pode usar o `CM_CUSTOM_VAR_NODE_VERSION` variável de ambiente para definir a versão desejada.

## Fonte única da verdade {#single-source-of-truth}

Uma boa prática geral é manter uma única fonte de verdade para o que está implantado em AEM. O objetivo do Cloud Manager é tornar essa única fonte de verdade óbvia. No entanto, como o pipeline front-end permite dissociar o local de partes do código, alguma responsabilidade adicional está na configuração correta dos pipelines front-end. Alguns cuidados devem ser tomados para não criar vários pipelines de front-end que sejam implantados no mesmo site no mesmo ambiente.

Por isso, e especialmente quando vários pipelines de front-end são criados, é recomendável manter uma convenção de nomenclatura sistemática, como a seguinte:

* O nome do módulo front-end, definido pelo `name` da `package.json` , deve conter o nome do site ao qual se aplica. Por exemplo, para um site localizado em `/content/wknd`, o nome do módulo front-end seria algo como `wknd-theme`.
* Quando um módulo front-end compartilha o mesmo repositório Git com outros módulos, o nome de sua pasta deve ser igual ou conter o mesmo nome do módulo front-end. Por exemplo, se o módulo front-end for nomeado `wknd-theme`, o nome da pasta de inclusão seria algo como `wknd-theme-sources`.
* O nome do pipeline front-end do Cloud Manager também deve conter o nome do módulo front-end e também adicionar o ambiente ao qual ele implanta (produção ou desenvolvimento). Por exemplo, para o módulo front-end chamado `wknd-theme`, o pipeline pode ser nomeado como algo como `wknd-theme-prod`.

Essa convenção deve evitar eficientemente os seguintes erros de implantação:

* Aplicação de um módulo front-end ao site errado
* Criação de vários módulos front-end que aplicam o mesmo site, o que se sobrescreveria
* Criar vários pipelines de front-end para as mesmas fontes, o que poderia causar condições de corrida, não garantindo a ordem das implantações

## Separação de problemas {#separation-of-concerns}

Outra boa prática que se aplica a qualquer separação de preocupações é ter especial cuidado com a forma como o contrato que separa as preocupações é concebido e gerido. No caso do gasoduto front-end, o contrato que separa esse código do resto é o HTML e JSON renderizado pelo site. Se esse HTML e JSON permanecerem estáveis, o pipeline front-end fornecerá seu valor máximo, tornando a equipe front-end totalmente independente.

No momento, não há nenhum recurso específico para executar o pipeline de pilha completa de forma síncrona com os pipeline front-end. Por esta razão, ao dissociar o desenvolvimento de front-end do gasoduto de pilha completa, deve ser incluído um cuidado adicional no contrato que separa estas duas áreas de preocupação. Esse contrato geralmente é o HTML e/ou JSON que o Experience Manager renderiza. As alterações a esse contrato devem, por conseguinte, ser bem planejadas entre as equipes que operam os diferentes gasodutos, de modo a que estas acordem em como proceder às alterações correspondentes.

As etapas a seguir são geralmente recomendadas quando é necessário executar alterações na saída do HTML e/ou JSON que afetam ambas as áreas de preocupação.

1. A equipe de back-end configura primeiro um ambiente de desenvolvimento com o novo HTML e/ou saída JSON.
   1. Por meio do pipeline de pilha completa, eles implantam o código necessário para renderizar o novo HTML e/ou a saída JSON que é desejada.
   1. Se isso for para um ambiente ao qual a equipe de front-end não tinha acesso anteriormente, as etapas a seguir devem ser executadas.
      1. URL: A equipe de front-end deve saber o URL desse ambiente de desenvolvimento.
      1. ACL: A equipe de front-end deve receber um usuário local AEM com algo semelhante aos direitos de &quot;Contribuidores&quot;.
      1. Git: A equipe de front-end deve ter um local Git separado para o módulo de front-end que direciona especificamente esse ambiente de desenvolvimento.
         * Uma prática comum é criar um `dev` ramificação , para que as alterações feitas no ambiente de desenvolvimento possam ser facilmente mescladas de volta ao `main` ramificação que deve ser implantada no ambiente de produção.
      1. Pipeline: A equipe de front-end deve ter um pipeline de front-end que é implantado no ambiente de desenvolvimento. Esse pipeline implantaria o módulo front-end normalmente localizado no `dev` ramificação, tal como descrito no ponto anterior.
1. A equipe de front-end faz com que o código CSS e JS funcionem com a saída antiga e a nova.
   1. Como de costume, desenvolver localmente:
      1. O `npx aem-site-theme-builder proxy` comando executado no módulo front-end inicia um servidor proxy que solicita o conteúdo de um ambiente AEM, ao substituir os arquivos CSS e JS do módulo front-end pelos arquivos locais `dist` pasta.
      1. Configurar a `AEM_URL` na variável oculta `.env` permite controlar a partir de qual ambiente AEM o servidor proxy local consome o conteúdo.
      1. Alterar o valor disso `AEM_URL` assim, o permite alternar entre os ambientes de produção e desenvolvimento para ajustar o CSS e o JS, de modo que se ajuste a ambos os ambientes.
      1. Ele deve funcionar com o ambiente de desenvolvimento que renderiza a nova saída e com o ambiente de produção que renderiza a saída antiga.
   1. O trabalho de front-end é concluído quando o módulo de front-end atualizado funciona para ambos os ambientes e é implantado em ambos.
1. A equipe de back-end pode atualizar o ambiente de produção, implantando o código que renderiza o novo HTML e/ou a saída JSON por meio do pipeline de pilha completa.
1. A equipe de front-end pode, então, limpar o CSS e o JS e remover o que era necessário apenas para a saída antiga, implantando essa última atualização na produção por meio do pipeline de front-end.

## Recursos adicionais {#additional-resources}

* [Temas do Site](/help/sites-cloud/administering/site-creation/site-themes.md) - Saiba como AEM temas do site podem ser usados para personalizar o estilo e o design do site.
* [AEM Criador de Tema do Site](https://github.com/adobe/aem-site-theme-builder) - O Adobe fornece um AEM Criador de Temas do Site como um conjunto de scripts para criar novos temas do site.
