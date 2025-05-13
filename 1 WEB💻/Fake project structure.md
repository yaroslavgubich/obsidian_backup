
#structure #fake #project 
# Build and Deploy a Unique 3D Web Developer Portfolio with React, Three JS & GSAP

[](https://www.youtube.com/@javascriptmastery)
### How much time will this take?

|Stage|What you’ll actually do|**Realistic time** for a careful beginner (Yaroslav-level)|
|---|---|---|
|**1. First watch-through (no typing)**|Play the **≈ 3 h 45 min** video at 1.25× speed, take rough notes.|~ 3 h|
|**2. Type-along “copy” pass**|Pause every few minutes, replicate the code 1-for-1, debug typos, run `pnpm dev`.|6 – 8 h|
|**3. Immediate “blind” rebuild**|Close the repo, create a fresh branch/folder and rebuild **without looking**, consulting notes only when stuck (< 5 min each time).|5 – 7 h|
|**4. Day-after memory check**|Re-implement the trickiest bits (GSAP timeline, Three.js model import, EmailJS) from scratch.|2 h|
|**Total commitment**|**≈ 16-20 hours** spread over 3-4 evenings or a full weekend.||

_(If you already know basic React + Tailwind, shave ~25 %. If you hit lots of ESLint/Tailwind errors, add ~2 h.)_

---

### What you **must** understand vs. what’s safe to gloss over

|Worth deep understanding|Okay to treat as “black box” (come back later)|
|---|---|
|• Folder structure (`src/components`, `constants/index.js`)||
|• React component patterns (props, state, `useRef`, `useEffect`)||
|• Tailwind utility mindset (spacing, breakpoints)||
|• GSAP basics: `gsap.from`, `ScrollTrigger` life-cycle||
|• Three.js fundamentals: `<Canvas>`, loading a GLB, lighting, orbit controls||
|• Deployment flow (`pnpm run build`, `vercel --prod`)|• Precise math behind mouse-angle → glow (you can copy)|
|• Fine-tuning conic-gradient CSS for the glow||
|• Exact EmailJS dashboard setup (once it works, move on)||
|• Shaders & advanced material settings (can swap for a plain MeshStandard)||
|• Every Tailwind class name (build intuition over time)||

Trying to master the right-hand column on first pass is a **time sink**—park questions in a TODO list and revisit when the core app runs.

---

### My 3 comprehension checks for you

1. **Why does each `GlowCard` store its DOM node in an array ref instead of a single `useRef`?**
    
2. **What problem does `ScrollTrigger` solve compared to a pure CSS `@keyframes` animation?**
    
3. **When you deploy to Vercel, why do you still run `pnpm run build` locally before `vercel dev --prebuilt`?**
    

Answer those out loud (or in reply) to be sure the big ideas stick. If any feel fuzzy, that’s the detail worth another 20 min, not another 2 h.