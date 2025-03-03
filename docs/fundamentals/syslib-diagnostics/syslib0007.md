---
title: SYSLIB0007 warning
description: Learn about the obsoletions that generate compile-time warning SYSLIB0007.
ms.date: 10/20/2020
---
# SYSLIB0007: Default implementations of cryptography algorithms not supported

The cryptographic configuration system in .NET Framework doesn't allow for proper cryptographic agility and isn't present in .NET Core and .NET 5+. .NET's backward-compatibility requirements also prohibit the framework from updating certain cryptographic APIs to keep up with advances in cryptography. As a result, the following APIs are marked obsolete, starting in .NET 5.0. Use of these APIs generates warning `SYSLIB0007` at compile time.

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HMAC.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=fullName>

## Workarounds

- The recommended course of action is to replace calls to the now-obsolete APIs with calls to factory methods for specific algorithms, for example, <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType>. This gives you full control over which algorithms are instantiated.

- If you need to maintain compatibility with existing payloads generated by .NET Framework apps that use the now-obsolete APIs, use the replacements suggested in the following table. The table provides a mapping from .NET Framework default algorithms to their .NET 5+ equivalents.

  | .NET Framework | .NET Core / .NET 5.0+ compatible replacement | Remarks |
  | - | - | - |
  | <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.RSA.Create?displayProperty=nameWithType> | |
  | <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.SHA1.Create?displayProperty=nameWithType> | The SHA-1 algorithm is considered broken. Consider using a stronger algorithm if possible. Consult your security advisor for further guidance. |
  | <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | The HMACSHA1 algorithm is discouraged for most modern applications. Consider using a stronger algorithm if possible. Consult your security advisor for further guidance. |
  | <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | The HMACSHA1 algorithm is discouraged for most modern applications. Consider using a stronger algorithm if possible. Consult your security advisor for further guidance. |
  | <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> |

[!INCLUDE [suppress-syslib-warning](includes/suppress-syslib-warning.md)]

## See also

- [Instantiating default implementations of cryptographic abstractions is not supported](../../core/compatibility/cryptography/5.0/instantiating-default-implementations-of-cryptographic-abstractions-not-supported.md)
