---
UID: NS:wdm._FILE_NETWORK_OPEN_INFORMATION
title: _FILE_NETWORK_OPEN_INFORMATION (wdm.h)
description: The FILE_NETWORK_OPEN_INFORMATION structure is used as an argument to ZwQueryInformationFile.
old-location: kernel\file_network_open_information.htm
tech.root: kernel
ms.date: 04/30/2018
keywords: ["FILE_NETWORK_OPEN_INFORMATION structure"]
ms.keywords: "*PFILE_NETWORK_OPEN_INFORMATION, FILE_NETWORK_OPEN_INFORMATION, FILE_NETWORK_OPEN_INFORMATION structure [Kernel-Mode Driver Architecture], PFILE_NETWORK_OPEN_INFORMATION, PFILE_NETWORK_OPEN_INFORMATION structure pointer [Kernel-Mode Driver Architecture], _FILE_NETWORK_OPEN_INFORMATION, kernel.file_network_open_information, kstruct_b_761510b6-751c-457d-a516-cce0d9fa3027.xml, wdm/FILE_NETWORK_OPEN_INFORMATION, wdm/PFILE_NETWORK_OPEN_INFORMATION"
req.header: wdm.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h
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
req.typenames: FILE_NETWORK_OPEN_INFORMATION, *PFILE_NETWORK_OPEN_INFORMATION
f1_keywords:
 - _FILE_NETWORK_OPEN_INFORMATION
 - wdm/_FILE_NETWORK_OPEN_INFORMATION
 - PFILE_NETWORK_OPEN_INFORMATION
 - wdm/PFILE_NETWORK_OPEN_INFORMATION
 - FILE_NETWORK_OPEN_INFORMATION
 - wdm/FILE_NETWORK_OPEN_INFORMATION
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - HeaderDef
api_location:
 - Wdm.h
api_name:
 - _FILE_NETWORK_OPEN_INFORMATION
 - PFILE_NETWORK_OPEN_INFORMATION
 - FILE_NETWORK_OPEN_INFORMATION
---

# _FILE_NETWORK_OPEN_INFORMATION structure


## -description

The <b>FILE_NETWORK_OPEN_INFORMATION</b> structure is used as an argument to <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile">ZwQueryInformationFile</a>.

## -struct-fields

### -field CreationTime

Specifies the time that the file was created.

### -field LastAccessTime

Specifies the time that the file was last accessed.

### -field LastWriteTime

Specifies the time that the file was last written to.

### -field ChangeTime

Specifies the time that the file was last changed.

### -field AllocationSize

Specifies the file allocation size, in bytes. Usually, this value is a multiple of the sector or cluster size of the underlying physical device.

### -field EndOfFile

Specifies the absolute end-of-file position as a byte offset from the start of the file. <b>EndOfFile</b> specifies the byte offset to the end of the file. Because this value is zero-based, it actually refers to the first free byte in the file. In other words, <b>EndOfFile</b> is the offset to the byte immediately following the last valid byte in the file.

### -field FileAttributes

Specifies one or more FILE_ATTRIBUTE_<i>XXX</i> flags. For descriptions of these flags, see the documentation of the <b>GetFileAttributes</b> function in the Microsoft Windows SDK.

## -remarks

FILE_READ_ATTRIBUTES access to the file is required to query this information.

Time values <b>CreationTime</b>, <b>LastAccessTime</b>, <b>LastWriteTime</b>, and <b>ChangeTime</b> are expressed in absolute system time format. Absolute system time is the number of 100-nanosecond intervals since the start of the year 1601 in the Gregorian calendar.

This structure must be aligned on a LONGLONG (8-byte) boundary.

## -see-also

<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile">ZwQueryInformationFile</a>

