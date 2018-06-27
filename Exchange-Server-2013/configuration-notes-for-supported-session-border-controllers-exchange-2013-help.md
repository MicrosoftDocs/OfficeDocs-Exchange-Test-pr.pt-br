---
title: 'Notas de configuração para controladores de borda de sessão suportados: Exchange 2013 Help'
TOCTitle: Notas de configuração para controladores de borda de sessão suportados
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50556295
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Notas de configuração para controladores de borda de sessão suportados

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2017-07-25_

Os Controladores de Borda de Sessão habilitam você a conectar sua rede de telefonia local a um datacenter da Microsoft através de uma conexão de rede pública dedicada. Um SBC fica na borda de sua rede IP local e se conecta a um segundo SBC em um datacenter da Microsoft.

Um SBC exige o uso de certificados digitais para criptografar todo o tráfego entre sua organização local e o datacenter da Microsoft. Você deve obter um certificado digital para o elemento de borda da rede, como um controlador de borda de sessão, que você está usando para se comunicar com implantações híbridas e online do Exchange. Os certificados digitais estabelecem confiança entre sua organização local e o datacenter da Microsoft e habilitam a segurança do protocolo TLS (TLS mútuo). Depois que essa confiança é estabelecida, os elementos de borda de rede em sua organização local e no datacenter da Microsoft trocam chaves de sessão e usam essas chaves para criptografar o tráfego de dados subsequente.

Em implantações híbridas ou online, um gateway de IP de UM representa um SBC. O nome comum do assunto no certificado deve corresponder ao valor do nome de domínio totalmente qualificado (FQDN) no campo Endereço do gateway IP de UM que você criar. Por exemplo, se você especificar o endereço FQDN sbcexternal.contoso.com no seu gateway IP de UM, certifique-se de que o nome do assunto e o nome alternativo do assunto no certificado contenham o mesmo valor: sbcexternal.contoso.com. O nome que você usa faz distinção entre maiúsculas e minúsculas, então, certifique-se de que as maiúsculas e minúsculas estejam iguais no certificado e no gateway IP de UM. Se você estiver usando um SBC da Acme Packet e o nome comum não corresponder ao FQDN do gateway de IP de UM, a chamada será rejeitada com um erro 403.


> [!TIP]
> Como SBCs projetadas para ficam na borda da rede, eles também funcionam como um firewall. Se você configurar um SBC atrás do firewall da organização, ele pode causar problemas de configuração e não é suportado para conectar-se ao Office 365.



## Controladores de borda de sessão com suporte

Os seguintes SBCs foram testados com êxito para interoperabilidade com implantações híbridas e online do Exchange. Observe que os recursos e as compatibilidades dos SBCs podem variar, e a configuração deles pode ser diferente, dependendo de outros equipamentos na sua rede. Entre em contato com o fabricante do SBC para ver se há observações de configuração específicas para a Unificação de Mensagens em uma implantação híbrida ou online.


> [!TIP]
> Exchange Online UM suporte para sistemas de PBX de terceiros por meio de conexões diretas do cliente operado SBCs será finalizado no de 2018 julho. Consulte o blog da equipe <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">suporte para controladores de borda de sessão no Exchange Online Descontinuado Unificação de mensagens</A> Exchange para obter mais informações.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Fornecedor</strong></p></td>
<td><p><strong>Modelo</strong></p></td>
<td><p><strong>Notas de configuração</strong></p></td>
<td><p><strong>Comentários</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme Packet</a></p></td>
<td><p>Net-Net 3820 ou 4500</p></td>
<td><p><strong>Entre em contato com o fornecedor de hardware para obter instruções sobre como configurar o seu dispositivo atualizadas.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Entre em contato com o fornecedor de hardware para obter instruções sobre como configurar o seu dispositivo atualizadas.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Entre em contato com o fornecedor de hardware para obter instruções sobre como configurar o seu dispositivo atualizadas.</strong></p></td>
<td><p>SBC e gateway IP</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>

> [!TIP]
> Deve ter o S3 IOS 15.4 (3) ou posterior instalado.


</td>
<td><p><strong>Entre em contato com o fornecedor de hardware para obter instruções sobre como configurar o seu dispositivo atualizadas.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>Entre em contato com o fornecedor de hardware para obter instruções sobre como configurar o seu dispositivo atualizadas.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>Entre em contato com o fornecedor de hardware para obter instruções sobre como configurar o seu dispositivo atualizadas.</strong></p></td>
<td><p>Opção de SBC para um produto de gateway VoIP</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 ou posterior</p></td>
<td><p><strong>Entre em contato com o fornecedor de hardware para obter instruções sobre como configurar o seu dispositivo atualizadas.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
</tbody>
</table>

