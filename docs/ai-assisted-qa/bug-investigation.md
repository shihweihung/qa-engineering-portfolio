# Bug Investigation with AI

## Where AI Helps

**Explaining code behavior.** When I'm investigating a bug and need to understand a piece of code I didn't write, I paste it into an AI assistant and ask what it does. This is faster than reading documentation or asking a developer when the developer is busy. Understanding the code is often the first step to understanding why it's failing.

**Generating hypotheses.** When I describe a bug's symptoms to an AI assistant, it generates a list of potential causes. Not all of them are plausible for my specific system, but the list is a useful forcing function — it makes me think through each hypothesis and rule them out, which is more systematic than following a single intuition.

**Log parsing and pattern matching.** For bugs that produce a lot of log output, AI can help identify patterns in structured log data faster than reading line by line. I've used this for production incidents where the signal was buried in a large volume of log data.

**Summarizing error messages.** Cryptic stack traces or error codes that I don't immediately recognize are faster to diagnose when I can ask an AI to explain what the error means in context.

---

## Where AI Doesn't Help

**System-specific context.** AI doesn't know our architecture, our data model, or the history of a particular subsystem. When the answer to "why is this failing" depends on knowing that one service has a known timing issue or that a particular API endpoint behaves differently for accounts created before a certain date — that knowledge comes from me, not from AI.

**Reproducing the bug.** AI can't run code or interact with the product. The observation and reproduction work is entirely manual.

**Making the judgment call.** Is this a blocker? Is this a known issue? Does this match a previous bug? Those calls require context and experience that AI doesn't have.

---

## How I Use It in Practice

Bug investigation is the area where I use AI most opportunistically. When I hit a wall — can't figure out what's causing something, don't understand a piece of the system, need another perspective on what might be wrong — I describe the situation to an AI assistant and see what it surfaces.

It's like having a rubber duck that sometimes has useful suggestions.
