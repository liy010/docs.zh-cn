---
title: 将对象标识符映射到加密算法
ms.date: 03/30/2017
helpviewer_keywords:
- digital signatures
- identifiers, mapping object identifiers
- cryptographic algorithms
- mapping object identifiers
- cryptography, mapping object identifiers
ms.assetid: c9673f81-bf9e-47fd-bc6f-6bc1c1c4c15e
ms.openlocfilehash: a5aebac2d392d4540581dfe7c7afff0819968ac0
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2020
ms.locfileid: "69912544"
---
# <a name="mapping-object-identifiers-to-cryptography-algorithms"></a>将对象标识符映射到加密算法
数字签名确保在将数据从一个程序发送到另一个程序时，数据不会被篡改。 通常通过将数学函数应用于要签名的数据的哈希来计算数字签名。 设置要签名的哈希值的格式时，某些数字签名算法会在格式设置操作过程中追加一个 "ASN. 1" 对象标识符（OID）。 OID 标识用于计算哈希的算法。 可以将算法映射到对象标识符，以将加密机制扩展为使用自定义算法。 下面的示例演示如何将对象标识符映射到新的哈希算法。  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MyNewHash="MyNewHashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="NewHash" class="MyNewHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.14.33.42.46"  name="NewHash"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 [ \<oidEntry> 元素](./file-schema/cryptography/oidentry-element.md)包含两个属性。 **OID**特性是对象标识符号。 **Name**属性是[ \<nameEntry> 元素](./file-schema/cryptography/nameentry-element.md)中**name**属性的值。 在将对象标识符映射到简单名称之前，必须先将算法名称映射到类。  
  
## <a name="see-also"></a>另请参阅

- [配置加密类](configure-cryptography-classes.md)
- [加密服务](../../standard/security/cryptographic-services.md)
