---
title: Alterar os ícones de indicadores e os conjuntos de indicadores (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8a056adf-4473-473d-9b0c-314675af7bfd
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: d681a7b5e9c72283d924970d843582bb82b8522c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130703"
---
# <a name="change-indicator-icons-and-indicator-sets-report-builder-and-ssrs"></a>Alterar os ícones de indicadores e os conjuntos de indicadores (Construtor de Relatórios e SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece conjuntos de indicadores pré-configurados, que podem nem sempre descrevam seus dados com eficiência e funciona bem no relatório entregue. Este tópico fornece procedimentos para alterar a aparência de ícones de indicador e alterar os conjuntos de indicadores para incluir ícones de indicadores diferentes e mais ou menos ícones.  
  
 Opções como cores podem ser definidas com o uso de expressões. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-color-of-an-indicator-icon"></a>Para alterar a cor de um ícone de indicador  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Clique na seta para baixo na coluna **Cor** ao lado do ícone que você deseja alterar e clique na cor a ser usada, **Sem Cor**ou **Mais cores**.  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define o valor da opção **Cor** .  
  
     Se você clicou em **Mais Cores**, a caixa de diálogo **Selecionar Cor** é aberta, na qual é possível escolher de uma ampla gama de cores. Para obter mais informações sobre suas opções, consulte [Caixa de diálogo Selecionar Cor &#40;Construtor de Relatórios e SSRS&#41;](../select-color-dialog-box-report-builder-and-ssrs.md). Clique em **OK** para fechar a caixa de diálogo **Selecionar Cor** .  
  
4.  Clique em **OK**.  
  
### <a name="to-change-the-icon"></a>Para alterar o ícone  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Clique na seta para baixo ao lado do ícone que você deseja alterar e selecione outro ícone.  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define o valor da opção **Ícone** .  
  
4.  Clique em **OK**.  
  
### <a name="to-use-a-custom-image-as-an-indicator-icon"></a>Para usar uma imagem personalizada como um ícone de indicador  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Clique na seta para baixo ao lado do ícone que você deseja alterar e selecione **Imagem**.  
  
4.  Na lista **Selecionar a origem da imagem** , clique em **Externa**, **Inserida**ou **Banco de Dados**.  
  
5.  Dependendo da origem da imagem, siga um destes procedimentos:  
  
    -   Para usar uma imagem armazenada externamente ao relatório, clique em **Procurar** e localize a imagem. O relatório incluirá uma referência para a imagem.  
  
    -   Para usar uma imagem inserida no relatório, clique em **Importar** e localize a imagem. A imagem será adicionada à definição de relatório e salva com ela.  
  
    -   Para usar uma imagem que esteja em um banco de dados, na lista **Usar este campo** . Selecione o campo na lista e, na lista **Usar este tipo MIME** , selecione o tipo MIME da imagem.  
  
6.  Clique em **OK**.  
  
### <a name="to-add-an-icon-to-the-indicator-set"></a>Para adicionar um ícone ao conjunto de indicadores  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Clique em **Adicionar**. Um indicador é adicionado, usando o ícone padrão e a opção **Sem Cor** .  
  
     Configure o indicador para usar a cor e o ícone desejado. Os procedimentos anteriores neste tópico descrevem a etapa para fazer isso.  
  
4.  Clique em **OK**.  
  
### <a name="to-delete-an-icon-to-the-indicator-set"></a>Para excluir um ícone do conjunto de indicadores  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Selecione o ícone a ser excluído e clique em **Excluir**.  
  
4.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  