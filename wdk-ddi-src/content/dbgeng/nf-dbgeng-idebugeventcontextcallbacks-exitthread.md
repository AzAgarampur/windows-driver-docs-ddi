---
UID: NF:dbgeng.IDebugEventContextCallbacks.ExitThread
tech.root: 
title: IDebugEventContextCallbacks::ExitThread
ms.date: 02/10/2021
ms.topic: language-reference
targetos: Windows
description: 
req.assembly: 
req.construct-type: function
req.ddi-compliance: 
req.dll: 
req.header: dbgeng.h
req.idl: 
req.include-header: 
req.irql: 
req.kmdf-ver: 
req.lib: 
req.max-support: 
req.namespace: 
req.redist: 
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.target-type: 
req.type-library: 
req.umdf-ver: 
req.unicode-ansi: 
topic_type:
 - apiref
api_type:
 - COM
api_location:
 - dbgeng.h
api_name:
 - IDebugEventContextCallbacks::ExitThread
f1_keywords:
 - IDebugEventContextCallbacks::ExitThread
 - dbgeng/IDebugEventContextCallbacks::ExitThread
dev_langs:
 - c++
---

## -description


## -parameters

### -param ExitCode

### -param Context [in]

Specifies the [DEBUG_EVENT_CONTEXT structure](ns-dbgeng-_debug_event_context.md) as the “context” parameter of each event callback. The context structure contains additional information about the debug event that occurred.

Refer to [IDebugEventCallbacks::ExitThread](nf-dbgeng-idebugeventcallbacks-exitthread.md) for parameter description and additional information.

### -param ContextSize [in]

Specifies the size of the buffer Context.

## -returns

## -remarks

## -see-also

[IDebugEventContextCallbacks (dbgeng.h)](nn-dbgeng-idebugeventcontextcallbacks.md)