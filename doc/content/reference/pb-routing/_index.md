---
title: "Packet Broker Routing"
---

This reference contains default Packet Broker routing tables.

<!--more-->

The following table explains which Forwarder Networks and Home Networks are configured by default in {{% tts %}}. To configure custom routing policies for your deployment, see the [Configure Packet Broker]({{< ref "getting-started/packet-broker/configure/routing-policies" >}}) section.

|Forwarder Network | Home Network | Status|
|--- | --- | ---|
|TTN V2 | TTS Cloud | Enabled|
|TTN V2 | TTS Community Edition | Enabled|
|TTS Community Edition | TTS Cloud | Enabled|
|TTS Community Edition | TTN V2 | Not Enabled|
|TTS Cloud | TTS Community Edition | Not Enabled|
|TTS Cloud <TENANT X> | TTS Cloud <TENANT Y> | Not Enabled|