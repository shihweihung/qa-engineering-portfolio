# Connected Device & IoT Testing

## Background

A significant part of my experience has been testing software that interacts with hardware — mobile apps that communicate with physical devices over Bluetooth or Wi-Fi, MQTT-based data pipelines connecting sensors to backend services, and enterprise workflows where device state and app state need to stay synchronized.

This kind of testing is different from pure application testing. The failure surface is larger, the variables are harder to control, and bugs often sit at the boundary between the device firmware, the communication protocol, and the application logic.

---

## What I've Tested

**Bluetooth and Wi-Fi device pairing and communication**

Pairing flows, connection stability, reconnection behavior after drop, and data integrity across the communication channel. These tests are inherently more flaky than pure software tests because they depend on physical RF conditions and device firmware — understanding that distinction is important for diagnosing intermittent failures.

**MQTT-based data flow**

Testing data published from devices through MQTT brokers to backend services and eventually to UI. The verification challenge here is end-to-end: a value changes on a physical device and needs to appear correctly in the application. This requires understanding the full data path and checking each hand-off, not just the UI state.

**Device-to-app interaction**

Testing the behaviors that require both device state and app state to be correct simultaneously — scenarios where either side can be the source of failure. This involves coordinating physical hardware, app builds, and sometimes backend test environments at the same time.

**System integration testing**

Testing enterprise workflows where multiple systems — mobile app, backend services, connected devices, and external integrations — need to work together correctly. The challenge is isolating failure to a specific system when the symptoms appear at the surface level.

---

## What Makes This Testing Different

**Flakiness is structural, not a test quality problem.** RF communication is inherently variable. Tests that rely on Bluetooth connections will be less deterministic than pure software tests. The right response is to design tests with retry logic where appropriate, document the expected variability, and distinguish between test infrastructure problems and actual product bugs.

**Reproduction is harder.** A bug in a Bluetooth pairing flow may depend on specific firmware version, specific device state, specific RF environment, or a specific sequence of events. Systematic reproduction requires controlling more variables than software-only testing.

**The test environment needs hardware.** You can't emulate connected device behavior in a simulator. Physical device inventory, device management, and hardware setup are part of the testing infrastructure, not just the software stack.

---

## What I've Learned

The discipline for connected device testing is the same as for any other testing — understand the system, identify the failure modes, design tests that will actually catch them. The specific techniques differ because the system includes hardware, but the thinking process doesn't.

The most useful skill I've developed is being systematic about which layer a problem is coming from: device, protocol, backend, or app. Starting the investigation from the right layer saves significant time.
