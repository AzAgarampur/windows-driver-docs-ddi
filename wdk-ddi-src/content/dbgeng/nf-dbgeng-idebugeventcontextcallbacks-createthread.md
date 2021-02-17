---
UID: NF:dbgeng.IDebugEventContextCallbacks.CreateThread
tech.root: debugger
title: IDebugEventContextCallbacks::CreateThread
ms.date: 02/12/2021
ms.topic: language-reference
targetos: Windows
description: The CreateThread callback method is called by the engine when a create-threaddebugging event occurs in the target.
req.assembly: 
req.construct-type: function
req.ddi-compliance: 
req.dll: 
req.header: dbgeng.h
req.idl: 
req.include-header: dbgeng.h
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
 - IDebugEventContextCallbacks::CreateThread
f1_keywords:
 - IDebugEventContextCallbacks::CreateThread
 - dbgeng/IDebugEventContextCallbacks::CreateThread
dev_langs:
 - c++
---

## -description

The CreateThread callback method is called by the engine when a create-threaddebugging event occurs in the target.

Any of these values can be zero if they cannot be provided by the engine.
Currently the kernel does not return thread or process change events.

Refer to [IDebugEventCallbacks::CreateThread](nf-dbgeng-idebugeventcallbacks-createthread.md) for parameter description and additional information.

## -parameters

### -param Handle

### -param DataOffset

### -param StartOffset

### -param Context [in]

Specifies the [DEBUG_EVENT_CONTEXT structure](ns-dbgeng-_debug_event_context.md) as the “context” parameter of each event callback. The context structure contains additional information about the debug event that occurred.

### -param ContextSize [in]

Specifies the size of the buffer Context.

## -returns

## -remarks

## -see-also

[IDebugEventContextCallbacks (dbgeng.h)](nn-dbgeng-idebugeventcontextcallbacks.md)