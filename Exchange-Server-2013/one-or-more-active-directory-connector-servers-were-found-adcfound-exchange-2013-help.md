---
title: 'Um ou mais servidores de conector do Active Directory foram found_ADCFound: Exchange 2013 Help'
TOCTitle: Um ou mais servidores de conector do Active Directory foram found_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 50486355
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Um ou mais servidores de conector do Active Directory foram found\_ADCFound

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-15_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 e Exchange Server 2010 não pode continuar porque um ou mais conectores ADC (Active Directory) foram encontrados no ambiente atual do Microsoft Exchange.

ADC replica objetos de Exchange Server versão 5.5 para o serviço de diretório do Active Directory em um ambiente do Microsoft Exchange de modo misto e não é suportada pelo Exchange 2007 ou Exchange 2010.

A instalação do Exchange 2007 ou Exchange 2010 exige que todos os componentes de ADC ser removido.

Para resolver esse problema, remova todos os componentes de ADC e execute novamente o programa de instalação do Exchange 2007 ou Exchange 2010.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para remover os componentes do conector do Active Directory</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Para desabilitar o serviço ADC no servidor que está executando o serviço ADC, clique com o botão <strong>Meu computador</strong> na área de trabalho e, em seguida, clique em <strong>Gerenciar</strong>.</p></li>
<li><p>Expanda o nó <strong>serviços e aplicativos</strong> e, em seguida, clique no nó de <strong>Serviços</strong>.</p></li>
<li><p>No painel direito, clique com o botão <strong>Microsoft Active Directory Connector</strong> e clique em <strong>Propriedades</strong>.</p></li>
<li><p>Altere o <strong>tipo de inicialização</strong> para <strong>desabilitado</strong>. Na próxima vez que o computador inicia, o serviço ADC não será iniciado.</p></li>
<li><p>Clique em <strong>Aplicar</strong> e em <strong>OK</strong>.</p></li>
<li><p>Para desinstalar o serviço ADC, use o Assistente de instalação do Active Directory no Microsoft Exchange 2000 Server ou CD do Microsoft Exchange Server 2003. Abra a pasta \ADC\I386 e clique duas vezes em Setup.exe programa. Siga os prompts para <strong>Remover todos os</strong> componentes do serviço de ADC.</p>

> [!IMPORTANT]
> Você deve concluir a etapa 6 e <STRONG>Remover tudo</STRONG> ADC componentes para resolver esse problema. É insuficiente para desabilitar o serviço ADC.


</li>
</ol></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre ADC, consulte os seguintes artigos da Base de Conhecimento Microsoft:

  - 325300, "WebCast de suporte: Introdução ao conector do Active Directory" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325300)).

  - 325221, "WebCast de suporte: Microsoft Advanced conector do Active Directory" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325221)).

  - 312632, "Como instalar e configurar o conector do Active Directory no Exchange 2000 Server" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=312632)).

