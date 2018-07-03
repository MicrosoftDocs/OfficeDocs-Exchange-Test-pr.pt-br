---
title: 'Configurar telefones celulares para acessar email: Exchange Online Help'
TOCTitle: Configurar telefones celulares para acessar email
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52058456
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar telefones celulares para acessar email

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-12_

Você pode configurar um celular, como um Windows Phone, para usar o MicrosoftExchange ActiveSync. Você deve executar este procedimento em cada telefone celular na sua organização.

## Pré-requisitos

  - Você examinou a documentação do fabricante para o telefone celular que deseja configurar.

  - O Exchange ActiveSync está habilitado em sua organização.


> [!TIP]
> Para informações específicas a um determinado dispositivo sobre como configurar o email baseado no Microsoft Exchange em um telefone ou tablet, confira <A href="https://support.office.com/pt-br/article/configurar-os-aplicativos-do-office-e-de-email-em-um-dispositivo-m%c3%b3vel-7dabb6cb-0046-40b6-81fe-767e0b1f014f?ui=pt-br%26rs=pt-br%26ad=br">Configurar um dispositivo móvel usando o Office 365 para empresas</A>.



## Configurar um telefone celular para usar o Exchange ActiveSync

A maioria dos telefones e dispositivos celulares podem usar a Descoberta Automática para configurar o cliente de email móvel para usar o Exchange ActiveSync. Para configurar uma conta de email na maioria dos telefones celulares, você precisará de duas informações.

  - O endereço de email do usuário

  - A senha do usuário

Se o celular não puder entrar em contato com o servidor Exchange automaticamente pela Descoberta Automática, será preciso configurá-lo manualmente. A configuração manual requer o endereço de email e a senha do usuário, além do nome do servidor Exchange ActiveSync. Na maioria das organizações, o nome do servidor Exchange ActiveSync é igual ao nome do servidor do Outlook Web App sem o /owa; por exemplo, mail.contoso.com.

## Sincronização com o Windows Phone

Se você estiver configurando um celular Windows Phone para sincronizar com uma caixa de correio do Exchange usando o Exchange ActiveSync, apenas um subconjunto das configurações de política de caixa de correio para dispositivos móveis são compatíveis. Essas configurações de política são detalhadas em [Suporte a políticas de caixa de correio de dispositivo móvel para Windows telefones e dispositivos](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md).

Se você definir configurações de política de caixa de correio de dispositivos móveis que não são compatíveis com a versão do Windows Phone que está usando, será necessário também definir a configuração de política **AllowNonProvisionableDevices** como verdadeira ou criar uma política de caixa de correio de dispositivo móvel separada para telefones celulares com Windows Phone.

