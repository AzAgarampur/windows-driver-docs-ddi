---
UID: NS:dispmprt._DXGK_DEBUG_REPORT_INTERFACE
title: DXGK_DEBUG_REPORT_INTERFACE (dispmprt.h)
description: The DXGK_DEBUG_REPORT_INTERFACE structure contains pointers to functions in the Debug Report interface, which is implemented by the display port driver.
old-location: display\dxgk_debug_report_interface.htm
tech.root: display
ms.date: 11/19/2021
keywords: ["DXGK_DEBUG_REPORT_INTERFACE structure"]
ms.keywords: "*PDXGK_DEBUG_REPORT_INTERFACE, DXGK_DEBUG_REPORT_INTERFACE, DXGK_DEBUG_REPORT_INTERFACE structure [Display Devices], DmStructs_b6b70526-c889-47d8-bfb7-7f961cbcef38.xml, PDXGK_DEBUG_REPORT_INTERFACE, PDXGK_DEBUG_REPORT_INTERFACE structure pointer [Display Devices], _DXGK_DEBUG_REPORT_INTERFACE, display.dxgk_debug_report_interface, dispmprt/DXGK_DEBUG_REPORT_INTERFACE, dispmprt/PDXGK_DEBUG_REPORT_INTERFACE"
req.header: dispmprt.h
req.include-header: Dispmprt.h
req.target-type: Windows
req.target-min-winverclnt: Windows Vista
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
req.typenames: DXGK_DEBUG_REPORT_INTERFACE, *PDXGK_DEBUG_REPORT_INTERFACE
f1_keywords:
 - _DXGK_DEBUG_REPORT_INTERFACE
 - dispmprt/_DXGK_DEBUG_REPORT_INTERFACE
 - PDXGK_DEBUG_REPORT_INTERFACE
 - dispmprt/PDXGK_DEBUG_REPORT_INTERFACE
 - DXGK_DEBUG_REPORT_INTERFACE
 - dispmprt/DXGK_DEBUG_REPORT_INTERFACE
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - HeaderDef
api_location:
 - dispmprt.h
api_name:
 - _DXGK_DEBUG_REPORT_INTERFACE
 - PDXGK_DEBUG_REPORT_INTERFACE
 - DXGK_DEBUG_REPORT_INTERFACE
---

# DXGK_DEBUG_REPORT_INTERFACE structure

## -description

The **DXGK_DEBUG_REPORT_INTERFACE** structure contains pointers to functions in the Debug Report interface, which is implemented by the display port driver.

## -struct-fields

### -field Size

The size, in bytes, of this structure.

### -field Version

The version number of the Debug Report interface. Version number constants are defined in *Dispmprt.h* (for example, DXGK_DEBUG_REPORT_INTERFACE_VERSION_1).

### -field Context

A pointer to a context that is provided by the display port driver.

### -field InterfaceReference

A pointer to an interface reference function that is implemented by the display port driver.

### -field InterfaceDereference

A pointer to an interface dereference function that is implemented by the display port driver.

### -field DbgReportCreate

Creates an initial error report.

If your display miniport driver detects a failure and then recovers from it, you can create an error report that can later be used for debugging. First, call **DbgReportCreate** to create an initial report. Then add data to the report by making one or more calls to **DbgReportSecondaryData**. When you have finished adding data to the report, call **DbgReportComplete**.

The syntax for **DbgReportComplete** follows.

```cpp
// IRQL: PASSIVE_LEVEL
DXGK_DEBUG_REPORT_HANDLE (*DbgReportCreate)(
  _In_ HANDLE    DeviceHandle,
  _In_ ULONG     ulCode,
  _In_ ULONG_PTR ulpArg1,
  _In_ ULONG_PTR ulpArg2,
  _In_ ULONG_PTR ulpArg3,
  _In_ ULONG_PTR ulpArg4
);
```

* *DeviceHandle* is a handle to a context block associated with a display adapter. The display miniport driver created this handle in its [**DxgkDdiAddDevice***](nc-dispmprt-dxgkddi_add_device.md) function. This parameter can be NULL.

* *ulCode* is a code for the error report. The following codes are supported:

  * THREAD_STUCK_IN_DEVICE_DRIVER
  * VIDEO_DRIVER_DEBUG_REPORT_REQUEST
  * VIDEO_TDR_FATAL_ERROR
  * VIDEO_TDR_SUCCESS

* *ulpArg1* is the first argument to be added to the report. The developer of the display miniport driver determines the value and meaning of *ulpArg1*.

* *ulpArg2* is the second argument to be added to the report. The developer of the display miniport driver determines the value and meaning of *ulpArg2*.

* *ulpArg3* is the third argument to be added to the report. The developer of the display miniport driver determines the value and meaning of *ulpArg3*.

* *ulpArg4* is reserved.

### -field DbgReportSecondaryData

Appends data to an initial error report that was previously created by **DbgReportCreate**.

Call **DbgReportSecondaryData** to add data to an initial report that was created by a previous call to **DbgReportCreate**. You can call **DbgReportSecondaryData** several times, but with each call, the data written to the report overwrites the data written by the previous call. The following steps give a good strategy for incrementally adding data to the report.

1. Obtain the data that is safest to collect.
2. Call **DbgReportSecondaryData** to write that data to the report.
3. Obtain data that is more risky to collect.
4. Call **DbgReportSecondaryData** to write the original safe data along with the newly collected risky data to the report. You must include both the safe and the risky data in this call because the data written by this call overwrites the data written by the first call to **DbgReportSecondaryData**.
5. Continue calling **DbgReportSecondaryData**, enhancing the data each time, until you have no more data to add.
6. When you have finished adding data to the report, close the report by calling **DbgReportComplete**. The report is stored in a file and sent to Microsoft when the computer is rebooted.
7. If the computer stops responding before you call **DbgReportComplete**, the data added to the report by the most recent successful call to **DbgReportSecondaryData** is saved and then sent to Microsoft when the computer is rebooted.

```cpp
BOOLEAN (*DbgReportSecondaryData)(
  _Inout_ DXGK_DEBUG_REPORT_HANDLE hReport,
  _In_    PVOID                    pvData,
  _In_    ULONG                    ulDataSize
);
```

* *hReport* is a handle to the error report to which data will be appended. The display miniport driver previously obtained this handle by calling **DbgReportCreate**.

* *pvData* is a pointer to a buffer that holds the data to be added to the report.

* *ulDataSize* is the size, in bytes, of the data to be added to the report. The value of this parameter must be less than or equal to DXGK_DEBUG_REPORT_MAX_SIZE.

### -field DbgReportComplete

Closes an error report and frees any resources associated with the report.

**DbgReportCreate** creates an entry in the system event log and displays a dialog box that informs the user of the failure and presents the opportunity to upload an error report to Microsoft.

The error report is saved in a file and scheduled to be sent to Microsoft when the computer is rebooted. The error report contains an error code and four arguments. The error code and the first three arguments are provided by the caller of DbgReportCreate. The fourth argument in the report is provided by the operating system and indicates the number of reports generated since the computer was started. For example, if the value of the fourth argument is 5, this means that four previous error reports were generated by the display miniport driver since the computer was last started. Only the fifth report is saved because each report overwrites the previous one.

```cpp
// IRQL: PASSIVE_LEVEL
VOID DbgReportComplete(
   IN OUT DXGK_DEBUG_REPORT_HANDLE hReport
);
```

* *hReport* is a handle to the error report that is to be closed. The display miniport driver previously obtained this handle by calling **DbgReportCreate**.

**IRQL:** PASSIVE_LEVEL

## -remarks

The display miniport driver supplies the **Size** and **Version** members of this structure, and then calls [**DxgkCbQueryServices***](nc-dispmprt-dxgkcb_query_services.md), which fills in the remaining members of this structure.
