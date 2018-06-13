---
title: 'Simplificar a URL do Outlook Web App para configuração híbrida do Office 365: Exchange 2013 Help'
TOCTitle: Simplificar a URL do Outlook Web App para configuração híbrida do Office 365
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259173
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Simplificar a URL do Outlook Web App para configuração híbrida do Office 365

 

_**Tópico modificado em:**2016-11-11_

Saiba como configurar a URL do Outlook na Web (Outlook Web App) para usuários de caixa de correio baseada em nuvem em um ambiente híbrido.

A experiência do usuário é a maior preocupação das organizações que migram para o Office 365 de um Exchange local. Os usuários precisam de acesso ininterrupto às caixas de correio, independentemente do local ou de quando as caixas de correio serão migradas. Nesse sentido, o histórico de coexistência do Outlook na Web (anteriormente conhecido como Outlook Web App) é importante.

Considere o seguinte cenário: uma empresa usa uma implantação híbrida para migrar algumas das caixas de correio do Exchange local para o Office 365. Na sexta-feira antes da migração, os usuários acessaram as caixas de correio locais deles usando a URL https://mail.contoso.com/owa. Na segunda-feira após a migração, esses mesmos usuários passaram a receber uma mensagem de erro ao tentar acessar as respectivas caixas de correio usando essa URL.

Para permitir que os usuários afetados se conectem às caixas de correio deles usando o Outlook na Web, há duas possibilidades:

  - **Informe a nova URL aos usuários (por exemplo, https://outlook.com/owa/contoso.com)**   Esta opção pode gerar os seguintes problemas:
    
      - A URL é complexa.
    
      - A experiência é complicada para os usuários afetados.

  - **Configure o TargetOWAUrl definindo o relacionamento de organização**   Esta opção pode gerar os seguintes problemas:
    
      - O ponto de extremidade das caixas de correio baseadas em nuvem é externo, portanto ele não faz parte do domínio que os usuários esperam.
    
      - O ponto de extremidade exige o domínio da URL a fim de fazer a distinção entre empresas do Office 365 e ofertas de consumo do outlook.com.
    
      - O ponto de extremidade faz com que os usuários recebam avisos de incompatibilidade de certificado.

Para eliminar esses problemas com as caixas de correio dos usuários, faça o seguinte:

1.  **Crie um registro CNAME no DNS (por exemplo, cloudowa.contoso.com) que aponte para mail.office365.com**
    
      - Não deixe de criar esse registro CNAME no DNS interno e externo (público), já que os usuários podem usar conexões de Internet internas ou externas.
    
      - Em nosso exemplo, o domínio contoso.com é usado na solicitação (a parte cloudowa é descartada). Isso significa que não é necessário especificar o domínio na URL.

2.  **Configure o redirecionamento do Outlook na Web no relacionamento de organização local**   Para fazer isso, use a seguinte sintaxe no Shell de Gerenciamento do Exchange, no Exchange local:
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    Por exemplo, se o registro CNAME que você criou na etapa 1 for cloudowa.contoso.com, execute o seguinte comando:
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **Observações:**
    
      - Use http, não https.
    
      - O valor /owa à direita é necessário no relacionamento de organização, mas os usuários não precisam inseri-lo na URL.

## Vários prompts de autenticação

Os usuários podem receber vários prompts de autenticação, dependendo das seguintes condições:

  - O local do qual se conectam (conexões de Internet externas e internas).

  - Se há computadores ingressados ou não no domínio.

  - Se vocês estão usando a federação de identidades no ambiente híbrido.

Veja na tabela a seguir a descrição da experiência de prompt de autenticação que os usuários podem esperar.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Método de autenticação</th>
<th>Computador do cliente</th>
<th>Experiência de prompt de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Federação de identidades</p></td>
<td><p>Conexão interna com a Internet</p></td>
<td><p>Prompt único</p></td>
</tr>
<tr class="even">
<td><p>Federação de identidades</p></td>
<td><p>Conexão externa com a Internet</p></td>
<td><p>Prompt duplo</p></td>
</tr>
<tr class="odd">
<td><p>Nenhuma federação de identidades</p></td>
<td><p>Domínio ingressado (interno ou externo)</p></td>
<td><p>Prompt duplo</p></td>
</tr>
<tr class="even">
<td><p>Com ou sem federação de identidades</p></td>
<td><p>Domínio não ingressado (interno ou externo)</p></td>
<td><p>Prompt duplo</p></td>
</tr>
</tbody>
</table>


**Observação:** A federação de identidades exige que o ponto de extremidade do AD FS seja configurado na zona da Intranet do Internet Explorer, conforme descrito no tópico [https://go.microsoft.com/fwlink/p/?linkid=834460](https://go.microsoft.com/fwlink/p/?linkid=83446), e que o AD FS seja configurado de acordo com a orientação geral do Office 365.

