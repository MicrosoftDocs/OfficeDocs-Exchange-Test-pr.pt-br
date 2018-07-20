---
title: 'Configurações de dispositivo do Exchange ActiveSync com implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: Configurações de dispositivo do Exchange ActiveSync com implantações híbridas do Exchange
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64374752
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurações de dispositivo do Exchange ActiveSync com implantações híbridas do Exchange

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-01-27_

Os dispositivos do Exchange ActiveSync são reconfigurados automaticamente quando uma caixa de correio é movida de uma organização do Exchange local para o Office 365. O Exchange ActiveSync encontrará o local da nova caixa de correio no Office 365 e atualizará sua configuração para falar diretamente com o Office 365. O dispositivo do Exchange ActiveSync não tentará entrar em contato com o servidor do Exchange local depois que ele for redirecionado com êxito para o Office 365. Com apenas algumas exceções (há mais informações a seguir), o usuário não precisa mais configurar manualmente seu dispositivos para email para continuar trabalhando.

Se você desejar mover uma caixa de correio para o Office 365, consulte [Movimentação de caixas de correio entre organizações locais e do Exchange Online em implantações híbridas](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

Para saber mais sobre implantações híbridas, confira [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Para usar o redirecionamento automático, seus servidores locais precisam estar executando as versões mais recentes do Exchange 2010, Exchange 2013, Exchange 2016 ou posterior. Também é preciso ter usado o [Assistente de Configuração Híbrida](hybrid-configuration-wizard-exchange-2013-help.md) para configurar sua implantação híbrida. A funcionalidade de redirecionamento do Exchange ActiveSync usa a URL de destino do Outlook na Web definida no objeto de relação da organização. Esse objeto é configurado quando o Assistente de Configuração Híbrida é executado.

Se sua organização atende aos requisitos listados acima, os dispositivos móveis devem ser redirecionados automaticamente para o Office 365 quando a caixa de correio de um usuário é movida, sem nenhuma configuração adicional. Para obter a melhor experiência, verifique se os dispositivos móveis dos usuários estão executando as últimas versões de seus sistemas operacionais e clientes de email. Alguns dispositivos móveis, como os que executam o sistema operacional Android, podem demorar mais do que o esperado para serem redirecionados. Além disso, alguns dispositivos podem não interpretar corretamente as instruções de redirecionamento do Exchange ActiveSync 451 enviadas pelo Exchange. Para esses dispositivos, os usuários ainda precisarão reconfigurar manualmente ou recriar sua conta de email no dispositivo. Se você não tiver certeza se um dispositivo dá suporte ao redirecionamento do Exchange ActiveSync 451, contate o fabricante do dispositivo.

Não há suporte ao redirecionamento automático do Exchange ActiveSync nos seguintes cenários:

  - Mover caixas de correio do Office 365 para uma organização local do Exchange.

  - Mover caixas de correio entre organizações locais do Exchange.

  - Mover caixas de correio de servidores Exchange 2007 para o Office 365.

