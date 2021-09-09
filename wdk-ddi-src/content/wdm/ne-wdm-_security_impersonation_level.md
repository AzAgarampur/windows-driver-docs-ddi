---
UID: NE:wdm._SECURITY_IMPERSONATION_LEVEL
title: _SECURITY_IMPERSONATION_LEVEL (wdm.h)
description: The SECURITY_IMPERSONATION_LEVEL enumeration type contains values that specify security impersonation levels. Security impersonation levels govern the degree to which a server process can act on behalf of a client process.
old-location: ifsk\security_impersonation_level.htm
tech.root: ifsk
ms.date: 08/03/2021
keywords: ["SECURITY_IMPERSONATION_LEVEL enumeration"]
ms.keywords: "*PSECURITY_IMPERSONATION_LEVEL, PSECURITY_IMPERSONATION_LEVEL, PSECURITY_IMPERSONATION_LEVEL enumeration pointer [Installable File System Drivers], SECURITY_IMPERSONATION_LEVEL, SECURITY_IMPERSONATION_LEVEL enumeration [Installable File System Drivers], SecurityAnonymous, SecurityDelegation, SecurityIdentification, SecurityImpersonation, _SECURITY_IMPERSONATION_LEVEL, ifsk.security_impersonation_level, securitystructures_d049c4aa-1df4-46b1-b789-01f04e939de2.xml, wdm/PSECURITY_IMPERSONATION_LEVEL, wdm/SECURITY_IMPERSONATION_LEVEL, wdm/SecurityAnonymous, wdm/SecurityDelegation, wdm/SecurityIdentification, wdm/SecurityImpersonation"
req.header: wdm.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h, Fltkernel.h
req.target-type: Windows
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: 
req.dll: 
req.irql: 
targetos: Windows
req.typenames: SECURITY_IMPERSONATION_LEVEL, *PSECURITY_IMPERSONATION_LEVEL
f1_keywords:
 - _SECURITY_IMPERSONATION_LEVEL
 - wdm/_SECURITY_IMPERSONATION_LEVEL
 - PSECURITY_IMPERSONATION_LEVEL
 - wdm/PSECURITY_IMPERSONATION_LEVEL
 - SECURITY_IMPERSONATION_LEVEL
 - wdm/SECURITY_IMPERSONATION_LEVEL
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - HeaderDef
api_location:
 - wdm.h
api_name:
 - _SECURITY_IMPERSONATION_LEVEL
 - PSECURITY_IMPERSONATION_LEVEL
 - SECURITY_IMPERSONATION_LEVEL
---

# _SECURITY_IMPERSONATION_LEVEL enumeration (wdm.h)

## -description

The **SECURITY_IMPERSONATION_LEVEL** enumeration type contains values that specify security impersonation levels. Security impersonation levels govern the degree to which a server process can act on behalf of a client process.

## -enum-fields

### -field SecurityAnonymous

The server process cannot obtain identification information about the client and it cannot impersonate the client. It is defined with no value given, and thus, by ANSI C rules, defaults to a value of zero.

### -field SecurityIdentification

The server process can obtain information about the client, such as security identifiers and privileges, but it cannot impersonate the client. This is useful for servers that export their own objects, for example, database products that export tables and views. Using the retrieved client-security information, the server can make access-validation decisions without being able to utilize other services using the client's security context.

### -field SecurityImpersonation

The server process can impersonate the client's security context on its local system. The server cannot impersonate the client on remote systems.

### -field SecurityDelegation

The server process can impersonate the client's security context on remote systems.

## -remarks

Impersonation is the ability of a process to take on the security attributes of another process.

Be aware of the following derived types:

```cpp
#define DEFAULT_IMPERSONATION_LEVEL SecurityImpersonation
#define SECURITY_MAX_IMPERSONATION_LEVEL SecurityDelegation
#define SECURITY_MIN_IMPERSONATION_LEVEL SecurityAnonymous
```

## -see-also

[LUID](../igpupvdev/ns-igpupvdev-_luid.md)

[LUID_AND_ATTRIBUTES](./ns-wdm-_luid_and_attributes.md)

[PRIVILEGE_SET](/previous-versions/windows/hardware/drivers/ff551860(v=vs.85))

[PsImpersonateClient](../ntifs/nf-ntifs-psimpersonateclient.md)

[PsReferenceImpersonationToken](../ntifs/nf-ntifs-psreferenceimpersonationtoken.md)

[SECURITY_SUBJECT_CONTEXT](/windows-hardware/drivers/kernel/eprocess)

[SID_AND_ATTRIBUTES](../ntifs/ns-ntifs-_sid_and_attributes.md)

[SeAccessCheck](./nf-wdm-seaccesscheck.md)

[SeQueryInformationToken](../ntifs/nf-ntifs-sequeryinformationtoken.md)

[ZwQueryInformationToken](/previous-versions/ff567055(v=vs.85))