first some meta info about me for context. my entire ecosystem consists of the Clod Pro Plan with Clod assisting me inside VS Code or through the Windows 11 Clod Code/Cowork app and less often at Clod.ai. I give them all maximum permissions and trust. I am already onboarded on how to "sync" skills and sessions across all 3 domains so im not asking about that.

i need to instruct clod code with several very short skills (maybe up to 6) that map across my entire ecosystem of webdev.


SKILL 1. GENERATE FILE 

The Prollem: sometimes i ask clod to generate something and drop it in the present project. he generates it and even shows it but when i eventually look for it i cant find it anywhere but it still shows in browser which means its likely sandboxed for safety.

The Fix: after sandbox always save file inside project in a folder called GENERATED

Justification: we can bypass the doublewall fortress of safety (browser's sandbox and clod's VM) for 3 solid reasons:

1. im not compiling anything to binary which might encroach onto or damage existing OS components or other apps. i dont even do node. and i rarely touch python and when i do i dont even compile it (i know it doesnt need to compile to be dangerous) and with pythin i always work out of a sandbox anyway.

2. since i primarily i only do clientside webdev and a little backend but only the safe stuff like json fetching, the browser already forms a near impenetrable sandbox. i dont need a doublewalled fortress to protect me.

3. asset protections : a worst case scenario is a lose 1 hour of work (ive never lost any work from direct project file live coding) because that is my regular github commit push frequency.

here the start for a new skill which gem help generate but it assumes only one skill with wrong name and far too verbose. the set of miniskills should be called onboard. the actual keyword should be: generate file

```markdown
---
name: persistent-workspace-generator
description: Overrides ephemeral sandbox behavior for client-side web technologies (HTML, CSS, JS, JSON) by forcing generated code to be saved into a local GENERATED directory with proper file extensions.
---

# Persistent File Generation Protocol

When handling code generation requests for client-side web technologies (JavaScript, HTML, CSS, JSON) that would otherwise default to an ephemeral sandbox or temporary virtualized path, follow these operational rules:

1. **Proper Naming & Extensions:** Every generated file must be fully realized with its correct name, extension, and clear relative file paths indicated at the top of the output block.
2. **Local Directory Routing:** Check the root of the active project folder. If a folder named `GENERATED` does not exist, create it. 
3. **Workspace Drop-In:** Save or present all generated project files so they target the `GENERATED` directory, ensuring they remain immediately accessible in the local workspace environment without relying on session-cached container hashes.

```