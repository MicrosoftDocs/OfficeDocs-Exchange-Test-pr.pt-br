---
title: 'Requisitos de certificado para implantações híbridas: Exchange 2013 Help'
TOCTitle: Requisitos de certificado para implantações híbridas
ms:assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh563848(v=EXCHG.150)
ms:contentKeyID: 50487111
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisitos de certificado para implantações híbridas

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Em uma implantação híbrida, os certificados digitais são uma parte importante da proteção da comunicação entre a organização local do Exchange e o Office 365. Os certificados permitem que cada organização do Exchange confie na identidade de outra. Os certificados também ajudam a garantir que cada organização do Exchange esteja se comunicando com a origem certa.

Em uma implantação híbrida, vários serviços fazem uso de certificados:

  - **Azure Active Directory Connect (Azure AD Connect) com AD FS (Servidores de Federação do Active Directory)**   Se você selecionar implantar o Azure AD Connect com AD FS como parte de sua implantação híbrida, um certificado emitido por uma CA (autoridade de certificação) independente confiável é usado para estabelecer uma confiança entre clientes Web e proxies de servidor de federação, para assinar tokens de segurança e para descriptografar tokens de segurança.
    
    Saiba mais em [Certificados](http://go.microsoft.com/fwlink/p/?linkid=205993).

  - **Federação do Exchange**   Um certificado autoassinado é usado para criar uma conexão segura entre os servidores locais do Exchange e o sistema de autenticação do Azure Active Directory.
    
    Saiba mais em [Compartilhamento](https://technet.microsoft.com/pt-br/library/dd638083\(v=exchg.150\)).

  - **Serviços do Exchange**   Certificados emitidos por uma CA de terceiros confiável são usados para ajudar a proteger a comunicação de protocolo SSL entre servidores do Exchange e clientes. Serviços que usam certificados incluem Outlook na Web, Exchange ActiveSync, Outlook em Qualquer Lugar e o transporte de mensagens seguro.

  - **Servidores existentes do Exchange**   Seus servidores existentes do Exchange podem fazer uso de certificados para ajudar a proteger a comunicação do Outlook na Web, o transporte de mensagens e assim por diante. Dependendo de como os certificados são usados em seus servidores do Exchange, podem ser usados certificados autoassinados ou certificados emitidos por uma CA de terceiros confiável.

## Requisitos de certificação para uma implantação híbrida

Ao configurar uma implantação híbrida, você deve usar e configurar os certificados que adquiriu de uma CA de terceiros confiável. O certificado usado para o transporte de email híbrido seguro deve ser instalado em todos os servidores locais de Caixa de Correio (Exchange 2016 e mais recentes) e de Acesso para Cliente (Exchange 2013 e mais antigos).


> [!IMPORTANT]
> Se você estiver configurando uma implantação híbrida em uma organização com Exchange Servers implantados em várias florestas do Active Directory, deverá usar um certificado de CA de terceiros separado para <EM>cada</EM> floresta do Active Directory.




> [!TIP]
> Quando servidores de Transporte de Borda do Exchange são implantados em uma organização local, esse certificado também deve ser instalado em todos os servidores de Transporte de Borda. Cada servidor de transporte deve usar um certificado que compartilha a mesma CA de emissão e o mesmo assunto para o email seguro híbrido funcionar corretamente.



Vários serviços, como AD FS, federação do Exchange, serviços e Exchange exigem certificados. Dependendo da sua organização, pode ser necessário executar um dos procedimentos a seguir:

  - Usar um certificado de terceiros usado por todos os serviços em vários servidores.

  - Usar um certificado de terceiros para cada servidor que oferece serviços.

A escolha entre o uso do mesmo certificado para todos os serviços ou de um certificado dedicado a cada serviço depende da sua organização e do serviço que está sendo implementado. Aqui estão alguns itens a serem levados em conta para cada opção:

  - **Certificado de terceiros em múltiplos servidores**   Certificados de terceiros usados por serviços em vários servidores podem ser um pouco mais baratos, mas podem complicar a renovação e a substituição. A complicação acontece porque, quando um certificado precisa ser substituído, ele deve ser substituído em todos os servidores nos quais foi instalado.

  - **Certificado de terceiros para cada servidor**   O uso de um certificado dedicado para cada servidor que hospede serviços permite configurar o certificado especificamente para os serviços desse servidor. Se for necessário substituir o certificado ou renová-lo, basta substituí-lo no servidor no qual os serviços estão instalados. Os outros servidores não são afetados.

Recomendamos o uso de um certificado de terceiros dedicado para cada servidor AD FS opcional, outro certificado para os serviços do Exchange para sua implantação híbrida e, caso necessário, outro certificado em seus servidores do Exchange para outros serviços ou recursos necessários. A confiança de federação local configurada como parte do compartilhamento delegado em uma implantação híbrida usa um certificado autoassinado por padrão. A não ser que você tenha necessidades específicas, não há a necessidade de uso de um certificado de terceiros com a confiança da federação configurada como parte de uma implantação híbrida.

Os serviços instalados em um único servidor podem exigir a configuração de vários FQDNs (nomes de domínio totalmente qualificados) para o servidor. Você deve adquirir um certificado que aceite o número máximo necessário de FQDNs. Os certificados consistem no nome da entidade (também denominado nome principal) e um ou mais SANs (nomes alternativos de entidade). O nome da entidade é o FQDN para que o certificado seja emitido e deve usar o domínio SMTP principal que é compartilhado entre as organizações locais e do Exchange Online. Os SANs são FQDNs adicionais que podem ser somados a um certificado além do nome da entidade. Se for necessário um certificado para dar suporte a cinco FQDNs, adquira um certificado que permita que cinco domínios sejam adicionados ao certificado: um nome de entidade e quatro SANs.

A tabela a seguir descreve os FQDNs mínimos sugeridos que devem ser incluídos em certificados configurados para uso em uma implantação híbrida.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Serviço</th>
<th>FQDN sugerido</th>
<th>Campo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Domínio de SMTP principal compartilhado</p></td>
<td><p>contoso.com</p></td>
<td><p>Nome da entidade</p></td>
</tr>
<tr class="even">
<td><p>Descoberta Automática</p></td>
<td><p>Rótulo que corresponde ao FQDN de Descoberta Automática externo de seu servidor de Acesso para Cliente do Exchange 2013, como autodiscover.contoso.com</p></td>
<td><p>Nome alternativo da entidade</p></td>
</tr>
<tr class="odd">
<td><p>Transporte</p></td>
<td><p>Rótulo que corresponde ao FQDN externo de seus servidores de Transporte de Borda existente, como edge.contoso.com</p></td>
<td><p>Nome alternativo da entidade</p></td>
</tr>
</tbody>
</table>

