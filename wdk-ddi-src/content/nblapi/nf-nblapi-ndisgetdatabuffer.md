---
UID: NF:nblapi.NdisGetDataBuffer
title: NdisGetDataBuffer
ms.date: 11/30/2020
targetos: Windows
description: Call the NdisGetDataBuffer function to gain access to a contiguous block of data from a NET_BUFFER structure.
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
 - NdisGetDataBuffer
f1_keywords:
 - NdisGetDataBuffer
 - nblapi/NdisGetDataBuffer
dev_langs:
 - c++
---

# NdisGetDataBuffer function


## -description

Call the 
  <b>NdisGetDataBuffer</b> function to gain access to a contiguous block of data from a 
  <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a> structure.

## -parameters

### -param NetBuffer [in]


A pointer to a NET_BUFFER structure.

### -param BytesNeeded [in]


The number of contiguous bytes of data requested.

### -param Storage [in, optional]


A pointer to a buffer, or <b>NULL</b> if no buffer is provided by the caller. The buffer must be greater
     than or equal in size to the number of bytes specified in 
     <i>BytesNeeded</i> . If this value is non-<b>NULL</b>, and the data requested is not contiguous, NDIS copies the
     requested data to the area indicated by 
     <i>Storage</i> .

### -param AlignMultiple [in]


The alignment multiple expressed in power of two. For example, 2, 4, 8, 16, and so forth. If 
     <i>AlignMultiple</i> is 1, then there is no alignment requirement.

### -param AlignOffset [in]


The offset, in bytes, from the alignment multiple.

## -returns

<b>NdisGetDataBuffer</b> returns a pointer to the start of the contiguous data or it returns <b>NULL</b>.

If the 
      <b>DataLength</b> member of the 
      <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_data">NET_BUFFER_DATA</a> structure in the 
      <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a> structure that the <i>NetBuffer</i>
      parameter points to is less than the value in the 
      <i>BytesNeeded</i> parameter, the return value is <b>NULL</b>.

If the requested data in the buffer is contiguous, the return value is a pointer to a location that
      NDIS provides. If the data is not contiguous, NDIS uses the 
      <i>Storage</i> parameter as follows:

<ul>
<li>If the 
       <i>Storage</i> parameter is non-<b>NULL</b>, NDIS copies the data to the buffer at 
       <i>Storage</i>. The return value is the pointer passed to the 
       <i>Storage</i> parameter.</li>
<li>If the 
       <i>Storage</i> parameter is <b>NULL</b>, the return value is <b>NULL</b>.</li>
</ul>
The return value can also be <b>NULL</b> due to a low resource condition where a data buffer cannot be mapped. This may occur even if the data is contiguous or the <i>Storage</i> parameter is non-<b>NULL</b>.

## -remarks

Call this function to get a pointer to a network data header contained in the 
    <a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a> structure. You can easily parse the
    header stored in the contiguous data block that this function returns.

The requested alignment requirement is expressed as a power-of-two multiple plus an offset. For
    example, if 
    <i>AlignMultiple</i> is 4 and 
    <i>AlignOffset</i> is 3 then the data address should be a multiple of 4 plus 3. If necessary, NDIS will
    allocate memory to satisfy the alignment requirement.

## -see-also

<a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer">NET_BUFFER</a>



<a href="/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_data">NET_BUFFER_DATA</a>

