---
title: 'Usar um Exchange 2010 ou o servidor de transporte de borda 2007 no Exchange 2013: Exchange 2013 Help'
TOCTitle: Usar um Exchange 2010 ou o servidor de transporte de borda 2007 no Exchange 2013
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 50486685
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar um Exchange 2010 ou o servidor de transporte de borda 2007 no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

O servidor de Transporte de Borda está disponível no Microsoft Exchange Server 2013 Service Pack 1 (SP1). Entretanto, você pode continuar usando o atual Exchange Server 2007 ou os servidores de Transporte de Borda Exchange Server 2010 que você instalou no perímetro da sua rede. Ou, instale um novo Exchange 2007 ou um servidor de Transporte de Borda Exchange 2010 no perímetro da sua rede para uma organização do Exchange 2013 nova ou atualizada.

Aqui está o que você precisa saber:

  - Um servidor de Transporte de Borda Exchange 2007 ou Exchange 2010 espera uma conexão com um servidor de Transporte de Hub. No Exchange 2013, o serviço de Transporte existe no servidor de Caixa de Correio. Portanto, o fluxo de email da Internet ocorre entre o serviço de Transporte no servidor de Caixa de Correio e o servidor de Transporte de Borda, que ignora efetivamente o servidor de Acesso para Cliente Exchange 2013.

  - Você pode assinar um servidor de Transporte de Borda do Exchange 2007 ou do Exchange 2010 para um site do Active Directory que contém apenas servidores do Exchange 2013. Você pode importar o arquivo de Inscrição de Borda e executar EdgeSync em um servidor de caixa de correio autônomo do Exchange 2013, ou em um servidor em que tanto o servidor de Caixa de Correio quanto o de Acesso para Cliente estejam instalados no mesmo computador. Você não pode importar o arquivo de Inscrição de Borda nem executar o EdgeSync em um servidor autônomo de Acesso para Cliente do Exchange 2013.

  - Os procedimentos para implementação de um novo Exchange 2007 ou servidor de Transporte de Borda Exchange 2010 na sua organização do Exchange 2013 são basicamente os mesmos de versões anteriores do Exchange. Contudo, qualquer procedimento executado no servidor de transporte Hub é executado no servidor de Caixa de Correio no Exchange 2013. Os procedimentos são:
    
      - [Configurar o fluxo de emails da Internet através de um servidor de transporte de borda inscrito](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [Configurar o fluxo de emails entre um servidor de transporte de borda e servidores de transporte de Hub sem usar o EdgeSync](https://go.microsoft.com/fwlink/p/?linkid=276661)

