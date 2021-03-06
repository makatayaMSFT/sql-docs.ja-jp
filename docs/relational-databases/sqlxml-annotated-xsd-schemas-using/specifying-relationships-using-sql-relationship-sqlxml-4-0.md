---
title: 'Sql: relationship を使用したリレーションシップの設定 (SQLXML)'
description: 'SQLXML 4.0 の sql: relationship 注釈を使用して、XML 要素間のリレーションシップを指定する方法について説明します。'
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- parent attribute [SQLXML]
- element relationships [SQLXML]
- multiple element relationships
- attribute relationships [SQLXML]
- sql:relationship
- relationship chains [SQLXML]
- IDREF relationships [SQLXML]
- parent-child relationships [SQLXML]
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- relationships [SQLXML], specifying
- unnamed relationships
- ID relationships [SQLXML]
- hierarchical relationships [SQLXML]
- named relationships [SQLXML]
ms.assetid: 98820afa-74e1-4e62-b336-6111a3dede4c
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c050a6b34781fc6312e7d410aeccace29e3dc84
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461763"
---
# <a name="specifying-relationships-using-sqlrelationship-sqlxml-40"></a>sql:relationship を使用した、リレーションシップの指定 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  XML ドキュメント内の要素は関連付けることができます。 要素は階層的に入れ子にでき、要素間に ID、IDREF、または IDREFS のリレーションシップを指定することができます。  
  
 たとえば、XSD スキーマでは、要素に **\<Customer>** 子要素が含まれてい **\<Order>** ます。 スキーマを AdventureWorks データベースにマップすると、要素は **\<Customer>** sales. Customer テーブルにマップされ、 **\<Order>** 要素は SalesOrderHeader テーブルにマップされます。 これらの基になるテーブル (Sales. Customer および SalesOrderHeader) は、顧客が注文を配置するため、関連付けられています。 ここで、Sales.SalesOrderHeader テーブル内の CustomerID は、Sales.Customer テーブル内の CustomerID 主キーを参照する外部キーです。 **Sql: relationship** 注釈を使用すると、マッピングスキーマ要素間にこれらのリレーションシップを設定できます。  
  
 注釈付き XSD スキーマでは、 **sql: relationship** 注釈を使用して、要素のマップ先となる基になるテーブル間の主キーと外部キーのリレーションシップに基づいて、スキーマ要素を階層的に入れ子にします。 **Sql: relationship** 注釈を指定するときは、次のことを確認する必要があります。  
  
-   親テーブル (Sales.Customer) と子テーブル (Sales.SalesOrderHeader)。  
  
-   親テーブルと子テーブル間のリレーションシップを構成する列。 たとえば、親テーブルと子テーブル両方にある CustomerID 列を指定します。  
  
 これらの情報を使用して、適切な階層が生成されます。  
  
 テーブル名と必要な結合情報を指定するには、 **sql: relationship** 注釈で次の属性を指定します。 これらの属性は、要素でのみ有効です **\<sql:relationship>** 。  
  
 **名前**  
 リレーションシップの一意な名前を指定します。  
  
 **親**  
 親リレーション (テーブル) を指定します。 これは省略可能な属性です。この属性を指定しない場合、親テーブル名はドキュメント内の子階層の情報から取得されます。 同じでも異なる親要素を使用する2つの親子階層がスキーマで指定されている場合は、 **\<sql:relationship>** で親属性を指定しません **\<sql:relationship>** 。 この情報はスキーマ内の階層から取得されます。  
  
 **親-キー**  
 親の親キーを指定します。 親キーが複数の列で構成される場合は、値をスペースで区切って指定します。 複数列キーに指定される値と、それに対応する子キーに指定される値の間では、位置的なマッピングが行われます。  
  
 **子**  
 子リレーション (テーブル) を指定します。  
  
 **child-key**  
 親の parent-key を参照する子の、子キーを指定します。 子キーが複数の属性 (列) で構成される場合、child-key の値は、スペースで区切って指定します。 複数列キーに指定される値と、それに対応する親キーに指定される値の間では、位置的なマッピングが行われます。  
  
 **逆条件**  
 で指定されたこの属性 **\<sql:relationship>** は、アップデートグラムによって使用されます。 詳細については、「sql [: relationship での sql: 逆属性の指定](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)」を参照してください。  
  
 **Sql: キーフィールド** の注釈は、子要素を含む要素で指定する必要があります。この要素には、 **\<sql:relationship>** 要素と子の間にが定義され、親要素で指定されたテーブルの主キーは提供されません。 スキーマでが指定されていない場合でも **\<sql:relationship>** 、適切な階層を生成するために **sql: キーフィールド** を指定する必要があります。 詳細については、「 [sql: キーフィールドを使用したキー列の識別](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)」を参照してください。  
  
 結果に適切な入れ子を生成するには、すべてのスキーマで **sql: キーフィールド** を指定することをお勧めします。  
  
## <a name="examples"></a>例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、「 [SQLXML の例を実行するための要件](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)」を参照してください。  
  
### <a name="a-specifying-the-sqlrelationship-annotation-on-an-element"></a>A. 要素に sql:relationship 注釈を指定する  
 次の注釈付き XSD スキーマには、要素と要素が含まれてい **\<Customer>** **\<Order>** ます。 **\<Order>** 要素は要素の子要素です **\<Customer>** 。  
  
 スキーマでは、子要素に **sql: relationship** 注釈が指定されてい **\<Order>** ます。 リレーションシップ自体は、要素で定義され **\<xsd:appinfo>** ます。  
  
 要素は、 **\<relationship>** SalesOrderHeader テーブルの customerid を外部キーとして識別します。これは、sales. Customer テーブルの customerid 主キーを参照します。 したがって、顧客に属する注文は、その要素の子要素として表示され **\<Customer>** ます。  
  
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
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                    sql:relationship="CustOrders" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 上のスキーマでは名前付きリレーションシップを使用しましたが、 名前のないリレーションシップを指定することもできます。 この結果は同じです。  
  
 次は、スキーマを変更し、名前のないリレーションシップを指定した例です。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer"  type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader">  
           <xsd:annotation>  
            <xsd:appinfo>  
              <sql:relationship   
                parent="Sales.Customer"  
                parent-key="CustomerID"  
                child="Sales.SalesOrderHeader"  
                child-key="CustomerID" />  
            </xsd:appinfo>  
           </xsd:annotation>  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 sql-relationship.xml として保存します。  
  
2.  次のテンプレートをコピーし、テキストファイルに貼り付けます。 sql-relationship.xml を保存したディレクトリに sql-relationshipT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-relationship.xml">  
            /Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (sql-relationship.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\sql-relationship.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した [SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 結果セットは次のようになります。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1">   
    <Order OrderID="43860" CustomerID="1" />   
    <Order OrderID="44501" CustomerID="1" />   
    <Order OrderID="45283" CustomerID="1" />   
    <Order OrderID="46042" CustomerID="1" />   
  </Customer>   
</ROOT>  
```  
  
### <a name="b-specifying-a-relationship-chain"></a>B. リレーションシップ チェーンを指定する  
 この例では、AdventureWorks データベースから取得したデータを使用して、次の XML ドキュメントを要求するとします。  
  
```  
<Order SalesOrderID="43659">  
  <Product Name="Mountain Bike Socks, M"/>   
  <Product Name="Sport-100 Helmet, Blue"/>  
  ...  
</Order>  
...  
```  
  
 SalesOrderHeader テーブル内の各注文に対して、XML ドキュメントには1つの要素があり **\<Order>** ます。 各 **\<Order>** 要素には **\<Product>** 、注文で要求された製品ごとに1つの子要素のリストがあります。  
  
 この階層を生成する XSD スキーマを指定するには、OrderOD と ODProduct の 2 つのリレーションシップを指定する必要があります。 OrderOD リレーションシップでは、Sales.SalesOrderHeader テーブルと Sales.SalesOrderDetail テーブル間の親子リレーションシップを指定します。 ODProduct リレーションシップでは、Sales.SalesOrderDetail テーブルと Production.Product テーブル間のリレーションシップを指定します。  
  
 次のスキーマでは、要素の **msdata: relationship** 注釈によっ **\<Product>** て、Orderod と ODProduct の2つの値が指定されています。 これらの値の指定順序は重要です。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <msdata:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  
    <msdata:relationship name="ODProduct"  
          parent="Sales.SalesOrderDetail"  
          parent-key="ProductID"  
          child="Production.Product"  
          child-key="ProductID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID"  
                     msdata:relationship="OrderOD ODProduct">  
          <xsd:complexType>  
             <xsd:attribute name="Name" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
    </xsd:complexType>  
</xsd:schema>  
```  
  
 名前付きリレーションシップを指定する代わりに、匿名のリレーションシップを指定することもできます。 この場合、2つのリレーションシップを記述する... の内容全体が、 **\<annotation>** **\</annotation>** の子要素として表示されます。 **\<Product>**  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID" >  
         <xsd:annotation>  
          <xsd:appinfo>  
           <msdata:relationship   
               parent="Sales.SalesOrderHeader"  
               parent-key="SalesOrderID"  
               child="Sales.SalesOrderDetail"  
               child-key="SalesOrderID" />  
  
           <msdata:relationship   
               parent="Sales.SalesOrderDetail"  
               parent-key="ProductID"  
               child="Production.Product"  
               child-key="ProductID" />  
         </xsd:appinfo>  
       </xsd:annotation>  
       <xsd:complexType>  
          <xsd:attribute name="Name" type="xsd:string" />  
       </xsd:complexType>  
     </xsd:element>  
   </xsd:sequence>  
   <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
  </xsd:complexType>  
 </xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationshipChain.xml として保存します。  
  
2.  次のテンプレートをコピーし、テキストファイルに貼り付けます。 relationshipChain.xml を保存したディレクトリに relationshipChainT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationshipChain.xml">  
            /Order  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationshipChain.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationshipChain.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した [SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 結果セットは次のようになります。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Order SalesOrderID="43659">  
    <Product Name="Mountain Bike Socks, M" />   
    <Product Name="Sport-100 Helmet, Blue" />   
    <Product Name="AWC Logo Cap" />   
    <Product Name="Long-Sleeve Logo Jersey, M" />   
    <Product Name="Long-Sleeve Logo Jersey, XL" />   
    ...  
  </Order>  
  ...  
</ROOT>  
```  
  
### <a name="c-specifying-the-relationship-annotation-on-an-attribute"></a>C. 属性にリレーションシップ注釈を指定する  
 この例のスキーマには、 \<Customer> 子要素を持ち、 \<CustomerID> IDREFS 型の OrderIDList 属性を持つ要素が含まれています。 要素は、 \<Customer> AdventureWorks データベースの Sales. Customer テーブルにマップされます。 既定では、このマッピングのスコープは、子要素または属性に **sql: relation** が指定されていない限り、すべての子要素または属性に適用されます。その場合は、要素を使用して、適切な主キー/外部キーのリレーションシップを定義する必要があり \<relationship> ます。 また、 **リレーションシップ注釈を** 使用して別のテーブルを指定する子要素または属性では、 **リレーションシップ** 注釈も指定する必要があります。  
  
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
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="CustomerID"   type="xsd:string" />   
     </xsd:sequence>  
     <xsd:attribute name="OrderIDList"   
                     type="xsd:IDREFS"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:field="SalesOrderID"  
                     sql:relationship="CustOrders" >  
        </xsd:attribute>  
    </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationship-on-attribute.xml として保存します。  
  
2.  次のテンプレートをコピーして、ファイルに貼り付け、 relationship-on-attribute.xml を保存したディレクトリに relationship-on-attributeT.xml として保存します。 このテンプレートのクエリでは、CustomerID が 1 の顧客が選択されます。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-on-attribute.xml">  
        /Customer[CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationship-on-attribute.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationship-on-attribute.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した [SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 結果セットは次のようになります。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer OrderIDList="43860 44501 45283 46042">  
    <CustomerID>1</CustomerID>   
  </Customer>  
</ROOT>  
```  
  
### <a name="d-specifying-sqlrelationship-on-multiple-elements"></a>D. 複数の要素に sql:relationship を指定する  
 この例では、注釈付き XSD スキーマには、、、およびの各要素が含まれてい **\<Customer>** **\<Order>** **\<OrderDetail>** ます。  
  
 **\<Order>** 要素は要素の子要素です **\<Customer>** 。 **\<sql:relationship>** は子要素で指定されます **\<Order>** 。したがって、顧客に属する注文は、の子要素として表示され **\<Customer>** ます。  
  
 要素には **\<Order>** 、 **\<OrderDetail>** 子要素が含まれます。 **\<sql:relationship>** は子要素で指定されているため、 **\<OrderDetail>** 注文に関連する注文の詳細は、その要素の子要素として表示され **\<Order>** ます。  
  
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
  
    <sql:relationship name="OrderOrderDetail"  
        parent="Sales.SalesOrderHeader"  
        parent-key="SalesOrderID"  
        child="Sales.SalesOrderDetail"  
        child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
              sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                             sql:relationship="OrderOrderDetail"   
                             maxOccurs="unbounded" >  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                    <xsd:attribute name="ProductID" type="xsd:string" />  
                    <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationship-multiple-elements.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 relationship-multiple-elements.xml を保存したディレクトリに relationship-multiple-elementsT.xml として保存します。 このテンプレート内のクエリでは、CustomerID が 1、SalesOrderID が 43860 の顧客の注文情報が返されます。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-multiple-elements.xml">  
        /Customer[@CustomerID=1]/Order[@SalesOrderID=43860]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationship-multiple-elements.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationship-multiple-elements.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した [SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 結果セットは次のようになります。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1">  
     <OrderDetail SalesOrderID="43860" ProductID="761" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="770" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="758" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="765" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="762" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="768" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="763" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="756" OrderQty="1" />   
  </Order>  
</ROOT>  
```  
  
### <a name="e-specifying-the-sqlrelationship-without-the-parent-attribute"></a>E. \<sql:relationship>親属性を指定せずにを指定する  
 この例では、親属性を指定せずにを指定してい **\<sql:relationship>** ます。  たとえば、次の従業員テーブルがあるとします。  
  
```  
Emp1(SalesPersonID, FirstName, LastName, ReportsTo)  
Emp2(SalesPersonID, FirstName, LastName, ReportsTo)  
```  
  
 次の XML ビューには **\<Emp1>** 、 **\<Emp2>** Emp1 テーブルと Emp2 テーブルにマッピングされる要素と要素があります。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="EmpOrders"  
          parent-key="SalesPersonID"  
          child="Sales.SalesOrderHeader"  
          child-key="SalesPersonID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Emp1" sql:relation="Sales.Emp1" type="EmpType" />  
  <xsd:element name="Emp2" sql:relation="Sales.Emp2" type="EmpType" />  
   <xsd:complexType name="EmpType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:relationship="EmpOrders" >  
          <xsd:complexType>  
             <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesPersonID"   type="xsd:integer" />   
        <xsd:attribute name="LastName"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 スキーマで **\<Emp1>** は、要素と要素の両方 **\<Emp2>** が **emptype** 型です。 **Emptype** 型は、 **\<Order>** 子要素とそれに対応するを記述し **\<sql:relationship>** ます。 この場合、 **\<sql:relationship>** **親** 属性を使用してで特定できる1つの親がありません。 この場合、で **親** 属性を指定する必要はありません **\<sql:relationship>** 。 **親** 属性情報は、スキーマ内の階層から取得されます。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  AdventureWorks データベース内に次のテーブルを作成します。  
  
    ```  
    USE AdventureWorks  
    CREATE TABLE Sales.Emp1 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    CREATE TABLE Sales.Emp2 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    ```  
  
2.  テーブルに次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Sales.Emp1 values (279, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Sales.Emp1 values (282, 'Andrew', 'Fuller',1)  
    INSERT INTO Sales.Emp1 values (276, 'Janet', 'Leverling',1)  
    INSERT INTO Sales.Emp2 values (277, 'Margaret', 'Peacock',3)  
    INSERT INTO Sales.Emp2 values (283, 'Steven', 'Devolio',4)  
    INSERT INTO Sales.Emp2 values (275, 'Nancy', 'Buchanan',5)  
    INSERT INTO Sales.Emp2 values (281, 'Michael', 'Suyama',6)  
    ```  
  
3.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationship-noparent.xml として保存します。  
  
4.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 relationship-noparent.xml を保存したディレクトリに relationship-noparentT.xml として保存します。 テンプレート内のクエリでは、すべての要素が選択 \<Emp1> されます (したがって、親は Emp1 です)。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationship-noparent.xml">  
            /Emp1  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationship-noparent.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationship-noparent.xml"  
    ```  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した [SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 結果セットの一部を次に示します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<Emp1 SalesPersonID="276" LastName="Leverling">  
  <Order SalesOrderID="43663" CustomerID="510" />   
  <Order SalesOrderID="43666" CustomerID="511" />   
  <Order SalesOrderID="43859" CustomerID="259" />  
  ...  
</Emp1>  
```  
  
  
