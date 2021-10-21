---
UID: NF:nblapi.NdisFreeReassembledNetBufferList
title: NdisFreeReassembledNetBufferList
ms.date: 11/30/2020
targetos: Windows
description: Call the NdisFreeReassembledNetBufferList function to free a reassembled NET_BUFFER_LIST structure and the associated NET_BUFFER structure and MDL chain.
tech.root: netvista
req.assembly: 
req.construct-type: function
req.ddi-compliance: Irql_NetBuffer_Function
req.dll: 
req.header: ndis/nblapi.h
req.idl: 
req.include-header: ndis.h
req.irql: <= DISPATCH_LEVEL
req.kmdf-ver: 
req.lib: Ndis.lib
req.max-support: 
req.namespace: 
req.redist: 
req.target-min-winverclnt: Supported in NDIS 6.0 and later.
req.target-min-winversvr: 
req.target-type: Universal
req.type-library: 
req.umdf-ver: 
req.unicode-ansi: 
topic_type:
 - apiref
api_type:
 - LibDef
api_location:
 - nblapi.h
api_name:
 - NdisFreeReassembledNetBufferList
f1_keywords:
 - NdisFreeReassembledNetBufferList
 - nblapi/NdisFreeReassembledNetBufferList
dev_langs:
 - c++
---

# NdisFreeReassembledNetBufferList function


## -description

Call the 
  <b>NdisFreeReassembledNetBufferList</b> function to free a reassembled 
  <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list">NET_BUFFER_LIST</a> structure and the associated 
  <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a> structure and MDL chain.

## -parameters

### -param ReassembledNetBufferList [in]


A pointer to a NET_BUFFER_LIST structure that the driver allocated by calling the 
     <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist">
     NdisAllocateReassembledNetBufferList</a> function.

### -param DataOffsetDelta [in]


The number of bytes to advance (add to) the 
     <b>DataOffset</b> member of the reassembled NET_BUFFER structure before freeing the structure. This value
     should match 
     <i>DataOffsetDelta</i> that the driver passed to 
     <b>NdisAllocateReassembledNetBufferList</b>.

### -param FreeReassembleFlags [in]


NDIS flags that can be combined with an OR operation. Set this parameter to zero. There are
     currently no flags defined for this function.

## -remarks

<b>NdisFreeReassembledNetBufferList</b> frees a reassembled 
    <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list">NET_BUFFER_LIST</a> structure that the caller
    allocated by calling 
    <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist">
    NdisAllocateReassembledNetBufferList</a>.

## -see-also

<a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a>



<a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list">NET_BUFFER_LIST</a>



<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist">
   NdisAllocateReassembledNetBufferList</a>

