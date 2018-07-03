---
title: Importar o Pacote de Gerenciamento do Exchange Server 2013
TOCTitle: Importar o Pacote de Gerenciamento do Exchange Server 2013
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53275647
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Importar o Pacote de Gerenciamento do Exchange Server 2013

 

_**Tópico modificado em:**  2013-03-30_

Comecemos com a importação do pacote de gerenciamento para a implantação do SCOM.

## Pré-requisitos

Antes de importar o pacote de gerenciamento, verifique se as seguintes condições são atendidas:

  - Você tem uma das seguintes versões do System Center Operations Manager implantada em sua organização:
    
      - System Center Operations Manager 2012 RTM ou posterior
    
      - System Center Operations Manager 2007 R2 ou posterior

  - Você já implantou agentes do SCOM nos servidores Exchange. [Verifique o status de implantação do agente](procedures-related-to-deployment.md).

  - Os agentes do SCOM em seus servidores Exchange estão sendo executados na conta do sistema local. [Verifique a configuração de segurança do agente](procedures-related-to-deployment.md).

  - Os agentes do SCOM em seus servidores Exchange estão configurados para atuar como um proxy e descobrir objetos gerenciados em outros computadores. [Verifique a configuração do proxy do agente](procedures-related-to-deployment.md).

  - Sua conta de usuário é um membro da função dos Administradores do Operations Manager

## Importar o Pacote de Gerenciamento do Exchange Server 2013

Use as seguintes etapas para importar o Pacote de Gerenciamento do Exchange Server 2013. Este procedimento pressupõe que você extraiu o conteúdo do pacote de gerenciamento para uma unidade local do seu servidor do System Center Operations Manager (SCOM). Baixe o Pacote de Gerenciamento do Exchange Server 2013 no.

1.  Faça logon em seu servidor do SCOM e baixe o Pacote de Gerenciamento do Exchange Server 2013 no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/p/?linkid=268587).

2.  Extraia o conteúdo do pacote de gerenciamento para uma pasta no seu sistema executando o arquivo `ExchangeServerManagementPack.msi`.

3.  Inicie o Console SCOM. No console SCOM, clique em **Administração**

4.  Clique com o botão direito em **Pacotes de Gerenciamento** e depois em **Importar Pacotes de Gerenciamento**.

5.  O assistente Importar Pacotes de Gerenciamento é aberto. Clique em **Adicionar** e, em seguida, clique em **Adicionar do disco**.

6.  A caixa de diálogo **Selecione os Pacotes de Gerenciamento para importação** será aberta. Navegue até o diretório onde você extraiu o pacote de gerenciamento. Clique no arquivo `Microsoft.Exchange.15.mp` e depois em **Abrir**.

7.  O pacote de gerenciamento do Exchange Server 2013 está listado na página **Selecionar Pacotes de Gerenciamento**. Clique em **Instalar**.

8.  A página **Importar Pacotes de Gerenciamento** é aberta e mostra o progresso. Se houver um problema em qualquer fase do processo de importação, selecione o pacote de gerenciamento na lista para exibir os detalhes do status.

9.  Quando a importação for concluída, clique em **Fechar**.

10. Clique em **Exibir** e depois em **Atualizar** ou pressione F5, para ver o pacote de gerenciamento do Microsoft Exchange Server 2013 na lista de Pacotes de Gerenciamento.

Agora que você já importou o pacote de gerenciamento, consulte [Introdução ao Pacote de Gerenciamento do Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md) para saber mais sobre o novo pacote.

