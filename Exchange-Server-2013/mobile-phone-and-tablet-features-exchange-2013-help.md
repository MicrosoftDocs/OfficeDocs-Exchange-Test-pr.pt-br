---
title: 'Telefone celular e recursos de tablet: Exchange 2013 Help'
TOCTitle: Telefone celular e recursos de tablet
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50556271
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Telefone celular e recursos de tablet

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Os usuários podem acessar seus emails, calendário, contatos e informações sobre a tarefa em telefones celulares, tablets e outros dispositivos portáteis através do Microsoft Exchange ActiveSync. Eles também podem usá-lo para configurar sua assinatura e as respostas automáticas. Uma ampla variedade de telefones e dispositivos móveis funcionam com o Exchange ActiveSync.


> [!TIP]
> Embora nos referimos consistentemente dispositivos que acessam Exchange Server 2013 como telefones celulares, existem muitos dispositivos que podem acessar Exchange 2013, mas não têm a funcionalidade de telefone celular. O termo "telefone celular" nesta documentação se refere a esses dispositivos.



## Dispositivos de compatíveis com o ActiveSync do Exchange

Os usuários podem tirar proveito dos recursos avançados do Exchange ActiveSync selecionando celulares que sejam compatíveis com Exchange ActiveSync. Esses telefones móveis estão disponíveis a partir de vários fabricantes e em muitas operadoras. Para obter mais informações, consulte a documentação do celular específico.

Celulares que sejam compatíveis com Microsoft Exchange incluem o seguinte:

  - **Apple**   O Apple iPhone, iPod Touch e iPad suportem Exchange ActiveSync.

  - **Windows Phone**   Suportem a Windows Phone 8, Windows Phone 7 e versões anteriores do Exchange ActiveSync.

  - **Android**   Muitos telefones móveis e tablets com o sistema operacional Android suportam Exchange ActiveSync. No entanto, esses dispositivos móveis podem não suportar todas as diretivas de caixa de correio de dispositivo móvel disponíveis. Para obter mais informações, consulte [Políticas de caixa de correio para dispositivos móveis](mobile-device-mailbox-policies-exchange-2013-help.md).

## Recursos de software do Windows Phone

Celulares que tinha uma versão do Windows software de telefone como seu sistema operacional oferecem a funcionalidade de maior durante a sincronização com o Exchange 2013. A tabela a seguir lista as diretivas de caixa de correio de dispositivo móvel que estão disponíveis com o Windows Phone 8 e Windows Phone 7.

### Windows Phone 7 e 8 recursos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sistema operacional</th>
<th>Recursos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 suporta as seguintes políticas de caixa de correio de dispositivo móvel:</p>
<ul>
<li><p>Permitir senha simples de dispositivo</p></li>
<li><p>Senha alfanumérica necessária</p></li>
<li><p>Senha de dispositivo habilitada</p></li>
<li><p>Expiração de senha de dispositivo</p></li>
<li><p>IRM habilitado</p></li>
<li><p>Tentativas fracassadas de senha de dispositivo máximo</p></li>
<li><p>Bloqueio de tempo máximo de inatividade dispositivo</p></li>
<li><p>Mínimo de caracteres complexos na senha do dispositivo</p></li>
<li><p>Comprimento da senha de dispositivo mínimos</p></li>
<li><p>Exigir Criptografia do Dispositivo</p></li>
<li><p>Apagamento remoto</p></li>
</ul>

> [!WARNING]
> Se sua organização usa outras configurações de diretiva de caixa de correio de dispositivo móvel, você precisará definir a política de <STRONG>dispositivos não provisionáveis de permitir</STRONG> como true. Isso pode ter implicações de segurança da sua organização, pois outros telefones e dispositivos móveis que não atendem a todos os requisitos das suas configurações de política de dispositivo móvel serão permitidos para sincronizar. Para obter mais informações, consulte <A href="mobile-device-mailbox-policies-exchange-2013-help.md">Políticas de caixa de correio para dispositivos móveis</A>.


</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Telefones celulares Windows Phone 7 suporta apenas um subconjunto de todas as configurações de diretiva de caixa de correio do Exchange ActiveSync:</p>
<ul>
<li><p>Senha necessária</p></li>
<li><p>Tamanho mínimo da senha</p></li>
<li><p>Bloqueio máximo de tempo de inatividade</p></li>
<li><p>Tentativas fracassadas de senha de dispositivo máximo</p></li>
<li><p>Permitir senha simples</p></li>
<li><p>Expiração da senha</p></li>
<li><p>Histórico da senha</p></li>
<li><p>Desabilitar o armazenamento removível</p></li>
<li><p>Desabilitar IrDA</p></li>
<li><p>Desabilitar a sincronização da área de trabalho</p></li>
<li><p>Área de trabalho remota do bloco</p></li>
<li><p>Bloquear o compartilhamento de Internet</p></li>
</ul></td>
</tr>
</tbody>
</table>

