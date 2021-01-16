---
UID: NS:ntpoapi._COUNTED_REASON_CONTEXT
title: _COUNTED_REASON_CONTEXT (ntpoapi.h)
description: The COUNTED_REASON_CONTEXT structure contains one or more strings that give reasons for a power request.
old-location: kernel\counted_reason_context.htm
tech.root: kernel
ms.date: 04/30/2018
keywords: ["COUNTED_REASON_CONTEXT structure"]
ms.keywords: "*PCOUNTED_REASON_CONTEXT, COUNTED_REASON_CONTEXT, COUNTED_REASON_CONTEXT structure [Kernel-Mode Driver Architecture], PCOUNTED_REASON_CONTEXT, PCOUNTED_REASON_CONTEXT structure pointer [Kernel-Mode Driver Architecture], _COUNTED_REASON_CONTEXT, kernel.counted_reason_context, kstruct_a_52baf683-dfd2-4004-abed-e9ae6221c342.xml, wdm/COUNTED_REASON_CONTEXT, wdm/PCOUNTED_REASON_CONTEXT"
req.header: ntpoapi.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h, Ntpoapi.h
req.target-type: Windows
req.target-min-winverclnt: Supported in Windows 7 and later versions of the Windows operating system.
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
req.typenames: COUNTED_REASON_CONTEXT, *PCOUNTED_REASON_CONTEXT
f1_keywords:
 - _COUNTED_REASON_CONTEXT
 - ntpoapi/_COUNTED_REASON_CONTEXT
 - PCOUNTED_REASON_CONTEXT
 - ntpoapi/PCOUNTED_REASON_CONTEXT
 - COUNTED_REASON_CONTEXT
 - ntpoapi/COUNTED_REASON_CONTEXT
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - HeaderDef
api_location:
 - wdm.h
api_name:
 - _COUNTED_REASON_CONTEXT
 - PCOUNTED_REASON_CONTEXT
 - COUNTED_REASON_CONTEXT
---

# _COUNTED_REASON_CONTEXT structure (ntpoapi.h)


## -description

The <b>COUNTED_REASON_CONTEXT</b> structure contains one or more strings that give reasons for a power request.

## -struct-fields

### -field Version

The version number of the structure. Set this member to DIAGNOSTIC_REASON_VERSION.

### -field Flags

Indicates whether the structure contains a simple reason string or a detailed set of reason strings. Set this member to one of the following constants:

<ul>
<li>
DIAGNOSTIC_REASON_SIMPLE_STRING

</li>
<li>
DIAGNOSTIC_REASON_DETAILED_STRING

</li>
</ul>
If <b>Flags</b> = DIAGNOSTIC_REASON_SIMPLE_STRING, the <b>SimpleString</b> member of the union is valid. If <b>Flags</b> = DIAGNOSTIC_REASON_DETAILED_STRING, the <b>ResourceFileName</b>, <b>ResourceReasonId</b>, <b>StringCount</b>, and <b>ReasonStrings</b> members are valid (and the <b>SimpleString</b> member is not valid).

### -field DUMMYUNIONNAME

### -field DUMMYUNIONNAME.DUMMYSTRUCTNAME

### -field DUMMYUNIONNAME.DUMMYSTRUCTNAME.ResourceFileName

A pointer to a wide-character, null-terminated string that contains the pathname of a resource file. This resource file contains one or more localized strings that give reasons for a power request. This member is optional and can be specified as <b>NULL</b> or as an empty string if no resource file is required. This member is valid only if <b>Flags</b> = DIAGNOSTIC_REASON_DETAILED_STRING.

### -field DUMMYUNIONNAME.DUMMYSTRUCTNAME.ResourceReasonId

The resource ID assigned to the first reason string in the resource file that is specified by <b>ResourceFileName</b>. This member is valid only if <b>Flags</b> = DIAGNOSTIC_REASON_DETAILED_STRING.

### -field DUMMYUNIONNAME.DUMMYSTRUCTNAME.StringCount

The number of reason strings in the <b>ReasonStrings</b> array or in the resource file that is specified by <b>ResourceFileName</b>. This member is valid only if <b>Flags</b> = DIAGNOSTIC_REASON_DETAILED_STRING.

### -field DUMMYUNIONNAME.DUMMYSTRUCTNAME.ReasonStrings

A pointer to an array of string pointers. Each array element is a pointer to a wide-character, null-terminated string. The number of array elements is specified by <b>StringCount</b>. This member is valid only if <b>Flags</b> = DIAGNOSTIC_REASON_DETAILED_STRING.

### -field DUMMYUNIONNAME.SimpleString

A pointer to a wide-character, null-terminated string that explains the reason for a power request. This member is valid only if <b>Flags</b> = DIAGNOSTIC_REASON_SIMPLE_STRING.

## -remarks

This structure is used by the <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocreatepowerrequest">PoCreatePowerRequest</a> routine.

The <a href="/windows-hardware/drivers/kernel/power-manager">power manager</a> uses the reason string or strings contained in this structure as a diagnostic aid during functional and performance testing.

The <b>COUNTED_REASON_CONTEXT</b> structure can contain either a simple reason string or a set of detailed reason strings. If <b>Flags</b> = DIAGNOSTIC_REASON_SIMPLE_STRING, the <b>SimpleString</b> member points to a string that explains the reason for the power request. If <b>Flags</b> = DIAGNOSTIC_REASON_DETAILED_STRING, the <b>ResourceFileName</b>, <b>ResourceReasonId</b>, <b>StringCount</b>, and <b>ReasonStrings</b> members can give a detailed set of reasons for the power request.

The DIAGNOSTIC_REASON_DETAILED_STRING flag supports localization. If the localized resource file specified by <b>ResourceFileName</b> exists, the power manager retrieves the resource string specified by <b>ResourceReasonId</b> from the file and then formats the string, replacing `%1`, `%2`, etc. placeholders with corresponding items from the <b>ReasonStrings</b> array. Other format specifiers used with **FormatMessageW** are not supported.

The power manager retrieves the resource strings from [STRINGTABLE resources](/windows/win32/menurc/stringtable-resource).

## -see-also

<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocreatepowerrequest">PoCreatePowerRequest</a>

