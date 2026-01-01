# Bonzi Buddy C# – Microsoft Agent Command Reference

This README documents the **actual Microsoft Agent commands** used to control a Bonzi Buddy–style character in **C#** using **`AgentCtl.dll`**, **`AgentSvr.tlb`**, and **`DaServer.tlb`**.

This is a **technical reference** you can use while building or modding a Bonzi-style desktop assistant.

---

## ⚠️ Important Compatibility Notes

Microsoft Agent is **legacy technology**.

Requirements:

* Windows only
* **.NET Framework 4.8** (not .NET Core / .NET 6+)
* **x86 (32-bit)** build target
* Valid `.acs` character file (Bonzi, Merlin, Genie, etc.)

---

## Libraries Used

Add these references to your project:

* `AgentCtl.dll`
* `AgentSvr.tlb`
* `DaServer.tlb`

## Add bonzi animations to your project:
First copy the **bonzi.acs** file to your conation of choice (eg. C:/)
```csharp
using AgentObjects;

Agent agent = new Agent();
agent.Connected = true;

// Load the Bonzi character
agent.Characters.Load("Bonzi", "C:/bonzi.acs"); // Change the location here

IAgentCtlCharacterEx bonzi =
    agent.Characters["Bonzi"] as IAgentCtlCharacterEx;

// Test
bonzi.Show(false);
bonzi.Speak("Bonzi loaded successfully!");
```

Namespace commonly used:

```csharp
using AgentObjects;
```

---

## Core Objects

```csharp
Agent agent;
IAgentCtlCharacterEx bonzi;
```

The `IAgentCtlCharacterEx` interface is where **all Bonzi commands live**.

---

## 🗣️ Speech Commands

### Speak Text

```csharp
bonzi.Speak("Hello world!");
```

### Stop Speaking or Animations

```csharp
bonzi.Stop();
```

### Think (Text Bubble Only)

```csharp
bonzi.Think("Hmm...");
```

---

## 🎭 Animation Commands

### Play an Animation

```csharp
bonzi.Play("Wave");
bonzi.Play("Think");
bonzi.Play("Congratulate");
```

### Check If Animation Exists

```csharp
bool hasWave = bonzi.HasAnimation("Wave");
```

### Common Animation Names

```
Greet
Wave
Explain
Think
Congratulate
Read
Write
Idle1
Idle2
Idle3
Surprised
Sad
Happy
Laugh
Confused
```

---

## 👀 Visibility Commands

### Show Character

```csharp
bonzi.Show(false); // false = no intro animation
```

### Hide Character

```csharp
bonzi.Hide();
```

---

## 🚶 Movement Commands

### Move Instantly

```csharp
bonzi.MoveTo(300, 400, 0);
```

### Move With Animation

```csharp
bonzi.MoveTo(300, 400, 1000); // milliseconds
```

### Read Position

```csharp
int x = bonzi.Left;
int y = bonzi.Top;
```

---

## 🖱️ User Interaction Settings

### Enable Dragging

```csharp
bonzi.Dragging = true;
```

### Enable Speech Balloon

```csharp
bonzi.SpeechEnabled = true;
```

### Enable Sound Effects

```csharp
bonzi.SoundEffectsEnabled = true;
```

---

## 💬 Speech Balloon Customization

```csharp
bonzi.Balloon.FontName = "Comic Sans MS";
bonzi.Balloon.FontSize = 12;
bonzi.Balloon.ForeColor = 0x000000;
bonzi.Balloon.BackColor = 0xFFFFFF;
```

---

## 🎯 Gesture Commands

### Point or Gesture at Screen Location

```csharp
bonzi.GestureAt(x, y);
```

---

## 🔊 Audio Control

### Mute Character

```csharp
bonzi.SoundEffectsEnabled = false;
```

### Unmute Character

```csharp
bonzi.SoundEffectsEnabled = true;
```

---

## 📋 Character Information

```csharp
string name = bonzi.Name;
string description = bonzi.Description;
```

---

## 📐 Size Control

```csharp
bonzi.Width = 200;
bonzi.Height = 200;
```

---

## ❌ Shutdown & Cleanup

Always disconnect cleanly:

```csharp
bonzi.Hide();
agent.Connected = false;
```

---

## 🧪 Minimal Working Example

```csharp
bonzi.Show(false);
bonzi.MoveTo(200, 300, 1000);
bonzi.Play("Wave");
bonzi.Speak("Hello! I am Bonzi!");
```

---

## 🛑 Common Problems

**Bonzi does not appear**

* Build target not x86
* Missing `.acs` file

**Speech not working**

* Windows TTS disabled

**Crashes on startup**

* COM references missing or wrong framework

---

## ⚠️ Ethics & Safety

Classic Bonzi Buddy was spyware.

This project should:

* ❌ Not spy
* ❌ Not auto-start without consent
* ❌ Not download files
* ✅ Always allow exit

---

## 📌 Final Notes

This README documents the **real Microsoft Agent API**, not a mock wrapper.

If you can call it on `IAgentCtlCharacterEx`, it belongs here.

Have fun, keep it cringe, and keep it harmless 🐵
