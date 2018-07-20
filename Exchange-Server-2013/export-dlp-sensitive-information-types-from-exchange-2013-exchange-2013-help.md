---
title: 'Exportar os tipos de informações confidenciais de DLP do Exchange 2013: Exchange 2013 Help'
TOCTitle: Exportar os tipos de informações confidenciais de DLP do Exchange
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59635877
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar os tipos de informações confidenciais de DLP do Exchange 2013

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-05-04_

Você pode exibir ou alterar os detalhes em suas políticas de DLP sem usar o Centro de administração do Exchange (EAC) ou cmdlets Shell de Gerenciamento do Exchange exportando as políticas, salvá-los como um arquivo XML e modificar esse arquivo XML. Normalmente você seria importar arquivo XML de volta à Exchange. Dessa forma, as políticas podem ser editadas independente da Exchange. No entanto, eles devem atender os requisitos de formato específico, também conhecidos como o esquema XML, para que funcionem corretamente.

Para tarefas de gerenciamento adicionais relacionadas a DLP, consulte [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Prevenção de perda de dados (DLP)\&quot; no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

O EAC não fornece uma maneira para exportar as políticas DLP ou modelos para um arquivo externo. Use o Shell de Gerenciamento do Exchange para executar essa tarefa.

## Use o Shell de Gerenciamento do Exchange para exportar os tipos de informações confidenciais de DLP

Este exemplo exporta todos os tipos de informações confidenciais de DLP, juntamente com seus atributos para um arquivo XML no caminho C:\\My Documents\\exportedInformationTypes.xml. É recomendável fazer uma cópia de backup do seu conjunto de tipos de informações confidenciais de DLP atual. Uma maneira de fazer isso é para exportar e copiar imediatamente e renomear o mesmo arquivo XML.

1.  Abra o Shell de Gerenciamento do Exchange.

2.  Tipo de **Get-ClassificationRuleCollection**e tipos de informações confidenciais da sua organização devem exibir na tela. Se você não criou todos os tipos de informações confidenciais de sua preferência, você verá apenas o padrão, o conjunto de tipos de informações confidenciais internas, rotulada como "Pacote Microsoft Rule."

3.  Armazene os tipos de informações confidenciais em uma variável, digitando **$ruleCollections = Get-ClassificationRuleCollection**.

4.  Agora faça um arquivo XML formatado com todos esses dados digitando **Set-Content - caminho "C:\\My Documents\\exportedRules.xml"-Encoding Byte-valor $ruleCollections.SerializedClassificationRuleCollection**..

Agora você pode editar o arquivo XML para ajustar as políticas conforme necessário. Para saber como personalizar os tipos de informações confidenciais internas, consulte [Personalizar os tipos de informações confidenciais de DLP internos](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md). Para obter detalhes sobre como importar políticas de volta no Exchange, consulte [Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

## Para obter mais informações

[O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Personalizar os tipos de informações confidenciais de DLP internos](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

