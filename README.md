# github-contribution-log

# Contribution [#]: [Issue Title]

**Contribution Number:** 1  
**Student:** Ashley Jackson  
**Issue:** [[GitHub issue link] ](https://github.com/meshtastic/firmware/issues/10517) 
**Status:** Phase I

---

## Why I Chose This Issue

I am almost finished with the MVP for an app I am creating. My stretch goal includes incorporating meshtastic into the application. This issue gives me a good entry level issue into the code so I can become familiar with it over time.

---

## Understanding the Issue

### Problem Description

Firmware update has caused issues with the LED light on the ThinkNode M1

### Expected Behavior

The light is not supposed to remain on past the intial start up

### Current Behavior

The light remains on persistently after users upgrade firmware to the newest version

### Affected Components
EInkDisplay2.cpp has comments about the hardware backlight and it automatically starting enabled


---

## Reproduction Process

### Environment Setup

[Notes on setting up your local development environment - challenges you faced, how you solved them]
This is brand new for me, I am working on firmware and having to reproduce the issue physically and not in the code. The README provided gave really good guidance. I had to install an additional IDE inside of VSCode. It is called Platform IDE. I did some quick research and apparently PlayformIO IDE is used for meshtastic because it is extremely complex and has over 1000 different development boards. Using PlatformIO supports a large amount of platforms used in the Meshtastic ecosystem and the 1000+ development boards. 
I had to do setup within VSCode that still seems a bit foreign to me. The README directed me to: https://meshtastic.org/docs/development/firmware/build/
I had to build the firmware locally and then select the project (Hardware) I was working with. 


### Steps to Reproduce

1. This is a physical issue with the firmware that is found on an electric device. The light remains on, when previously the led status light could be turned off


### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** The issue can be reproduced after I updated my device to the newest firmware. Previously, I could turn the LED light off with the knob on the device.
- <img width="1920" height="1080" alt="Screenshot 2026-06-16 at 9 42 42 PM" src="https://github.com/user-attachments/assets/476eef18-f8ac-4483-865c-5e613bdf7207" />

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]
nicheGraphics.h is where a lot of the visual aspects of the devide are defined. Such as font size and font family, applets, what happens with the backlight when clicking specific buttons. This directly connects to LatchingBacklight.h which includes Observer.h and covers backlight. 

#elif defined(ELECROW_ThinkNode_M1)
#define HW_VENDOR meshtastic_HardwareModel_THINKNODE_M1

StatusLEDModule.cpp is directly for the status light that is mentioned in the issue. It covers the LED power for the status lights on the device. This is where the issue would be solved, the backlight modules would be additional to the issue but proves beneficial. 
board pin = variant.h
boot LED init = main.cpp
runtime and charge status is StatusLEDModule.cpp


### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

**Understand:** [Restate the problem]
The newest firmware for Meshtastic forced the status led on the ThinkNode M1 to stay on after booting up. 

**Match:** [What similar patterns/solutions exist in the codebase?]
Syncing changes to the blacklight to change with the LED light would be a stretch goal but prove beneficial. 

**Plan:** [Step-by-step implementation plan]
1. main.cpp forces the led on on bootup for the specific device. Current set up is a heartbeat status. 
   In main.cpp, LED_POWER is being forced on early boot. Removing this or adding a setting that allows user to set a preference on boot.
2. LED_Notification in StatusLEDModule.cpp, allow surpression of charge and pairing status lights.


**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
