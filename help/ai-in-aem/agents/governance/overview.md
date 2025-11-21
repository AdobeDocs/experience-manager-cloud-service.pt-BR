---
title: Visão geral do agente de governança
description: Saiba como o AEM Governance Agent protege a integridade e a conformidade da marca no AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 9b26cd1f30ad6fa23e28c9f36fe48091e069962e
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Visão geral do agente de governança {#governance-agent}

O **Agente de Governança** é uma solução projetada para proteger a integridade e a conformidade da marca em toda a Adobe Experience Manager. Ela aplica políticas de segurança, normativas e de marca para garantir que cada interação e ativação siga os padrões estabelecidos. O Agente de governança é totalmente integrado ao assistente de IA e foi projetado para operar de forma contínua em ambientes corporativos, aproveitando as ferramentas **A2A (Agente para Agente)** e **MCP (Protocolo de Controle de Modelo)**. Essas integrações permitem que o agente se conecte a orquestradores avançados de IA, como ChatGPT, Claude e outros sistemas de IA externa, garantindo inteligência flexível e escalável em todas as plataformas.

Os principais recursos incluem:

* **Governança da marca**: mantenha a consistência da marca e reduza a revisão manual automatizando as verificações da marca em todo o conteúdo e ativos
* **Permissões e Digital Rights Management (DRM):** garante a colaboração segura e compatível controlando permissões e direitos de uso em ativos digitais.

Ao combinar esses recursos, o Agente de governança reduz riscos e permite uma entrega rápida, segura e sob marca em escala.

>[!IMPORTANT]
>
>As respostas geradas por IA podem ser imprecisas ou enganosas. Verifique as correções e respostas sugeridas.
>
>Consulte também [Diretrizes de usuário da IA gerativa da Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Habilidades no AEM Governance Agent {#skills-in-aem-governance-agent}

### Governança da marca {#brand-governance}

O agente de governança pode validar o conteúdo em relação às diretrizes da marca para garantir a consistência em todas as experiências digitais. Ele usa regras de marca pré-assimiladas, como tom, declarações, uso de logotipo, tipografia e imagens. Ele opera em tempo real no chat, editores e modo de lote no Experience Hub, tornando-o ideal para conteúdo gerado por IA, migrações de sites e criação de sites com base em resumo.

![Visão geral sobre a governança da marca](/help/ai-in-aem/agents/governance/assets/brand-governance.png)

**Exemplos de Prompt:**

* *Esta página está alinhada à minha marca?`https://www.website/en.html`*
* *Este `https://www.website/en.html` segue as diretrizes de mensagens da marca?*
* *Verifique se `https://www.website/homepage` segue as diretrizes da marca*
* *Mostre-me as diretrizes da minha marca*

### Permissão e Digital Rights Management {#permission-and-digital-rights-management}

#### Gerenciamento de permissões no Content Hub {#permission-management-in-content-hub}

No Content Hub, o agente de governança garante que somente as pessoas certas acessem os ativos certos na hora certa. Ao aplicar controles granulares e baseados em atributos e direitos de uso, ele protege o conteúdo confidencial e, ao mesmo tempo, permite a colaboração segura. Isso significa menor risco de conformidade, maior integridade da marca e fluxos de trabalho mais rápidos. As equipes podem compartilhar e reutilizar ativos com confiança sem se preocupar com acesso não autorizado ou uso indevido. Esse equilíbrio de segurança e flexibilidade resulta em maior eficiência operacional e confiança em toda a organização.

![Visão Geral do Gerenciamento de Permissões](/help/ai-in-aem/agents/governance/assets/permission-management.png)

**Exemplos de Prompt:**

* *Mostrar todas as regras existentes do Content Hub ABAC.*
* *Crie uma regra que dê ao grupo &quot;Marketing&quot; acesso a todos os ativos.*
* *Conceda ao grupo de Vendas acesso aos ativos em que marketing:segment é igual a EMEA.*
* *Excluir todas as regras que dão acesso à agência externa*
* *O que é o ABAC no Content Hub e o que você pode me ajudar a fazer?*

#### Assets Digital Rights Management {#assets-digital-rights-management}

Com o agente, você pode gerenciar os direitos digitais da Assets no ecossistema de conteúdo. Ele controla permissões e direitos de uso em nível detalhado, garantindo que os ativos sejam acessados e usados somente dentro dos limites de conformidade definidos. Isso proporciona tranquilidade, protegendo a propriedade intelectual, reduzindo o risco regulamentar e mantendo a integridade da marca. Ao automatizar a aplicação de direitos, as equipes podem colaborar com segurança e confiança, acelerando a distribuição de conteúdo sem comprometer a segurança ou a conformidade.

![Visão Geral do Gerenciamento DRM](/help/ai-in-aem/agents/governance/assets/drm-management.png)

**Exemplos de Prompt:**

* *Algum dos meus ativos vai expirar em breve?*
* *Encontre todos os ativos de bicicleta que expiraram no mês passado.*
* *Quais ativos expiraram recentemente?*
* *Localizar ativos sem data de vencimento*
* *Mostrar todos os ativos em /content/dam/products que estão prestes a expirar nos próximos 14 dias*

