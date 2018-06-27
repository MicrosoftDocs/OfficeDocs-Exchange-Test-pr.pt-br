---
title: 'Compartilhamento: Exchange 2013 Help'
TOCTitle: Compartilhamento
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 50484979
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Compartilhamento

 

_**Aplica-se a:**Exchange Server 2013, Outlook 2013_

_**Tópico modificado em:**2015-02-27_

Talvez seja necessário coordenar agendas com pessoas de diferentes organizações ou com amigos e membros da família, para poder trabalhar em conjunto em projetos ou planejar eventos sociais. Com o Exchange 2013, os administradores podem configurar diferentes níveis de acesso de calendário para permitir a colaboração com outras empresas e para permitir que os usuários compartilhem suas agendas com outras pessoas. O compartilhamento de calendário de empresa para empresa é configurado pela criação de *relacionamentos de organização*. O compartilhamento de calendário de usuário para usuário é configurado pela aplicação de *políticas de compartilhamento*.


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



**Sumário**

Sharing Scenarios in Exchange 2013

Limitations of free/busy sharing

Firewall considerations for federated sharing

Coexistence with Exchange 2010

Coexistence with Exchange 2007

Sharing Documentation

## Cenários de compartilhamento no Exchange 2013

Os cenários de compartilhamento a seguir têm suporte no Exchange 2013:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Meta de compartilhamento</th>
<th>Configuração a ser usada</th>
<th>Requisitos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Compartilhar calendários com uma organização do Office 365</p></td>
<td><p>Relacionamentos da organização</p></td>
<td><p>A organização do Office 365 está pronta para ser configurada. O administrador do Exchange local configurou um relacionamento de autenticação com a nuvem (também conhecido como &quot;federação&quot;) e deve atender aos requisitos mínimos de software. Para saber mais sobre como configurar a federação, consulte <a href="federation-exchange-2013-help.md">Federação</a>.</p></td>
</tr>
<tr class="even">
<td><p>Compartilhar calendários com outra organização do Exchange local</p></td>
<td><p>Relacionamentos da organização</p></td>
<td><p>Ambas as organizações locais do Exchange precisam configurar a federação e devem atender aos requisitos mínimos de software</p></td>
</tr>
<tr class="odd">
<td><p>Compartilhar o calendário de um usuário do Exchange com um usuário da Internet</p></td>
<td><p>Diretivas de compartilhamento</p></td>
<td><p>Nenhum, pronto para configurar</p></td>
</tr>
<tr class="even">
<td><p>Compartilhar o calendário de um usuário do Exchange com outro usuário do Exchange local</p></td>
<td><p>Políticas de compartilhamento</p></td>
<td><p>Ambas as organizações locais do Exchange precisam configurar a federação e devem atender aos requisitos mínimos de software.</p></td>
</tr>
</tbody>
</table>


A tabela a seguir lista as diferenças entre os relacionamentos da organização e as políticas de compartilhamento.

### Relacionamentos de organização versus políticas de compartilhamento

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funcionalidade</th>
<th>Relação de organização</th>
<th>Diretiva de compartilhamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Requer uma relação de confiança de federação para sua organização</p></td>
<td><p>Sim</p></td>
<td><p>Sim, ao compartilhar com outras organizações de domínio federado. Não necessário para políticas de compartilhamento de Internet.</p></td>
</tr>
<tr class="even">
<td><p>Recomenda que o domínio externo seja federado</p></td>
<td><p>Sim</p></td>
<td><p>Sim, ao compartilhar com outras organizações de domínio federado. Não necessário para políticas de compartilhamento de Internet.</p></td>
</tr>
<tr class="odd">
<td><p>Permite o compartilhamento de informações de disponibilidade (incluindo assunto e local) com organizações externas de um conjunto de muitos usuários.</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Permite o compartilhamento de pastas de calendário com informações de disponibilidade</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Permite o compartilhamento de pastas de calendário com informações de disponibilidade, incluindo assunto e corpo</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Requer que os usuários enviem um convite de compartilhamento a destinatários externos</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Fornece o método de acesso</p></td>
<td><p>O servidor de Acesso para Cliente acessa o servidor de Acesso para Cliente da organização externa e recupera as informações de disponibilidade para o usuário externo, quando solicitado.</p></td>
<td><p>O servidor de Acesso para Cliente acessa o servidor de Acesso para Cliente da organização externa e inscreve-se na pasta Calendário do usuário externo. Para políticas de compartilhamento de Internet, os usuários externos acessam uma URL restrita ou pública no servidor de Acesso para Cliente.</p></td>
</tr>
<tr class="even">
<td><p>Aplica-se a todos os domínios externos</p></td>
<td><p>Não (uma relação um-para-um entre duas organizações do Exchange 2013)</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Fornece aos usuários experiências de compartilhamento diferentes com destinatários externos</p></td>
<td><p>Não</p></td>
<td><p>Sim, com base na diretiva de compartilhamento que é aplicada</p></td>
</tr>
<tr class="even">
<td><p>Desativa o compartilhamento para alguns usuários</p></td>
<td><p>Sim, especificando um grupo de distribuição de segurança para a relação de organização</p></td>
<td><p>Sim, desativando a diretiva de compartilhamento que é aplicada</p></td>
</tr>
<tr class="odd">
<td><p>Requer que a caixa de correio resida em um servidor de Caixa de Correio do Exchange 2013</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Limitações de compartilhamento de disponibilidade

As limitações a seguir aplicam-se ao compartilhamento de informações de disponibilidade entre organizações do Exchange:

1.  **Outlook Web Access 2003**   Quando um usuário em uma organização remota do Exchange 2003 usa o Outlook Web Access para acessar a disponibilidade de acesso para usuários em uma organização remota do Exchange 2013, a solicitação irá falhar. As conexões do Outlook Web Access do Exchange 2003 não podem fazer conexões WebDAV (Web-based Distributed Authoring and Versioning) para uma pasta de sistema de disponibilidade, para recuperar as informações para usuários remotos. Como o Exchange 2013 não suporta conexões WebDAV, o servidor Exchange 2003 não consegue se conectar a External (FYDIBOHF25SPDLT) no servidor CAS do Exchange 2013 para solicitações do Outlook Web Access. Os clientes do Outlook não passam por essa limitação porque eles usam MAPI, em vez de WebDAV, quando se conectam a External (FYDIBOHF25SPDLT).

2.  **Latência de rede de longa distância (WAN)**   Nas organizações do Exchange 2003, as réplicas de todas as pastas de disponibilidade devem ficar nos servidores de Caixa de Correio do Exchange 2010 SP2 ou superior. Em ambientes em que os bancos de dados de pasta pública do Exchange 2003 ficam em vários sites físicos, pode haver latência excessiva e problemas de desempenho, se as solicitações de disponibilidade internas tiverem que atravessar links WAN para acessar bancos de dados de pasta pública do Exchange 2010 não localizados no mesmo site físico.

3.  **Período das informações de disponibilidade**   As solicitações de informações de disponibilidade para uma organização do Exchange 2007 de uma organização do Exchange 2013 podem falhar devido a um problema de correspondência no período das informações de disponibilidade solicitadas. Por padrão, o Exchange 2007 aceita as solicitações de disponibilidade por 42 dias de informações de disponibilidade e o Exchange 2013 pode solicitar 62 dias de informações de disponibilidade. Se a solicitação exceder o limite padrão de 42 imposto pelo Exchange 2007, a solicitação irá falhar.
    
    Siga as instruções abaixo para configurar seus servidores CAS do Exchange 2007, de modo que aceitem solicitações de informações de disponibilidade de períodos maiores:
    
    1.  Em todos os seus servidores CAS do Exchange 2007, abra o seguinte arquivo com um editor de textos, como o Bloco de Notas: \<Exchange Installation Path\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config
        

        > [!WARNING]
        > Antes de fazer qualquer alteração no arquivo web.config, faça uma cópia do arquivo e armazene-a em um local seguro.

    
    2.  Localize a seção **appSettings** no arquivo web.config.
    
    3.  Adicionar uma nova chave"\<adicionar chave ="maximumQueryIntervalDays" valor = "62" /\>" e salve o arquivo web.config.
        

        > [!TIP]
        > O valor maximumQueryIntervalDays não está presente por padrão. Quando esse valor não estiver presente, o Exchange 2007 usará o intervalo padrão de 42 dias.

    
    4.  Interrompa e reinicie os Serviços de Informação da Internet (IIS) da Microsoft em todos os servidores CAS do Exchange 2007.

4.  **Organizações do Exchange com usuários locais e na nuvem**   Se você configurar o compartilhamento de calendário com outra organização do Exchange que esteja configurada em uma implantação híbrida com o Microsoft Office 365, ocorrerá falha nas pesquisas de disponibilidade de usuários baseados no Office 365 ou remotos que tenham sido movidos para a nuvem. Como o relacionamento de organização para a sua organização do Exchange é com a organização remota do Exchange no local, não com a organização do Exchange Online baseada no Office 365, a solicitação de disponibilidade não pode consultar os usuários baseados no Office 365. O Exchange 2013 não suporta a funcionalidade para transmitir por proxy essas solicitações de disponibilidade através da organização local para o serviço do Office 365.

Para detalhes sobre como configurar o compartilhamento de disponibilidade entre as implantações comuns do Exchange, consulte [Configurando o compartilhamento federado entre organizações do Exchange](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md).

## Considerações de firewall para compartilhamento federado

Recursos de compartilhamento federados exigem que os servidores de acesso para cliente em sua organização tenham acesso à Internet de saída usando HTTPS. Você deve permitir o acesso externo de HTTPS (porta 443 para TCP) para todos os servidores de caixa de correio Exchange 2013 na organização.

Para uma organização externa acessar as informações de disponibilidade da sua organização, você deve publicar em pelo menos um servidor de Acesso para Cliente na Internet. Isso requer acesso HTTPS de entrada da Internet para o servidor de Acesso para Cliente. Os servidores de Acesso para Cliente nos sites do Active Directory que não tenham um servidor de Acesso para Cliente publicado na Internet podem usar os servidores de Acesso para Cliente em outros sites do Active Directory que possam ser acessados da Internet. Os servidores de Acesso para Cliente que não são publicados na Internet devem ter a URL externa do diretório virtual de serviços da Web definida com a URL que é visível para organizações externas.

Voltar ao início

## Coexistência com o Exchange 2010

Em organizações que tenham tanto servidores Exchange 2010 quanto Exchange 2013, os usuários que tiverem uma caixa de correio em um servidor de Caixa de Correio do Exchange 2010 podem usar relacionamentos de organização para compartilhar informações de disponibilidade com destinatários em organizações de domínio federado externas do Exchange 2013. Os servidores de Caixa de Correio e de Acesso para Cliente do Exchange 2010 devem ter o SP2 ou superior, e você deve ter pelo menos um servidor de Acesso para Cliente do Exchange 2013 na organização do Exchange 2010.

## Coexistência com o Exchange 2007

Em organizações que tenham tanto servidores Exchange 2013 quanto Exchange 2007, os usuários que tenham uma caixa de correio em um servidor de Caixa de Correio do Exchange 2007 podem usar relacionamentos de organização para compartilhar informações de disponibilidade com destinatários em organizações de domínio federado externas. O servidor de Caixa de Correio deve ter o Exchange 2007 SP2 ou superior, e você deve ter pelo menos um servidor de Acesso para Cliente do Exchange 2013 na organização do Exchange. Você pode usar os relacionamentos de organização, introduzindo um único servidor de Acesso para Cliente do Exchange 2013 na organização, oferecendo uma solução mais robusta que as soluções que sincronizam as informações de disponibilidade e exigem a sincronização da GAL.

Ao usar o Outlook 2010 ou o Outlook Web App para agendar uma reunião em um servidor Exchange 2007, o usuário que tem uma caixa de correio em um servidor Exchange 2007 pode ver as informações de disponibilidade de um usuário na organização externa. As informações de disponibilidade de caixas de correio do Exchange 2007 estão visíveis para os destinatários na organização externa.

As diretivas de compartilhamento são atribuídas aos usuários da caixa de correio do Exchange 2013. Para usar diretivas de compartilhamento, uma caixa de correio deve estar localizada em um servidor de Caixa de Correio do Exchange 2013. Somente clientes do Outlook 2010 e do Outlook Web App podem ser usados para gerar ou responder a convites de compartilhamento.

Voltar ao início

## Documentação de compartilhamento

A tabela a seguir contém links para tópicos que irão ajudar você a aprender sobre e gerenciar o compartilhamento no Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="federation-exchange-2013-help.md">Federação</a></p></td>
<td><p>Saiba mais sobre a infraestrutura de confiança subjacente que oferece suporte a compartilhamento, um método fácil para os usuários compartilharem informações com destinatários externos.</p></td>
</tr>
<tr class="even">
<td><p><a href="organization-relationships-exchange-2013-help.md">Relações da organização</a></p></td>
<td><p>Saiba mais sobre os relacionamentos individuais entre organizações do Exchange que permitem o compartilhamento de disponibilidade do calendário.</p></td>
</tr>
<tr class="odd">
<td><p><a href="sharing-policies-exchange-2013-help.md">Diretivas de compartilhamento</a></p></td>
<td><p>Saiba mais sobre as políticas de pessoa-para-pessoa que permitem compartilhamento.</p>
<p></p></td>
</tr>
</tbody>
</table>

