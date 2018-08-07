---
title: 'Não é possível inst. funç. do Exchange 2007 após prep. o AD para Exchange 2010'
TOCTitle: Não é possível instalar as funções do Exchange 2007 depois de preparar o Active Directory para o Exchange 2010_NoE12ServerWarning
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 50485564
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não é possível instalar as funções do Exchange 2007 depois de preparar o Active Directory para o Exchange 2010\_NoE12ServerWarning

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Quando você executa o Microsoft Exchange Server 2010**Setup /PrepareAD**, a ferramenta do analisador do Microsoft Exchange Server consultará a topologia existente do Active Directory para determinar se qualquer funções de servidor do Microsoft Exchange Server 2007 existem. Se as funções de servidor de Exchange 2007 não forem detectadas, você recebe a seguinte mensagem de aviso:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Instalação vai preparar a organização do Exchange Server 2010 por meio de 'Setup /PrepareAD' e não foram detectadas funções nessa topologia do Exchange Server 2007. Após essa operação, ele será impossível instalar qualquer funções do Exchange Server 2007.</p></td>
</tr>
</tbody>
</table>


Antes de implantar Exchange Server 2010, considere os seguintes fatores que podem exigir que você implantar um servidor de Exchange 2007 com todas as funções de servidor instaladas antes da implantação Exchange 2007:

  - **Aplicativos desenvolvidos na empresa ou de terceiros**   Aplicativos desenvolvidos para Exchange 2003 não podem ser compatível com Exchange 2010 e, portanto, precisam ser atualizados ou substituída. Você pode manter esses aplicativos e a população de usuário associada no Exchange 2003; Mover para Exchange 2007; ou substitua o software com uma versão compatível do Exchange 2010.

  - **Requisitos de coexistência ou a migração**   Se você planeja migrar caixas de correio em sua organização, você pode implantar Exchange 2007 e usar o Microsoft transportador Suite, ou você pode usar uma solução de coexistência ou migração de terceiros. Para baixar o Microsoft transportador Suite, vá para a [Microsoft transportador Suite](http://go.microsoft.com/fwlink/?linkid=82688) no Microsoft Download Center.

Além disso, ao avaliar as opções para a sua organização, certifique-se de que você considerou as seguintes perguntas:

  - Você tem uma estratégia in-loco para mover os aplicativos que dependem Exchange 2010 antes de Exchange 2003 atinge o fim do suporte? Para obter mais informações, visite a página de ciclo de vida de suporte da Microsoft ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839)).

  - Sua estratégia que requer a coexistência de WebDAV e serviços da Web (Exchange 2007 )?

  - Já pensou em produtos de terceiros que oferecem suporte ao Exchange ou outras tecnologias da Microsoft que permitirá que você atenda aos requisitos de coexistência ou migração?

  - Qual é sua abordagem de ciclo de vida de hardware (continuam a usar o quantos servidores de 32 bits existentes possível versus comprar novos servidores de 64 bits)?

  - Qual é seu plano para migração (migração mais rápido possível versus migrando em uma estratégia de fases todos os servidores)? Da mesma forma, o que é o cronograma para a coexistência de versões diferentes do Exchange ?

Se você decidir que precisa para implantar um servidor de Exchange 2007 antes de implantar o Exchange 2010, a implantação de um único Exchange 2007 com todas as funções de servidor é suficiente para habilitar a implantação de servidores de futuras Exchange 2007 na organização. Para implantar o servidor Exchange 2007 em sua organização Exchange 2003, siga estas etapas:

1.  Execute Exchange 2007**Setup /PrepareSchema**.

2.  Execute Exchange 2007**Setup /PrepareAD**.

3.  Execute Exchange 2007**Setup /PrepareDomain** em todos os domínios que contêm destinatários, servidores Exchange 2003 ou catálogos globais que poderiam ser usados por um servidor de Exchange.

4.  Instale um servidor de Exchange 2007 com todas as funções de servidor de quatro (Transporte de Hub, acesso para cliente, caixa de correio e Unificação de mensagens).

