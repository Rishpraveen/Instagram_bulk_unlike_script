# Instagram Bulk Unlike Script

> **⚠️ DISCLAIMER**: This script is provided for educational purposes only. Using automated tools on Instagram violates their Terms of Service and may result in account suspension, rate limiting, or permanent ban. Use at your own risk.

## 📋 Overview

An advanced browser-based JavaScript automation script that enables bulk unliking of Instagram posts with sophisticated anti-detection mechanisms. The script simulates human behavior patterns through randomized timing, varied interaction patterns, and intelligent break systems.

## ✨ Features

### 🎯 Core Functionality
- **Bulk Unlike Operations** - Automatically unlikes Instagram posts in configurable batches
- **Smart Batch Processing** - Handles 45-75 items per batch with occasional smaller batches (20-40)
- **Infinite Scroll Support** - Automatically loads more content as needed
- **Progress Tracking** - Real-time console logging with timestamps and statistics

### 🛡️ Anti-Detection Systems
- **Randomized Timing** - Variable delays between all actions (100-3500ms ranges)
- **Multiple Selection Patterns** - Normal, reverse, and random order selection
- **Human Behavior Simulation**:
  - Mouse jitter and movement
  - Natural scroll patterns with steps
  - Reading pauses (3-8 seconds)
  - Hover events before clicks (40% probability)
  - Distraction simulations

### 🔒 Safety Features
- **Session Limits**:
  - Maximum 1-hour continuous operation
  - Daily limit of 4000 unlikes
  - Automatic stop on limit reach
- **Block Detection**:
  - Monitors for Instagram rate limiting
  - Auto-pauses 5-10 minutes on detection
  - Stops after multiple block detections
- **Error Handling**:
  - Graceful failure recovery
  - Comprehensive error logging
  - Retry mechanisms with backoff

### 🎲 Randomization Features
- **Variable Batch Sizes**:
  - Standard: 45-75 items (75% of batches)
  - Small: 20-40 items (25% of batches)
- **Break System**:
  - Short breaks: 15-45 seconds (18% probability)
  - Long breaks: 1.5-4 minutes (6% probability)
  - Extended pauses after 15+ consecutive batches
- **Interaction Variance**:
  - 80-100% scroll distance randomization
  - 100-350ms checkbox click delays
  - 1500-3000ms action delays

## 🚀 Installation & Usage

### Prerequisites
- Modern web browser (Chrome, Firefox, Edge, Brave)
- Active Instagram account
- Access to browser Developer Console

### Step-by-Step Guide

1. **Navigate to Instagram**
   ```
   https://www.instagram.com/your_username/saved/
   ```
   Or navigate to any page showing posts you've liked

2. **Open Developer Console**
   - Windows/Linux: `F12` or `Ctrl + Shift + J`
   - Mac: `Cmd + Option + J`
   - Or right-click → "Inspect" → "Console" tab

3. **Bypass Self-XSS Warning**
   - Instagram displays a security warning
   - If required, type: `allow pasting` (follow on-screen instructions)
   - This is a security feature to prevent account hijacking

4. **Copy and Paste Script**
   - Copy the entire contents of `instagram-unlike.js`
   - Paste into the console
   - Press `Enter` to execute

5. **Monitor Execution**
   - Watch console logs for progress
   - Script shows batch count, items unliked, and break notifications
   - Can be stopped anytime with `Ctrl + C` or by closing the console

### Expected Output

```
═══════════════════════════════════════════════════════════════════
🚀 INSTAGRAM BULK UNLIKE SCRIPT
═══════════════════════════════════════════════════════════════════
⚠️  WARNING: This violates Instagram Terms of Service
⚠️  Use at your own risk - account may be flagged or banned
═══════════════════════════════════════════════════════════════════

⚙️  Configuration:
   • Batch size: 45-75 items
   • Small batch chance: 25%
   • Short break chance: 18%
   • Long break chance: 6%
   • Max session: 60 minutes
   • Max daily unlikes: 4000
   • Reading simulation: 20%

═══════════════════════════════════════════════════════════════════
⏰ Starting at: 6:30:45 PM
═══════════════════════════════════════════════════════════════════

[6:30:47 PM] ℹ️ Selecting 67 items...
[6:31:02 PM] 📊 Batch 1: Selected 67 items | Total: 67
[6:31:05 PM] ✅ Successfully unliked 67 items
[6:31:18 PM] ☕ Taking short break for 23.4s...
```

## ⚙️ Configuration

### Adjusting Parameters

Edit the `CONFIG` object at the top of the script to customize behavior:

```javascript
const CONFIG = {
    batch: {
        min: 45,                    // Minimum items per batch
        max: 75,                    // Maximum items per batch
        smallBatch: {
            probability: 0.25,      // 25% chance of smaller batch
            min: 20,
            max: 40
        }
    },
    safety: {
        maxSessionDuration: 3600000,    // 1 hour (milliseconds)
        maxDailyUnlikes: 4000,          // Total unlikes before stop
    },
    breaks: {
        short: {
            probability: 0.18,      // 18% chance after each batch
            min: 15000,             // 15 seconds
            max: 45000              // 45 seconds
        },
        long: {
            probability: 0.06,      // 6% chance
            min: 90000,             // 1.5 minutes
            max: 240000             // 4 minutes
        }
    }
};
```

### Recommended Settings for Different Use Cases

**Conservative (Safest)**
```javascript
maxDailyUnlikes: 2000
maxSessionDuration: 1800000  // 30 minutes
batch.max: 50
```

**Moderate (Balanced)**
```javascript
maxDailyUnlikes: 4000
maxSessionDuration: 3600000  // 1 hour
batch.max: 75
```

**Aggressive (Higher Risk)**
```javascript
maxDailyUnlikes: 6000
maxSessionDuration: 5400000  // 1.5 hours
batch.max: 100
```

## 📊 Session Summary

After completion, the script displays a detailed summary:

```
═══════════════════════════════════════════════════════════════════
📊 SESSION SUMMARY
═══════════════════════════════════════════════════════════════════
⏰ Start time: 6:30:45 PM
⏰ End time: 7:15:22 PM
⌛ Duration: 44.6 minutes
✅ Total unliked: 3847
📈 Average rate: 86.3 unlikes/minute
⚠️  Block detections: 0
❌ Errors: 0
═══════════════════════════════════════════════════════════════════
```

## 🛠️ Technical Details

### Architecture

```
┌─────────────────────────────────────────┐
│         Main Execution Loop             │
│  ┌───────────────────────────────────┐  │
│  │  1. Check Safety Limits           │  │
│  │  2. Detect Blocks                 │  │
│  │  3. Click "Select" Button         │  │
│  │  4. Select Checkboxes (Batch)     │  │
│  │  5. Click "Unlike" + Confirm      │  │
│  │  6. Wait & Take Random Breaks     │  │
│  │  7. Simulate Human Behavior       │  │
│  └───────────────────────────────────┘  │
│              ↓                          │
│    Repeat Until Limit or Completion     │
└─────────────────────────────────────────┘
```

### Key Functions

| Function | Purpose |
|----------|---------|
| `removeLikes()` | Main execution loop |
| `selectCheckboxes()` | Handles item selection with patterns |
| `unlikeSelectedItems()` | Clicks unlike and confirmation |
| `checkForBlockDetection()` | Monitors for Instagram blocks |
| `takeBreak()` | Implements randomized pause system |
| `simulateReading()` | Adds human reading pauses |
| `clickElement()` | Natural click with hover/jitter |
| `naturalScroll()` | Human-like scroll behavior |

### Behavioral Patterns

**Selection Patterns:**
- 75%: Sequential (top to bottom)
- 15%: Reverse (bottom to top)
- 10%: Random order

**Scroll Behavior:**
- 30%: Multi-step scrolling (2-4 steps)
- 70%: Single smooth scroll
- 80-100%: Random scroll distance variance

**Click Behavior:**
- 40%: Hover before click
- 60%: Direct click
- Variable delays: 250-800ms before click
- 40%: Mouse movement after click

## ⚠️ Risks & Limitations

### Instagram Detection Risks

1. **Rate Limiting** - Instagram may temporarily block actions
2. **Account Flagging** - Repeated automation may flag your account
3. **Shadowban** - Reduced visibility of your content
4. **Temporary Block** - 24-48 hour action blocks
5. **Permanent Ban** - Severe violations may result in permanent suspension

### Known Limitations

- **Single Session Only** - Script doesn't persist across page reloads
- **No Resume Capability** - Cannot resume from where it stopped
- **Browser Tab Must Stay Open** - Closing tab stops execution
- **No Multi-Account Support** - Works on one account at a time
- **Desktop Only** - Not designed for mobile browsers

### What This Script Cannot Do

❌ Unlike posts you didn't like yourself  
❌ Bypass Instagram's security completely  
❌ Guarantee zero detection  
❌ Work on private/restricted accounts  
❌ Run on Instagram mobile app  

## 🔧 Troubleshooting

### Common Issues

**"Select button not found"**
- Solution: Ensure you're on the Instagram liked posts page
- Navigate to: Profile → Menu (☰) → Saved → All Posts

**"Element not found within timeout"**
- Solution: Slow internet connection - increase timeout values
- Check if Instagram UI changed (script may need updates)

**Script stops immediately**
- Solution: Check if you've hit daily limits
- Review console for error messages
- Verify you're on instagram.com domain

**Instagram shows "Try again later"**
- Solution: You've been rate limited - wait 6-24 hours
- Reduce batch sizes and increase delays
- Take longer breaks between sessions

**Console won't allow pasting**
- Solution: Type `allow pasting` when prompted
- This is a browser security feature

### Debug Mode

Enable verbose logging by adding to the top of script:

```javascript
const DEBUG = true;

// Then add throughout script:
if (DEBUG) console.log('Debug: checkpoint name', variable);
```

## 🤝 Contributing

Contributions are welcome! Areas for improvement:

- [ ] Better block detection algorithms
- [ ] Resume capability after interruption
- [ ] Multi-account queue support
- [ ] GUI configuration panel
- [ ] Export/import configuration presets
- [ ] Advanced statistics and analytics
- [ ] Browser extension version
- [ ] Notification system for completion

### Development Guidelines

1. Maintain anti-detection features
2. Add comments for complex logic
3. Test thoroughly before submitting
4. Update README with new features
5. Follow existing code style

## 📜 License

This project is provided **AS-IS** for educational purposes only.

**NO WARRANTY** - The authors are not responsible for:
- Account suspensions or bans
- Data loss or corruption
- Any consequences of using this tool
- Instagram Terms of Service violations

By using this script, you acknowledge that you:
- Understand the risks involved
- Take full responsibility for your actions
- Will not hold the authors liable for any outcomes

## 🔗 Related Resources

- [Instagram Terms of Service](https://help.instagram.com/581066165581870)
- [Instagram Community Guidelines](https://help.instagram.com/477434105621119)
- [Self-XSS Warning Explanation](https://www.facebook.com/selfxss)
- [Instagram API Documentation](https://developers.facebook.com/docs/instagram-platform/)

## 📧 Support

**Issues & Questions:**
- Open an issue on GitHub
- Check existing issues first
- Provide console error logs
- Describe expected vs actual behavior

**Security Concerns:**
- Report via GitHub Security Advisories
- Do not post security vulnerabilities publicly

---

**Remember:** This tool violates Instagram's Terms of Service. Use responsibly and at your own risk. The safest option is always to manually manage your liked posts through Instagram's official interface.

**Last Updated:** November 2025  
**Version:** 2.0 (Enhanced Anti-Detection)
