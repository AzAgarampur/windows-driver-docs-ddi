---
UID: NF:fltkernel.FltOplockFsctrlEx
title: FltOplockFsctrlEx function (fltkernel.h)
description: The FltOplockFsctrlEx routine performs various opportunistic lock (oplock) operations on behalf of a minifilter driver.
old-location: ifsk\fltoplockfsctrlex.htm
tech.root: ifsk
ms.date: 01/08/2021
keywords: ["FltOplockFsctrlEx function"]
ms.keywords: FltApiRef_e_to_o_fbf1fd08-c50d-41f9-8d13-5bd8f1265625.xml, FltOplockFsctrlEx, FltOplockFsctrlEx routine [Installable File System Drivers], fltkernel/FltOplockFsctrlEx, ifsk.fltoplockfsctrlex
req.header: fltkernel.h
req.include-header: Fltkernel.h
req.target-type: Universal
req.target-min-winverclnt: This routine is available starting with Windows 8.
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
req.lib: FltMgr.lib
req.dll: Fltmgr.sys
req.irql: <= APC_LEVEL
targetos: Windows
req.typenames: 
f1_keywords:
 - FltOplockFsctrlEx
 - fltkernel/FltOplockFsctrlEx
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - DllExport
api_location:
 - fltmgr.sys
api_name:
 - FltOplockFsctrlEx
---

# FltOplockFsctrlEx function

## -description

The **FltOplockFsctrlEx** routine performs various opportunistic lock (oplock) operations on behalf of a minifilter driver.

## -parameters

### -param Oplock

[in] Opaque oplock pointer for the file. This pointer must have been initialized by a previous call to [**FltInitializeOplock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializeoplock).

### -param CallbackData

[in] Pointer to the [**FLT_CALLBACK_DATA**](ns-fltkernel-_flt_callback_data.md) structure for the I/O operation. This parameter is required and cannot be **NULL**.

### -param OpenCount

[in] Number of user handles for the file, if an exclusive oplock is being requested. Setting a nonzero value for a level 2, R, or RH oplock request indicates that there are byte-range locks on the file. For information about oplock types, see [Oplock Overview](/windows-hardware/drivers/ifs/oplock-overview).

### -param Flags

[in] A bitmask for the associated oplock operations. A minifilter driver sets bits to specify the behavior of **FltOplockFsctrlEx**. The *Flags* parameter has the following options:

| Value | Meaning |
| ----- | ------- |
| OPLOCK_FSCTRL_FLAG_ALL_KEYS_MATCH (0x00000001) | The file system verified that all oplock keys on any handles that are currently open match. By specifying this flag, you allow the oplock package to grant an oplock of level RW or RWH when more than one open handle to the file exists. For more information about oplock types, see [Oplock Overview](/windows-hardware/drivers/ifs/oplock-overview). |

## -returns

**FltOplockFsctrlEx** returns FLT_PREOP_PENDING for some FSCTL operations. For more information, see the reference pages for the FSCTL codes listed in the following Remarks section. Otherwise, **FltOplockFsctrlEx** returns FLT_PREOP_COMPLETE.

## -remarks

A minifilter driver calls **FltOplockFsctrlEx** to perform various opportunistic lock operations for a create operation or file system control I/O operation.

The [**FLT_CALLBACK_DATA**](ns-fltkernel-_flt_callback_data.md) structure pointed to by the *CallbackData* parameter must represent an IRP-based [IRP_MJ_FILE_SYSTEM_CONTROL](/windows-hardware/drivers/kernel/irp-mj-file-system-control) or [IRP_MJ_CREATE](/windows-hardware/drivers/ifs/irp-mj-create) operation.

If the operation is an IRP_MJ_FILE_SYSTEM_CONTROL operation, **FltOplockFsctrlEx** can be used with the following FSCTL codes:

* [FSCTL_OPBATCH_ACK_CLOSE_PENDING](/windows-hardware/drivers/ifs/fsctl-opbatch-ack-close-pending)
* [FSCTL_OPLOCK_BREAK_ACK_NO_2](/windows-hardware/drivers/ifs/fsctl-oplock-break-ack-no-2)
* [FSCTL_OPLOCK_BREAK_ACKNOWLEDGE](/windows-hardware/drivers/ifs/fsctl-oplock-break-acknowledge)
* [FSCTL_OPLOCK_BREAK_NOTIFY](/windows-hardware/drivers/ifs/fsctl-oplock-break-notify)
* [FSCTL_REQUEST_BATCH_OPLOCK](/windows-hardware/drivers/ifs/fsctl-request-batch-oplock)
* [FSCTL_REQUEST_FILTER_OPLOCK](/windows-hardware/drivers/ifs/fsctl-request-filter-oplock)
* [FSCTL_REQUEST_OPLOCK_LEVEL_1](/windows-hardware/drivers/ifs/fsctl-request-oplock-level-1)
* [FSCTL_REQUEST_OPLOCK_LEVEL_2](/windows-hardware/drivers/ifs/fsctl-request-oplock-level-2)
* [FSCTL_REQUEST_OPLOCK](/windows-hardware/drivers/ifs/fsctl-request-oplock)

The FSCTL code is set in the **FsControlCode** member of the [**FLT_PARAMETERS**](ns-fltkernel-_flt_parameters.md) structure for the operation. For more information about **FsControlCode** and other IRP_MJ_FILE_SYSTEM_CONTROL parameters, see [FLT_PARAMETERS for IRP_MJ_FILE_SYSTEM_CONTROL](/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-file-system-control).

For more information about opportunistic locks, see the Microsoft Windows SDK documentation.

If the operation is an [IRP_MJ_CREATE](/windows-hardware/drivers/ifs/irp-mj-create) request, **FltOplockFsctrl** can be used to request a pending filter opportunistic lock if all of the following conditions are true:

* The value of the *OpenCount* parameter must be 1.
* The value of the *DesiredAccess* parameter for the IRP_MJ_CREATE request is FILE_READ_ATTRIBUTES. This parameter is set in the **SecurityContext** member of the FLT_PARAMETERS structure for the operation. For more information, see [FLT_PARAMETERS for IRP_MJ_CREATE](/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-create).
* The value of the *ShareAccess* parameter for the IRP_MJ_CREATE operation is FILE_SHARE_READ, FILE_SHARE_WRITE, or FILE_SHARE_DELETE. This parameter is set in the **ShareAccess** member of the FLT_PARAMETERS structure for the operation. For more information, see [FLT_PARAMETERS for IRP_MJ_CREATE](/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-create).

Filters and file systems that call this function must synchronize calls into the system-supplied oplock package. See [Oplock synchronization](/windows-hardware/drivers/ifs/oplock-synchronization) for more information.

## -see-also

[**FLT_CALLBACK_DATA**](ns-fltkernel-_flt_callback_data.md)

[FLT_PARAMETERS for IRP_MJ_CREATE](/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-create)

[FLT_PARAMETERS for IRP_MJ_FILE_SYSTEM_CONTROL](/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-file-system-control)

[FSCTL_OPBATCH_ACK_CLOSE_PENDING](/windows-hardware/drivers/ifs/fsctl-opbatch-ack-close-pending)

[FSCTL_OPLOCK_BREAK_ACKNOWLEDGE](/windows-hardware/drivers/ifs/fsctl-oplock-break-acknowledge)

[FSCTL_OPLOCK_BREAK_ACK_NO_2](/windows-hardware/drivers/ifs/fsctl-oplock-break-ack-no-2)

[FSCTL_OPLOCK_BREAK_NOTIFY](/windows-hardware/drivers/ifs/fsctl-oplock-break-notify)

[FSCTL_REQUEST_BATCH_OPLOCK](/windows-hardware/drivers/ifs/fsctl-request-batch-oplock)

[FSCTL_REQUEST_FILTER_OPLOCK](/windows-hardware/drivers/ifs/fsctl-request-filter-oplock)

[FSCTL_REQUEST_OPLOCK](/windows-hardware/drivers/ifs/fsctl-request-oplock)

[FSCTL_REQUEST_OPLOCK_LEVEL_1](/windows-hardware/drivers/ifs/fsctl-request-oplock-level-1)

[FSCTL_REQUEST_OPLOCK_LEVEL_2](/windows-hardware/drivers/ifs/fsctl-request-oplock-level-2)

[**FltCheckOplockEx**](nf-fltkernel-fltcheckoplockex.md)

[**FltInitializeOplock**](nf-fltkernel-fltinitializeoplock.md)

[**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)

[IRP_MJ_CREATE](/windows-hardware/drivers/ifs/irp-mj-create)

[IRP_MJ_FILE_SYSTEM_CONTROL](/windows-hardware/drivers/kernel/irp-mj-file-system-control)
