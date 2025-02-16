---
nav_title: iOS 15 Upgrade Guide
page_order: 7
platform: iOS
description: "This reference article covers the new iOS 15 OS updates, required SDK updates, and new features."

---

# iOS 15 SDK Upgrade Guide

This guide outlines changes introduced in iOS 15 (WWDC21) and the required upgrade steps for your Braze iOS SDK integration.

> For a complete list of new iOS 15 updates, see Apple's [iOS 15 Page](https://developer.apple.com/documentation/ios-ipados-release-notes/ios-ipados-15-beta-release-notes).

{% alert important %}
This is a working document and will evolve as Apple releases new beta versions and information on their upcoming changes.
{% endalert %}

## iOS 15 Changes

## Transparency Changes to UI Navigations

As part of our annual testing of iOS betas, we have identified a change made by Apple which causes certain UI navigation bars to appear transparent instead of opaque. This will be visible on iOS 15 when using Braze's default UI for Content Cards, News Feed, or when web deep links are opened inside your app instead of in a separate browser app.

To avoid this visual change in iOS 15, we strongly recommend you upgrade to the [Braze iOS SDK v4.3.2][1] as soon as possible, before users begin to upgrade their phone to the new iOS 15 operating system.

## New Notification Settings {#notification-settings}

iOS 15 introduced new notification features to help users stay focused and avoid frequent interruptions throughout the day. We're excited to offer support for these new features - stay tuned for more information to be announced near iOS 15's official release!

### Focus Modes {#focus-mode}

iOS 15 users can now create "Focus Modes" - custom profiles used to determine which notifications they want to __break through__ their focus and display prominently.

![Notification Settings]({% image_buster /assets/img/ios/ios15-notification-settings.png %}){: style="float:right;max-width:25%;margin-left:15px;border:0"}

### Interruption Levels {#interruption-levels}

In iOS 15, push notifications can be sent with one of four interruption levels:

* **Passive** (new) - No sound, no vibration, no screen waking, no break through of focus settings.
* **Active** (default) - Allows sound, vibration, screen waking, no break through of focus settings.
* **Time-Sensitive** (new) - Allows sound, vibration, screen waking, can break through system controls if allowed.
* **Critical** - Allows sound, vibration, screen waking, can break through system controls, and bypass ringer switch.

### Notification Summary {#notification-summary}

![Notification Summary]({% image_buster /assets/img/ios/ios15-notification-summary.png %}){: style="float:right;max-width:25%;margin-left:15px;border:0"}

In iOS 15, users can (optionally) choose certain times throughout the day to receive a summary of notifications. Notifications that don't require immediate attention (i.e., sent as "Passive" or while the user is in Focus Mode) will be grouped to prevent constant interruptions throughout the day.

For each notification you send, you'll soon be able to specify a "relevance score" to control which notification should appear at the top of the summary.

We're excited to offer support for these new features - stay tuned for more information to be announced near iOS 15's official release!

## Location Buttons {#location-buttons}

iOS 15 introduces a new, convenient way for users to temporarily grant location access within an app. 

The new location button builds off of the existing "Allow Once" permission without repeatedly prompting users who click multiple times in the same session.

For more information, watch Apple's [Meet The Location Button](https://developer.apple.com/videos/play/wwdc2021/10102/) video from this year's WWDC conference.

{% alert tip %}
This feature gives you an extra chance to prompt users for permission! Users who have previously declined location permissions before iOS 15 will be shown a prompt when clicking the location button as an opportunity to reset the permission from the declined state one last time.
{% endalert %}

### Using Location Buttons with Braze

No additional integration is required when using location buttons with Braze. Your app should continue passing a user's location - once they've granted permission - as usual.

According to Apple, users who have already shared background location access, the "While Using App" option will continue to grant that level of permission after they upgrade to iOS 15.

## Apple Mail {#mail}

This year, Apple has announced many updates to email tracking and privacy. For more information, check out our [recent blog post](https://www.braze.com/resources/articles/9-ways-email-marketers-can-respond-to-apples-mail-privacy-protection-feature).

## Safari IP Address Location

In iOS 15, users will be able to configure Safari to anonymize or generalize the location that can be determined from their IP Addresses. Please keep this in mind when using location-based targeting or segmentation.

[1]: https://github.com/Appboy/appboy-ios-sdk/releases/tag/4.3.2
[2]: https://github.com/Appboy/appboy-ios-sdk/issues
