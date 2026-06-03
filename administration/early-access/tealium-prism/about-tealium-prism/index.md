---
title: About Tealium Prism
description: Tealium Prism is a native mobile SDK for iOS (Swift) and Android (Kotlin) built on a unified, reactive event pipeline.
url: https://docs.tealium.com/administration/early-access/tealium-prism/about-tealium-prism/
---
## Overview

Tealium Prism is the mobile SDK for iOS (Swift) and Android (Kotlin), designed as a fully native, reactive event pipeline. Instead of configuring each vendor SDK separately, you instrument a single, unified event API in your app and let Prism deliver those events to Tealium Collect and supported third‑party SDKs. This reduces implementation effort, keeps data consistent across tools, and gives you more control over how mobile data is collected and activated.

Prism replaces the legacy webview‑driven model with a 100% native architecture and a custom event pipeline optimized for mobile throughput.

Three components manage when and where events are delivered: a native rules engine, dispatchers, and barriers. For example, Prism can throttle Collect traffic when offline while continuing to send events to local SDKs that handle their own queuing.

Configuration is driven by JSON (for example, from Tealium iQ), so many aspects of behavior can be tuned per environment without a new app release.

At a glance, Tealium Prism provides:  

* **Unified event API**: A single, consistent event API for Swift and Kotlin with near‑identical concepts and naming.  
* **Multi‑dispatcher pipeline**: Send the same event to Tealium Collect and on‑device vendor SDKs in parallel.  
* **Rules engine and barriers**: Control event delivery based on connectivity, batching, consent, or other conditions.  
* **On‑device transformations**: Modify, enrich, or filter event payloads before they leave the device, with the ability to update logic without an App Store / Play Store release.  
* **Configuration model**: A configuration model designed for consent‑aware behavior and environment‑specific settings.

## How it works

Tealium Prism is built for performance and maintainability, moving away from web-dependent logic to a fully native, unified approach.

### Native runtime

Prism eliminates legacy dependencies on `WKWebView`. All logic runs in a 100% native environment, powered by a custom rules engine and JSON configurations. This delivers a smaller memory footprint and improved battery efficiency, leveraging specialized reactive frameworks for high-throughput event processing.

### Swift and Kotlin parity

Both the Swift and Kotlin SDKs share nearly identical logic and naming conventions. This code parity enables mobile teams to manage iOS and Android implementations with a single mental model, reducing onboarding time and minimizing platform-specific discrepancies.

### Event control

Barriers are rules that control when and how events are delivered to each destination, giving you precise control over event flow.

Previously, legacy SDKs used a single event queue, and if one destination was offline, all event delivery paused. With Prism, each dispatcher operates independently, and barriers can be set per destination, allowing parallel processing and minimizing bottlenecks.

For example, Tealium Collect uses connectivity and batching barriers to optimize bandwidth and ensure reliable delivery. Third-party SDKs receive events in real time, even when offline, so they can manage their own queues.

### Native transformations

Use native transformations, with custom logic or built-in Tealium iQ extensions, to modify event payloads in Swift or Kotlin before they leave the device. Native transformations are ideal for correcting data issues or updating logic without an app update.

### Configuration governance

Prism offers a three-tier configuration system to help prevent misconfiguration and maintain app integrity. Settings are merged in a specific priority order that ensures critical or security-sensitive settings cannot be accidentally overridden by lower-priority sources.

| Tier | Priority | Can override? | Purpose |
| :---- | :---- | :---- | :---- |
| **Programmatic** | 1 (Highest) | No | Security-critical IDs and environment locks. |
| **Remote JSON** | 2 | Yes | Real-time updates for operational settings such as batch sizes or sampling. |
| **Local JSON** | 3 | Yes | Default fallback settings bundled with the app. |
