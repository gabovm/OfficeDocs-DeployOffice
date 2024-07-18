---
title: "Enabling Auto Release for your rooms"
ms.author: mactra
author: MachelleTranMSFT
manager: jtremper
ms.date: 06/03/2024
audience: ITPro
ms.topic: conceptual
ms.service: o365-proplus-itpro
ms.collection: Tier3
ms.localizationpriority: medium
recommendations: true
description: "Advise users they're using a room, and then free up the room for use by others if no current users are detected."
---

# Enabling Auto Release for your rooms

In the dynamic world of hybrid work, Microsoft Teams and Microsoft Places are innovating together to enhance room usage with the new Auto Release functionality. Once enabled, there are multiple ways for users to show that they're using a room and prevent it from automatically releasing. If a room enabled for Auto Release isn't  being used, Teams and Places free up the room for others to reserve, promoting efficient use of resources.

## Overview of Auto Release

Auto Release is a feature that's useful for conference rooms that are frequently booked and unused, especially in locations with limited room availability. With Auto Release, you can optimize the availability of conference rooms by having meeting attendees check in through one of two ways:

1. An attendee can [check in through a Teams panel](/microsoftteams/devices/check-in-and-room-release). To learn more about Teams panels, see [Overview of Microsoft Teams panels](/microsoftteams/devices/overview-teams-panels).

   :::image type="content" source="./media/enable-auto-release/person-using-teams-panel-device.png" alt-text="Screenshot that shows an image of a person using a Teams panel device.":::

   :::image type="content" source="./media/enable-auto-release/qr-code-reserved.png" alt-text="Screenshot that shows Teams Panels home screen. Information about the current meeting appears on the screen with a Check-in button.":::

1. An attendee can check in by joining a meeting through [Microsoft Teams Rooms](/microsoftteams/rooms/).

   :::image type="content" source="./media/enable-auto-release/join-meeting-through-teams-rooms.png" alt-text="Screenshot that shows Microsoft Teams Rooms. Example information about the meeting appears on the screen with a Join button.":::

1. The organizer or an attendee can check in through Teams Chat.

   :::image type="content" source="./media/enable-auto-release/meeting-chat-meeting-start-time.png" alt-text="Screenshot that shows check-in using Teams Chat.":::

   Teams Chat shows the organizer or an attendee they have checked into the room.

   :::image type="content" source="./media/enable-auto-release/meeting-chat-user-has-checked-in.png" alt-text="Screenshot that shows Teams Chat user is checked in.":::

   The organizer or an attendee can also make the room available for others through Teams Chat.

   :::image type="content" source="./media/enable-auto-release/meeting-chat-room-is-released.png" alt-text="Screenshot that shows Teams Chat user released the meeting room for others to book.":::

1. The organizer or an attendee can check in through email, which the room sends to the organizer or those who have accepted the meeting.

   > [!NOTE]
   > An email is only sent when the meeting isn't a Teams online meeting.

   :::image type="content" source="./media/enable-auto-release/auto-release-email.png" alt-text="Screenshot that shows check-in email sent when a meeting isn't a Teams online meeting.":::

> [!NOTE]
> When a Microsoft Places Public Preview user checks in via Teams Chat or email, the check-in webpage is hosted in Outlook for the web. Therefore, ensure that Outlook for the web is enabled for your organization to use this method of checking in to a room once it's available. Auto Release doesn't support on-premises mailboxes.

## Who is eligible to use Auto Release?

### Teams panels customers

- This feature is available for rooms with Teams Rooms Standard, Teams Rooms Premium, Teams Rooms Pro, or Teams Shared Device licenses.
- We recommend enabling this feature only for rooms with [Teams panels](/microsoftteams/devices/check-in-and-room-release) (can be standalone Teams panels or panels signed into the same resource account as Microsoft Teams Rooms). This recommendation is to ensure that users will always have the means to check in to the room, regardless of whether it's reserved for an online or offline meeting.
- To use this experience, Teams panels must be on application version 1449/1.0.97.2024061108 or later.

### Microsoft Places Public Preview customers

- Even if your room doesn't have a Teams Rooms Standard, Teams Rooms Premium, Teams Rooms Pro, or Teams Shared Device license, you have access to use Auto Release if you're part of the Microsoft Places preview. For more information, see [Opt in to the Microsoft Places Public Preview](opt-in-places-preview.md).
- If you receive access through the Microsoft Places preview program, this feature is available for all rooms, but we recommend enabling the feature only for rooms with a Teams panel. This ensures that users have all of the check-in options available to them, whether they reserved the room for an online or offline meeting.

> [!NOTE]
> Auto Release does not support or automatically release the room for non-Teams online meetings such as Zoom or Webex.

## How to enable specific rooms for Auto Release

Auto Release can be enabled in three different ways:

- Exchange PowerShell
- Microsoft Teams admin center
- Teams panel device

> [!NOTE]
> When Auto Release is enabled, disabled, or adjusted for a room, it can take up to 48 hours for this change to take effect. For this reason, we recommend that you adjust the settings when no meetings are scheduled for the next 48 hours.

### Exchange PowerShell

Enable this feature for rooms using the [`Set-CalendarProcessing`](/powershell/module/exchange/set-calendarprocessing?view=exchange-ps&preserve-view=true) Exchange PowerShell cmdlet.

The following example sets the Auto Release time to 10 minutes for the conference room named **Conference Room 1132**. If no usage is detected within 10 minutes of the meeting start time, the room is automatically released.

```powershell
Set-CalendarProcessing -Identity "Conference Room 1132" -EnableAutoRelease $true -PostReservationMaxClaimTimeInMinutes 10
```

### Microsoft Teams admin center

Enable this feature for rooms through [Teams admin center](https://admin.teams.microsoft.com/) under **Teams devices** > **Panels** > **Configuration profiles** > Add or Edit > Meeting settings > turn on **Release room if no one checks in** and set **Release after** > assign the configuration profile to a Teams panel.

For more information, see [Manage devices in Microsoft Teams](/microsoftteams/devices/device-management).

### Teams panel device

Enable this feature rooms on Teams panels under **Settings** > **Device settings** > **Teams Admin Settings** > **Meetings** > turn on **Release room if no one checks in** and set **Release after**.

For more information, see [Check-in and auto release on Teams panels](/microsoftteams/devices/check-in-and-room-release).

## Frequently asked questions

**Is this feature supported in any of the special cloud environments?**  
Auto Release is currently supported in Government Community Cloud (GCC).

**Does this feature support on-premises mailboxes?**  
No, this feature is only available for room mailboxes created in Exchange Online and doesn't support on-premises mailboxes. To learn more about how to manage your mailboxes, see [Manage resource mailboxes in Exchange Online](/exchange/recipients-in-exchange-online/manage-resource-mailboxes).

**Why does the tenant need to have Outlook for the web enabled?**  
When a Microsoft Places Public Preview user checks in via Teams Chat or email, the check-in webpage is hosted in Outlook for the web. Therefore, ensure that Outlook for the web is enabled for your organization to use this method of checking in to a room. Checking in via chat and email isn't yet available, but it's coming soon.

**I'm familiar with [check-in and room release on Teams panels](/microsoftteams/devices/check-in-and-room-release). How do these features work together?**  
Microsoft Teams and Microsoft Places work together to light up multiple ways for the user to reflect that they're using the room and prevent it from automatically releasing. For existing Teams Panel customers, there's no effect on the user experience. As previously noted, though, for Teams panels on 1449/1.0.97.2024061108 or later, settings adjustments can take up to 48 hours to take effect. Additionally, with Places, you're able to see data on unclaimed meeting rooms that were automatically released, such as the number of hours saved. You eventually are able to see the number of meeting room hours that were reclaimed and used productively in the Places analytics portal.  

**What triggers Auto Release?**  
When a meeting room is booked for a meeting, the attendees have time to check in to the room. When no one checks into the room using any of the previous options, the room is released and becomes available for others to reserve. The organizer receives an email notification that the room has been freed up for others to book.

**When will the room be automatically released?**  
The admin sets the time attendees must check in before the room is automatically released. If no time is set, the default is 10 minutes.

**Is the meeting organizer required to check in?**  
Anyone entering the meeting room can check in to prevent the room from being automatically released. Only one attendee needs to check in through any of the previously listed options.  