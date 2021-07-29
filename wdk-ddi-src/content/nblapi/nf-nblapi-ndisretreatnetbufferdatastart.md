---
UID: NF:nblapi.NdisRetreatNetBufferDataStart
title: NdisRetreatNetBufferDataStart
ms.date: 11/30/2020
targetos: Windows
description: Call the NdisRetreatNetBufferDataStart function to access more used data space in the MDL chain of a NET_BUFFER structure.
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
 - NdisRetreatNetBufferDataStart
f1_keywords:
 - NdisRetreatNetBufferDataStart
 - nblapi/NdisRetreatNetBufferDataStart
dev_langs:
 - c++
---

# NdisRetreatNetBufferDataStart function


## -description

Call the 
  <b>NdisRetreatNetBufferDataStart</b> function to access more 
  <i>used data space</i> in the MDL chain of a 
  <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a> structure.

## -parameters

### -param NetBuffer 

[in]
A pointer to a previously allocated NET_BUFFER structure.

### -param DataOffsetDelta 

[in]
The amount of 
     <i>used data space</i> to add. NDIS adjusts the 
     <b>DataOffset</b> member of the NET_BUFFER structure accordingly. If there is not enough 
     <i>unused data space</i> to satisfy the request, NDIS allocates additional memory.

### -param DataBackFill 

[in]
If NDIS must allocate memory, this parameter specifies the amount of data space, in addition to
     the value of the 
     <i>DataOffsetDelta</i> parameter, to allocate.

### -param AllocateMdlHandler 

[in, optional]
An optional entry point for an 
     <a href="/windows-hardware/drivers/ddi/nblapi/nc-nblapi-net_buffer_allocate_mdl">NetAllocateMdl</a> function. If the caller
     specifies an entry point for the 
     <i>NetAllocateMdl</i> function, NDIS calls 
     <i>NetAllocateMdl</i> to allocate an MDL and memory.

## -returns

<b>NdisRetreatNetBufferDataStart</b> returns one of the following:

<table>
<tr>
<th>Return code</th>
<th>Description</th>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>NDIS_STATUS_SUCCESS</b></dt>
</dl>
</td>
<td width="60%">
<b>NdisRetreatNetBufferDataStart</b> successfully allocated 
       <i>used data space</i> either by using the 
       <i>unused data space</i> or by allocating new storage.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>NDIS_STATUS_RESOURCES</b></dt>
</dl>
</td>
<td width="60%">
<b>NdisRetreatNetBufferDataStart</b> failed due to insufficient resources.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>NDIS_STATUS_FAILURE</b></dt>
</dl>
</td>
<td width="60%">
<b>NdisRetreatNetBufferDataStart</b> failed for reasons other than insufficient resources.

</td>
</tr>
</table>

## -remarks

<b>NdisRetreatNetBufferDataStart</b> attempts to satisfy the request by reducing the value of the 
    <b>DataOffset</b> member of the 
    <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a> structure.

If there isn't enough 
    <i>unused data space</i>, this function allocates a new buffer and an MDL to describe the new buffer and
    chains the new MDL to the beginning of the MDL chain. NDIS calls the 
    <a href="/windows-hardware/drivers/ddi/nblapi/nc-nblapi-net_buffer_allocate_mdl">NetAllocateMdl</a> function specified at 
    <i>AllocateMdl</i> to allocate the MDL and memory. The 
    <i>NetAllocateMdl</i> function can use any allocation method that meets the
    driver's design requirements.

Call the 
    <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart">
    NdisAdvanceNetBufferDataStart</a> function to release the 
    <i>used data space</i> that was added with 
    <b>NdisRetreatNetBufferDataStart</b>.

## -see-also

<a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a>



<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart">
   NdisAdvanceNetBufferDataStart</a>



<a href="/windows-hardware/drivers/ddi/nblapi/nc-nblapi-net_buffer_allocate_mdl">NetAllocateMdl</a>
