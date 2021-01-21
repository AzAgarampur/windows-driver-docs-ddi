---
UID: NS:ntddndis._NDIS_TIMESTAMP_CAPABILITIES
title: _NDIS_TIMESTAMP_CAPABILITIES (ntddndis.h)
description: The NDIS_TIMESTAMP_CAPABILITIES structure describes describes the combined timestamping capabilities of a NIC and miniport driver.
tech.root: netvista
ms.date: 12/31/2020
keywords: ["NDIS_TIMESTAMP_CAPABILITIES structure"]
ms.keywords: _NDIS_TIMESTAMP_CAPABILITIES, NDIS_TIMESTAMP_CAPABILITIES, *PNDIS_TIMESTAMP_CAPABILITIES,
req.header: ntddndis.h
req.include-header: ndis.h
req.target-type: 
req.target-min-winverclnt: Windows 10, version 21H1. Supported in NDIS 6.82 and later.
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.lib: 
req.dll: 
req.ddi-compliance: 
req.unicode-ansi: 
req.max-support: 
req.typenames: NDIS_TIMESTAMP_CAPABILITIES, *PNDIS_TIMESTAMP_CAPABILITIES
targetos: Windows
ms.custom: RS5
f1_keywords:
 - _NDIS_TIMESTAMP_CAPABILITIES
 - ntddndis/_NDIS_TIMESTAMP_CAPABILITIES
 - PNDIS_TIMESTAMP_CAPABILITIES
 - ntddndis/PNDIS_TIMESTAMP_CAPABILITIES
 - NDIS_TIMESTAMP_CAPABILITIES
 - ntddndis/NDIS_TIMESTAMP_CAPABILITIES
topic_type:
 - apiref
api_type:
 - HeaderDef
api_location:
 - ntddndis.h
api_name:
 - _NDIS_TIMESTAMP_CAPABILITIES
 - PNDIS_TIMESTAMP_CAPABILITIES
 - NDIS_TIMESTAMP_CAPABILITIES
---

# _NDIS_TIMESTAMP_CAPABILITIES structure


## -description

The **NDIS_TIMESTAMP_CAPABILITIES** structure describes the combined timestamping capabilities of a network interface card (NIC) and miniport driver.

## -struct-fields

### -field Header

The [NDIS_OBJECT_HEADER](../objectheader/ns-objectheader-ndis_object_header.md) structure that describes this **NDIS_TIMESTAMP_CAPABILITIES** structure. Set the members of the **NDIS_OBJECT_HEADER** structure as follows:

* Set the **Type** member to **NDIS_OBJECT_TYPE_DEFAULT**.

* Set the **Revision** member to **NDIS_TIMESTAMP_CAPABILITIES_REVISION_1**.

* Set the **Size** member to **NDIS_SIZEOF_TIMESTAMP_CAPABILITIES_REVISION_1**.


### -field HardwareClockFrequencyHz

This field contains the nominal frequency of the hardware clock used by the NIC for timestamping, rounded off to the nearest integer in Hertz units.

### -field CrossTimestamp

A value of **TRUE** indicates that the miniport/hardware combination is capable of generating a hardware cross timestamp.  A value of **FALSE** indicates this capability does not exist. A cross timestamp is the set of a NIC hardware timestamp and system timestamp(s) obtained very close to each other. The miniport driver handles the [OID_TIMESTAMP_GET_CROSSTIMESTAMP](/windows-hardware/drivers/network/oid-timestamp-get-crosstimestamp) OID to generate a cross timestamp.

### -field Reserved1

Reserved for future use.

### -field Reserved2

Reserved for future use.

### -field TimestampFlags

An [**NDIS_TIMESTAMP_CAPABILITY_FLAGS**](ns-ntddndis-_ndis_timestamp_capability_flags.md) structure that represents the NIC's timestamping capabilities in various contexts.

## -remarks

Miniport drivers use the **NDIS_TIMESTAMP_CAPABILITIES** structure with the [**NDIS_STATUS_TIMESTAMP_CAPABILITY**](/windows-hardware/drivers/network/ndis-status-timestamp-capability) status indication to report the NIC's hardware timestamping capabilities and the miniport driver's software timestamping capabilities to NDIS and overlying drivers.

Miniport drivers use the **NDIS_TIMESTAMP_CAPABILITIES** structure with the [**NDIS_STATUS_TIMESTAMP_CURRENT_CONFIG**](/windows-hardware/drivers/network/ndis-status-timestamp-current-config) status indication to report the current timestamping configuration to the operating system.

For more information, see [Reporting timestamping capabilities and current configuration](reporting-timestamping-capabilities.md).

## -see-also

[**NDIS_TIMESTAMP_CAPABILITY_FLAGS**](ns-ntddndis-_ndis_timestamp_capability_flags.md)

[**NDIS_STATUS_TIMESTAMP_CAPABILITY**](/windows-hardware/drivers/network/ndis-status-timestamp-capability)

[**NDIS_STATUS_TIMESTAMP_CURRENT_CONFIG**](/windows-hardware/drivers/network/ndis-status-timestamp-current-config)

[OID_TIMESTAMP_GET_CROSSTIMESTAMP](/windows-hardware/drivers/network/oid-timestamp-get-crosstimestamp)

[**MiniportInitializeEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[NDIS_OBJECT_HEADER](../objectheader/ns-objectheader-ndis_object_header.md)

[Reporting timestamping capabilities and current configuration](reporting-timestamping-capabilities.md)