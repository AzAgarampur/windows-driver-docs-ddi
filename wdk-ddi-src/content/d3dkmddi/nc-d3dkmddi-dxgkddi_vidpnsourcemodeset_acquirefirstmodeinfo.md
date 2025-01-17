---
UID: NC:d3dkmddi.DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO
title: DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO (d3dkmddi.h)
description: The pfnAcquireFirstModeInfo function returns a descriptor of the first mode in a specified VidPN source mode set.
old-location: display\dxgk_vidpnsourcemodeset_interface_pfnacquirefirstmodeinfo.htm
ms.date: 05/10/2018
keywords: ["DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO callback function"]
ms.keywords: DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO, DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO callback, VidPnFunctions_14a2da15-5fde-4701-b3e6-9e60c84f381b.xml, d3dkmddi/pfnAcquireFirstModeInfo, display.dxgk_vidpnsourcemodeset_interface_pfnacquirefirstmodeinfo, pfnAcquireFirstModeInfo, pfnAcquireFirstModeInfo callback function [Display Devices]
req.header: d3dkmddi.h
req.include-header: D3dkmddi.h
req.target-type: Desktop
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
req.irql: PASSIVE_LEVEL
targetos: Windows
tech.root: display
req.typenames: 
f1_keywords:
 - DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO
 - d3dkmddi/DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - UserDefined
api_location:
 - d3dkmddi.h
api_name:
 - DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO
product:
 - Windows
---

# DXGKDDI_VIDPNSOURCEMODESET_ACQUIREFIRSTMODEINFO callback function


## -description

The <b>pfnAcquireFirstModeInfo</b> function returns a descriptor of the first mode in a specified VidPN source mode set.

## -parameters

### -param hVidPnSourceModeSet [in]

A handle to a VidPN source mode set object. The display miniport driver previously obtained this handle by calling the <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiresourcemodeset">pfnAcquireSourceModeSet</a> function of the <a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface">DXGK_VIDPN_INTERFACE</a> interface.

### -param ppFirstVidPnSourceModeInfo [out]

A pointer to a variable that receives a pointer to a <a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode">D3DKMDT_VIDPN_SOURCE_MODE</a> structure. The structure contains a variety of information about the mode, including its ID, type, and rendering format.

## -returns

The <b>pfnAcquireFirstModeInfo</b> function returns one of the following values:

|Return code|Description|
|--- |--- |
|STATUS_SUCCESS|The function succeeded.|
|STATUS_GRAPHICS_INVALID_VIDPN_SOURCEMODESET|The handle supplied in hVidPnSourceModeSet was invalid.|

## -remarks

When you have finished using the D3DKMDT_VIDPN_SOURCE_MODE structure, you must release the structure by calling <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_releasemodeinfo">pfnReleaseModeInfo</a>.

You can enumerate all the modes that belong to a VidPN source mode set object by calling <b>pfnAcquireFirstModeInfo</b> and then making a sequence of calls to <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirenextmodeinfo">pfnAcquireNextModeInfo</a>.

The D3DKMDT_HVIDPNSOURCEMODESET data type is defined in <i>D3dkmdt.h</i>.

## -see-also

<a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode">D3DKMDT_VIDPN_SOURCE_MODE</a>



<a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirenextmodeinfo">pfnAcquireNextModeInfo</a>



<a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_releasemodeinfo">pfnReleaseModeInfo</a>

