---
title: 'Não é possível encontrar o registro Host para o computador local no banco de dados de DNS: Exchange 2013 Help'
TOCTitle: Não é possível encontrar o registro Host para o computador local no banco de dados de DNS
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 50485271
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não é possível encontrar o registro Host para o computador local no banco de dados de DNS

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-09_

A Instalação do Microsoft Exchange Server 2013 não pode continuar porque não foi possível encontrar o registro Host (A) para este computador no banco de dados DNS.

A Instalação do Exchange 2013 exige que o computador local tenha um registro HOST (A) válido registrado em um banco de dados DNS autoritativo para o domínio.

O Exchange depende de registros Host (A) DNS para o Endereço IP de seu próximo servidor de destino interno ou externo.

Para resolver esse problema:

  - Verifique se a configuração de TCP/IP local aponta para o servidor DNS correto. Para obter mais informações, consulte [Configurações TCP/IP configurar](https://go.microsoft.com/fwlink/p/?linkid=108281).

  - Use Nslookup.exe para verificar a existência do registro de Host (A) no servidor DNS. Para obter mais informações, consulte [para verificar se um recurso registros existem no DNS](https://go.microsoft.com/fwlink/?linkid=63001).

Para obter informações sobre resolução de nome DNS, solução de problemas e registros do Host (A), consulte:

  - [Solucionando problemas de DNS](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [Gerenciamento de registros de recurso](https://go.microsoft.com/fwlink/p/?linkid=294829)

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

