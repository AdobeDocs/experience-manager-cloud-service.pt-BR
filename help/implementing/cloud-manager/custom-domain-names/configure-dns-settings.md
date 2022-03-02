---
title: 'Definição das configurações de DNS '
description: Definição das configurações de DNS
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 016954bc712a135886a6031deba05d92e7d5099c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 6%

---

# Definição das configurações de DNS {#configure-dns}

Depois que seu nome de domínio personalizado for verificado e implantado com êxito, você estará pronto para atualizar os registros DNS para seu nome de domínio personalizado com seu provedor DNS. Isso permite que seu site forneça visitantes. Portanto, essa atividade normalmente é feita antes do lançamento.

>[!NOTE]
>Você ou o indivíduo apropriado em sua organização devem ser capazes de fazer logon ou entrar em contato com seu provedor de DNS (a empresa da qual você comprou o domínio) e fazer atualizações nas configurações de DNS.

Para fazer isso, é necessário determinar se as configurações de DNS devem ser definidas como `CNAME` ou Apex apontando seu nome de domínio personalizado para o nome de domínio do Cloud Manager. A `CNAME` ou Um registro, uma vez provisionado, roteará todo o tráfego da Internet do domínio para onde ele estiver apontando. Se esse local não for provisionado para veicular o tráfego, haverá uma interrupção. Se não tiver sido testado, pode haver erros no conteúdo. É por isso que essa etapa é sempre feita após a conclusão do teste e o cliente estar pronto para entrar em funcionamento.

As etapas a seguir devem ser completadas conforme indicado no quadro abaixo:

| Etapa |  | Responsabilidade | Saiba mais |
|--- |--- |--- |---|
| Adicionar certificado SSL | Adicionar certificado SSL | Cliente | [Adicionar um certificado SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Verificação de domínio | Adicionar registro TXT | Cliente | [Adicionar um registro TXT](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Verificar Status de Verificação de Domínio |  | Cliente |  |
|  | Status: Falha na Verificação de Domínio | Cliente | [Verificando o status do nome de domínio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Status: Verificado, Falha na Implantação | Entre em contato com o representante da Adobe | [Verificando o status do nome de domínio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Adicionar registros DNS que apontam para AEM as a Cloud Service adicionando registros CNAME ou APEX | Definir configurações de DNS | Cliente | [Definição das configurações de DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Verificar Status do Registro DNS |  | Cliente | [Verificação de status do registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: Status de DNS não detectado | Cliente | [Verificação de status do registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: O DNS resolve incorretamente | Cliente |  |


## Registro CNAME {#cname-record}

As seções a seguir ajudarão você a determinar qual tipo de registro é apropriado para sua configuração de DNS.

Um nome canônico ou `CNAME` record é um tipo de registro DNS que mapeia um nome de alias para um nome de domínio verdadeiro ou canônico. Os registros CNAME normalmente são usados para mapear um subdomínio como `www.example.com`  ao domínio que hospeda o conteúdo desse subdomínio.

Faça logon no Registrador de domínio e crie um registro CNAME para apontar o nome de domínio personalizado para o público-alvo, conforme mostrado abaixo:

| CNAME | Ponto de Nome de Domínio Personalizado para Destino |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## Registro APEX {#apex-record}

Um domínio de ápice é um domínio personalizado que não contém um subdomínio, como example.com. Um domínio anexado é configurado com um `A` , `ALIAS` ou `ANAME` registre por meio do provedor DNS. Os domínios do Apex devem apontar para endereços IP específicos.

Adicione todos os seguintes registros A às configurações de DNS do Domínio por meio do provedor de domínio:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
