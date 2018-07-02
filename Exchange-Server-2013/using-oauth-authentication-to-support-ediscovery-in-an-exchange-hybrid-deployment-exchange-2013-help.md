---
title: 'Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange: Exchange 2013 Help'
TOCTitle: Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61292928
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Para executar pesquisas entre locais da Descoberta eletrônica com êxito em uma organização híbrida do Exchange 2013, será necessário configurar a autenticação OAuth (Autorização Aberta) entre suas organizações locais do Exchange e organizações do Exchange Online, de forma que você possa usar a Descoberta eletrônica local para pesquisar em caixas de correio locais e baseadas em nuvem. A autenticação OAuth oferece suporte aos seguintes cenários de Descoberta eletrônica em uma implantação híbrida do Exchange:

  - Pesquisa de caixas de correio locais que usam o Arquivamento do Exchange Online para caixas de correio de arquivamento baseadas em nuvem.

  - Pesquisa de caixas de correio locais e baseadas em nuvem na mesma pesquisa de Descoberta eletrônica.

Para obter instruções detalhadas sobre a configuração da autenticação OAuth a fim de oferecer suporte à Descoberta eletrônica, consulte [Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## O que é autenticação OAuth?

A autenticação OAuth é um protocolo de autenticação de servidor para servidor que permite que aplicativos autentiquem uns aos outros. Com a autenticação OAuth, as credenciais e senhas do usuário não são transferidas de um computador para outro. Em vez disso, a autenticação e a autorização são baseadas na troca de tokens de segurança. Esses tokens concedem acesso a um conjunto específico de recursos por um período determinado.

A autenticação OAuth normalmente envolve três partes: um único servidor de autorização e os dois realms que precisam se comunicar . Os tokens de segurança são emitidos pelo servidor de autorização (também conhecido como servidor do token de segurança) para os dois realms que precisam se comunicar. Esse tokens verificam se as comunicações originadas de um realm devem ser confiadas pelo outro realm. Ao usar a autenticação OAuth entre uma organização local do Exchange e o Exchange Online, a função do servidor de autorização é fornecida pelo ACS (Access Control Services) do Active Directory do Microsoft Azure em sua organização do Office 365. Por exemplo, durante uma pesquisa de Descoberta Eletrônica entre instalações, o ACS do Azure emite tokens que verificam se um administrador ou responsável pela conformidade da organização local do Exchange é capaz de acessar as caixas de correio na organização do Exchange Online e vice-versa.

## Cenários de Descoberta Eletrônica em uma implantação híbrida

A tabela a seguir identifica os cenários de Descoberta Eletrônica em uma implantação híbrida do Exchange que exige a autenticação OAuth.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cenário de Descoberta Eletrônica</th>
<th>Exige autenticação OAuth?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pesquisa em caixas de correio locais do Exchange e em caixas de correio do Exchange Online na mesma pesquisa de Descoberta Eletrônica iniciada a partir da organização local do Exchange. Por exemplo, pesquisar em todas as caixas de correio na organização em uma única pesquisa de Descoberta Eletrônica.</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Pesquisa de caixas de correio locais do Exchange que usam o Arquivamento do Exchange Online para caixas de correio de arquivamento baseadas em nuvem. Quando você usa a Descoberta Eletrônica In-loco, as caixas de correio principal e de arquivamento são pesquisadas.</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Pesquisa de caixas de correio do Exchange Online de uma pesquisa de Descoberta Eletrônica iniciada a partir da organização local do Exchange por um administrador ou responsável pela conformidade.</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Pesquisa de caixas de correio locais usando uma pesquisa de Descoberta Eletrônica iniciada na organização local do Exchange por um administrador ou responsável pela conformidade.</p></td>
<td><p>Não</p>

> [!TIP]
> Conforme discutido anteriormente, a autenticação OAuth seria necessária se as caixas de correio locais fossem configuradas com caixas de correio de arquivamento com base na nuvem.


</td>
</tr>
<tr class="odd">
<td><p>Pesquisa de caixas de correio do Exchange Online de uma pesquisa de Descoberta Eletrônica iniciada do Exchange Online ou do Centro de Descoberta Eletrônica no SharePoint Online por um administrador de locatário do Office 365 ou um responsável pela conformidade conectado a uma conta de usuário do Office 365.</p></td>
<td><p>Não</p></td>
</tr>
</tbody>
</table>


## Configurando a autenticação OAuth para oferecer suporte a Descoberta Eletrônica

Conforme indicado anteriormente, consulte [Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) para obter instruções de configuração da autenticação OAuth a fim de suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange.

Se o OAuth não for configurado para sua implantação híbrida do Exchange, não será possível usar a Descoberta Eletrônica para pesquisar caixas de correio locais do Exchange e do Exchange Online na mesma pesquisa de Descoberta Eletrônica. Você terá que pesquisar caixas de correio locais a partir de uma pesquisa de Descoberta Eletrônica iniciada de sua organização local. Da mesma forma, você pode pesquisar apenas caixas de correio do Exchange Online a partir de uma pesquisa de Descoberta Eletrônica iniciada de sua organização do Exchange Online ou usando o Centro de Descoberta Eletrônica no SharePoint Online. Além disso, não será possível pesquisar caixas de correio locais principais se suas caixas de correio de arquivamento correspondentes residirem no Exchange Online ou em uma organização de Arquivamento do Exchange Online.

## Mais informações

  - Você também pode usar a autenticação OAuth para permitir que outros aplicativos, como SharePoint 2013 e Lync Server 2013, autentiquem no Exchange 2013. Para obter mais informações, consulte [Configurar a autenticação OAuth com o SharePoint 2013 e Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - Você pode configurar a autenticação entre servidores entre o Exchange 2013 e o SharePoint 2013 de modo que os administradores e responsáveis pela conformidade possam usar o Centro de Descoberta Eletrônica no SharePoint 2013 para pesquisar caixas de correio do Exchange 2013. Para obter mais informações, consulte [Configurar o Exchange para o SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - Você pode configurar uma implantação híbrida do Exchange usando o Assistente de configuração híbrida no Exchange 2013. Para uma lista de verificação de configuração implantação híbrida personalizada, passo a passo, consulte o [Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=277105).

