---
title: 'Criando elementos constantes usando SQL: is-constant (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- sql:is-constant
- XSD schemas [SQLXML], constant elements
- element mapping [SQLXML], constant elements
- is-constant annotation
- constant elements [SQLXML]
- annotated XSD schemas, constant elements
ms.assetid: 940eea1b-54f5-445f-b844-c894d9f3941b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc100446eb6dff17125b0df7a60b8c2c82e46277
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013941"
---
# <a name="creating-constant-elements-using-sqlis-constant-sqlxml-40"></a>Criando elementos constantes usando sql:is-constant (SQLXML 4.0)
  Para especificar um elemento Constant, ou seja, um elemento no esquema XSD que não é mapeado para nenhuma tabela ou coluna de banco de dados, você pode `sql:is-constant` usar a anotação. Essa anotação usa um valor Booliano (0 = false, 1 = true). Os valores aceitáveis são 0, 1, true e false. A anotação `sql:is-constant` pode ser especificada em um elemento que não tem nenhum atributo. Se ela for especificada em um elemento com o valor true (ou 1), esse elemento não será mapeado para o banco de dados, mas ainda aparecerá no documento XML.  
  
 A anotação `sql:is-constant` pode ser usada para:  
  
-   Adicionar um elemento de nível superior ao documento XML. XML requer um único elemento de nível superior (elemento root) para o documento.  
  
-   Criar elementos de contêiner, como um ** \<elemento Orders>** que encapsula todos os pedidos.  
  
 A `sql:is-constant` anotação pode ser adicionada a um ** \<elemento>complexo** .  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlis-constant-to-add-a-container-element"></a>a. Especificando sql:is-constant para adicionar um elemento do contêiner  
 Neste esquema XSD anotado, ** \<CustomerOrders>** é definido como um elemento constante, especificando o `sql:is-constant` atributo com um valor de 1. Portanto, ** \<o CustomerOrders>** não está mapeado para nenhuma tabela ou coluna de banco de dados. Esse elemento Constant consiste na ** \<ordem>** elementos filho.  
  
 Embora ** \<CustomerOrders>** não seja mapeado para nenhuma tabela ou coluna de banco de dados, ele ainda aparece no XML resultante como um elemento de contêiner que contém a ** \<ordem>** elementos filho.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
        parent="Sales.Customer"  
        parent-key="CustomerID"  
        child="Sales.SalesOrderHeader"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="CustomerOrders" sql:is-constant="1" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"  
                           sql:relationship="CustOrders"   
                           maxOccurs="unbounded" >  
                <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="OrderDate" type="xsd:date" />  
                   <xsd:attribute name="CustomerID" type="xsd:string" />  
                </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>  
         </xsd:sequence>  
          <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como isConstant.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como isConstantT.xml no mesmo diretório onde você salvou isConstant.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="isConstant.xml">  
            Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (isConstant.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\isConstant.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
<Customer CustomerID="1">   
  <CustomerOrders>   
    <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1" />   
    <Order SalesOrderID="44501" OrderDate="2001-11-01" CustomerID="1" />   
    <Order SalesOrderID="45283" OrderDate="2002-02-01" CustomerID="1" />   
    <Order SalesOrderID="46042" OrderDate="2002-05-01" CustomerID="1" />   
    ...  
  </CustomerOrders>   
</Customer>   
</ROOT>  
```  
  
  
