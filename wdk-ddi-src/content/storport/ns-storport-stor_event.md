---
UID: NS:storport._STOR_EVENT
title: STOR_EVENT
description: The STOR_EVENT structure describes an event object.
tech.root: storage
ms.date: 03/24/2020
ms.keywords: STOR_EVENT, STOR_EVENT, *PSTOR_EVENT, *PRSTOR_EVENT,
req.header: storport.h
req.include-header: 
req.target-type: 
req.target-min-winverclnt: Windows 10, version 2004
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.lib: 
req.dll: 
req.ddi-compliance: 
req.unicode-ansi: 
req.max-support: 
req.typenames: STOR_EVENT, *PSTOR_EVENT, *PRSTOR_EVENT
targetos: Windows
f1_keywords:
 - _STOR_EVENT
 - storport/_STOR_EVENT
 - PSTOR_EVENT
 - storport/PSTOR_EVENT
 - STOR_EVENT
 - storport/STOR_EVENT
topic_type:
 - apiref
api_type:
 - HeaderDef
api_location:
 - storport.h
api_name:
 - _STOR_EVENT
 - PSTOR_EVENT
 - STOR_EVENT
product:
 - Windows
---

# STOR_EVENT structure


## -description

The **STOR_EVENT** structure describes an event object.

## -struct-fields

### -field Header

An opaque [**STOR_DISPATCHER_HEADER**](ns-storport-stor_dispatcher_header.md) structure that describes an event object.

## -remarks

Callers of [**StorPortInitializeEvent**](nf-storport-storportinitializeevent.md) must first allocate space for a **STOR_EVENT** structure.

## -see-also

[**KeInitializeEvent**](../wdm/nf-wdm-keinitializeevent.md)
[STOR_EVENT](ns-storport-stor_event.md)

[**STOR_DISPATCHER_HEADER**](ns-storport-stor_dispatcher_header.md)

[**StorPortInitializeEvent**](nf-storport-storportinitializeevent.md)

[**StorPortSetEvent**](nf-storport-storportsetevent.md)

