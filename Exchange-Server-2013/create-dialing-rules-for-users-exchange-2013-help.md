---
title: 'Criar regras de discagem para usuários: Exchange 2013 Help'
TOCTitle: Criar regras de discagem para usuários
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51407911
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar regras de discagem para usuários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

Grupos de regras de discagem consistem entradas de regras de discagem. Regras de discagem são usadas para modificar um número de telefone antes de enviá-la a um sistema telefônico de local (PBX) ou no IP PBX para chamadas de saída. Regras de discagem têm duas finalidades:

  - Eles especificam os números que podem ser discados para chamadas de saída. Quando você cria uma regra de discagem, você pode especificar os formatos de número que podem ser discados. Qualquer número que não corresponda a um dos formatos especificado será rejeitado. Se você não definir quaisquer regras de discagem, os chamadores podem fazer chamadas dentro da sua organização, mas não é possível realizar qualquer chamadas.

  - Eles transformam os números discados antes de enviá-los a seu sistema de telefone local. Regras de discagem podem remover números de ou adicionar números para o número discado. Por exemplo, você pode usar as regras de discagem para adicionar o código de acesso de linha externa para o seu sistema telefônico ou para adicionar ou remover o código de país/região para números de longa distância ou locais.

Para especificar os tipos de chamadas de saída que você deseja permitir para um plano de discagem de UM, você cria um grupo de regras de discagem com regras de discagem e depois usá-los para autorizar chamadas de saída para os usuários do Outlook Voice Access e os chamadores que discarem para um atendedor automático. Você criar grupos de regras de discagem separados para o país/região e para chamadas internacionais.


> [!TIP]
> Se você estiver integrando a Unificação de mensagens com o Microsoft Lync Server, é recomendável que você crie pelo menos um grupo de regras de discagem e autoriza a esse grupo de regras de discagem nos planos de discagem URI do SIP, diretivas de caixa de correio de UM e atendedores automáticos para permitir que todas as chamadas de saída para serem encaminhadas ao Lync Servers.



Para outras tarefas de gerenciamento para discagem externa, consulte [Permitindo que usuários façam chamadas de procedimentos](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Exemplos de regras de discagem comumente usadas


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Padrão de número</strong></p></td>
<td><p><strong>Número discado</strong></p></td>
<td><p><strong>Quando você usaria esta regra de discagem?</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>Permitir todas as chamadas de saída.</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>Impedir que usuários obtendo um ramal interno ou um erro quando eles esquecerem discar o número de linha de fora do access.</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>Permitir que todos os números que começam com 1.</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>Adicione 1 e os números de 425 para 7 dígitos do código de área local.</p></td>
</tr>
</tbody>
</table>


## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: menos de 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Se você aplicará grupos de regras de discagem às políticas de caixa de correio de Unificação de mensagens, você precisará confirme se uma diretiva de caixa de correio UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Se você aplicará grupos de regras de discagem para atendedores automáticos, você precisará confirme se um atendedor automático de UM foi criado. Para obter etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o EAC para criar uma regra de discagem

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, clique em **Configurar**.

3.  Na página de **Plano de discagem de UM** \> **regras de discagem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") em **regras de discagem do país/região** ou **internacional regras de discagem**.

4.  Na página **Nova regra de discagem**, insira as seguintes informações:
    
      - **Nome da regra de discagem**   Insira o nome da regra de discagem de grupo que você deseja que essa regra seja parte do. Para combiná-lo com outras regras, use o mesmo nome de grupo. Para criar um novo grupo de regras de discagem, insira um novo nome exclusivo.
    
      - **Padrão de número para transformar (máscara de número)**   Insira o padrão de número para transformar antes de discar, por exemplo, 91425xxxxxxx. Se um chamador disca um número que corresponde, Unificação de mensagens transforma-lo ao número discado antes de fazer a chamada. Insira apenas números e o caractere curinga (x). O padrão numérico também é chamado de uma *máscara de número*.
    
      - **Número de Dialed** Insira o número para discar. Use apenas números e o caractere curinga (x), como o número 9xxxxxxx padrão. Caracteres curinga (x) é substituída pelos dígitos do número discado pelo usuário original. Verifique se que o número de caracteres curinga em que o número discado é o mesmo que o número de caracteres curinga no número padrão.
    
      - **Comentário** Insira um comentário ou uma descrição para esta regra de discagem. Você pode usar o comentário para descrever o que a regra faz, por exemplo, "Adicionar um 9 para chamadas de saída".

5.  Clique em **OK** para salvar a regra de discagem. Você pode continuar inserir regras, usando o mesmo nome de grupo de regra de discagem para regras que você deseja autorizar juntos.

