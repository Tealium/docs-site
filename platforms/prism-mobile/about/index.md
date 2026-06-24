---
title: About Tealium Prism
description: Architecture overview of the Tealium Prism SDK, including the native event pipeline, rules engine, and dispatcher model.
url: https://docs.tealium.com/platforms/prism-mobile/about/
---
## Overview

Tealium Prism is the mobile SDK for iOS (Swift) and Android (Kotlin), designed as a fully native, reactive event pipeline. Instead of configuring each vendor SDK separately, you instrument a single, unified event API in your app and let Prism deliver those events to Tealium Collect and supported third‑party SDKs. This reduces implementation effort, keeps data consistent across tools, and gives you more control over how mobile data is collected and activated.

Prism replaces the legacy webview‑driven model with a 100% native architecture and a custom event pipeline optimized for mobile throughput.

Three components manage when and where events are delivered: a native rules engine, dispatchers, and barriers. For example, Prism can throttle Collect traffic when offline while continuing to send events to local SDKs that handle their own queuing.

Configuration is managed through a Tealium mobile profile, so modules, rules, barriers, and transformations can be updated without a new app release.

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

### Remote settings

Most SDK configuration happens outside the app in a Tealium mobile profile. A mobile profile gives you a dedicated workspace to manage modules, extensions, barriers, and load rules through a UI. Changes publish as remote settings, and the SDK picks them up on the next refresh or app startup — no code changes or app release required.

This is the recommended approach for most configuration. It keeps implementation code minimal and lets your team adjust SDK behavior in response to business or operational needs.

### Advanced configuration

Two additional configuration methods are available for scenarios where remote settings are not sufficient.

**Local JSON** bundles a settings file directly in the app. Use this as a reliable fallback when the device cannot reach the remote settings endpoint, or to pre-configure behavior before the first remote fetch completes.

**Programmatic configuration** sets values directly in code using the SDK&#39;s configuration API. Use this when:

* The configuration depends on device state at runtime — for example, adjusting batch size based on available disk space.
* A setting must be locked against remote changes — for example, enforcing `LogLevel.silent` in production builds so a publishing mistake cannot enable verbose logging.
* You need to verify behavior during development without publishing a change to the platform.

Programmatic settings take the highest precedence, overriding both remote and local JSON. In all other cases, configure using the UI.

| Method | Priority | Use when |
| :---- | :---- | :---- |
| **Programmatic** | 1 (highest) | Runtime-calculated values or settings that must be locked in code. |
| **Remote settings** | 2 | Standard operational configuration — modules, barriers, transformations, rules. |
| **Local JSON** | 3 | Fallback defaults bundled with the app. |
