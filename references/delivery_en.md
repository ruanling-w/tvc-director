# TVC Output Format & Iteration Knowledge Base

> **Responsibility**: Prompt output format templates + iterative optimization guides.
> **Out of Scope**: Creative strategies (refer to [treatment_en.md](treatment_en.md)), prompt engineering (refer to [shot-language_en.md](shot-language_en.md)), storyboards & videos (refer to [storyboard_en.md](storyboard_en.md)).

---

## Part 1: Output Format Templates

Output format templates for single frames, sequences, TVC asset sequences, Multi-Phase video prompts, and End Frames.

---

## I. Mode 1: Single Keyframe Prompt

Used when the user needs to generate a **single specific frame**.

**Output Structure**:

```
### Keyframe: [Title]
**Usage**: [Role of this frame in the video—first frame / end frame / transition frame / character setting / environment setting]
**Aspect Ratio**: [16:9 / 9:16 / 1:1 / Recommended based on usage]

**Nano Banana Pro Prompt**:
[Complete prompt ready to be copied and used directly]

**Reference Image Requirements**: [Whether the user has provided reference images. Yes → label "Provided, generate with attached image"; No → label "No reference image, generate with pure text description"]

**Generation Recommendations**: [Notes for generating this image, such as parts that may require multiple fine-tunings]
```

---

## II. Mode 2: Keyframe Sequence Prompt

Used when the user needs to generate a **set of keyframes** for a complete storyboard script.

**Output Structure**:

```
## Keyframe Sequence: [Project Name]

### Generation Sequence & Dependencies
| ID | Keyframe | Type | Dependency | Priority |
|----|----------|------|------------|----------|
| 1  | ...      | Character Setting | None | ★★★★★ |
| 2  | ...      | Environmental Concept | None | ★★★★★ |
| 3  | ...      | Narrative Composition | Depends on #1, #2 | ★★★★☆ |
| ...| ...      | ...  | ...        | ...      |

### Consistency Anchors
- **Character Consistency**: [How to maintain character consistency across multiple images]
- **Environmental Consistency**: [How to maintain a unified environmental style]
- **Color Tone Consistency**: [How to maintain the color palette of the entire set of images]

---

### Frame 1: [Title]
(Same as the single-frame structure in Mode 1)

### Frame 2: [Title]
...
```

---

## III. Sequence Generation Order Principles

1. **Characters Before Scenes**: Character setting images (three-view drawings / close-ups) are generated first; subsequent scene images can reference character references.
2. **Environment Before Composition**: Independent environment concept images take priority; narrative composition is generated after both character and environment are determined.
3. **Global Before Details**: Wide shots / panoramas take priority to establish the overall atmosphere, followed by close-ups / partial shots.
4. **Keyframes > Transition Frames**: Climax frames, first frames, and freeze frames take priority; transition frames are generated last.

---

## IV. Consistency Maintenance Strategies

### Character Consistency

- First generate character three-view drawings / setting images to establish a visual baseline.
- Subsequent scene images use `[Character Name] in the image` or `Image 1` to reference character reference images.
- Clothing, hairstyle, and body type descriptions for the same character remain consistent across different scenes.
- If there are special changes (injury, outfit changes), explicitly annotate the change points.

### Environmental Consistency

- Different angles/shots of the same scene maintain the same materials, color tones, and atmospheric descriptions.
- Use unified environmental keywords to lock in the style.
- First generate environment concept images to determine the keynote, then reference them in narrative compositions.

### Color Tone Consistency

- The entire set of keyframes uses a unified art style direction (A/B/C/D/E).
- Color tone variations should follow the color arc design in the creative pitch.
- Keep the same core words in the art style anchor portion of each frame's prompt.

---

## V. Mode 3: TVC Product Asset Sequence

Used when establishing a **product visual asset library** for a TVC commercial. Product assets are the cornerstone of the TVC visual system—all subsequent scenes, video prompts, and End Frames rely on product assets as visual anchors.

**Output Structure**:

```
## Product Asset Sequence: [Product Name]

### Product Asset Inventory
| ID | Asset Type | Usage | Priority |
|----|------------|-------|----------|
| 1  | Product Hero Shot | Lock in the product's primary visual | ★★★★★ |
| 2  | Product Material Macro | Lock in the material texture | ★★★★☆ |
| 3  | Brand World Environment | Lock in the usage scenario atmosphere | ★★★★☆ |
| 4  | Product Interaction Close-up | Lock in usage actions / gestures | ★★★☆☆ |
| 5  | Product Packaging/Accessories | Lock in brand peripheral elements | ★★★☆☆ |
| ...| ...        | ...   | ...      |

### Product Consistency Anchors
- **Product Appearance**: [Precise description of the product's shape, proportions, and signature design features]
- **Material / Lighting**: [Product surface material type, reflection characteristics, recommended lighting setup]
- **Brand Colors**: [Specific color codes or descriptive definitions for primary/secondary/accent colors]
```

```
### Asset 1: Product Hero Shot
**Usage**: Lock in the product's primary visual, serving as the reference baseline for all subsequent product shots.
**Aspect Ratio**: 16:9

**Nano Banana Pro Prompt**:
[Complete prompt ready to be copied and used directly]

**Reference Image Requirements**: [Whether the user has provided product reference images. Yes → label "Provided, generate with attached image"; No → label "No reference image, generate with pure text description"]

**Generation Recommendations**: [Notes for generating product renders, such as material precision, Logo clarity, etc.]

---

### Asset 2: Product Material Macro
...

### Asset 3: Brand World Environment
...
```

**Key Usage Points**:

- The Product Hero Shot is the highest priority asset and must be generated and confirmed first.
- All subsequent keyframes and video prompts involving the product must reference the Hero Shot as the visual anchor.
- Brand world environment images are used to lock in the atmospheric keynote of the scenes where the product appears, with subsequent scene frames refined on this basis.

---

## VI. Mode 4: TVC Multi-Phase Video Prompts

Used when generating **segmented prompts that can be directly used in video generation tools** for a specific storyboard section of the TVC. Each Segment corresponds to one panel in the multi-grid storyboard.

**Output Structure**:

```
## TVC Video Prompt: [Project Name] · Segment [N] ([Timeframe])

**Corresponding Multi-Grid**: Grid [N]
**World Type**: Product World / Brand World / Crossover
**Duration**: [X]s

**Multi-Phase Video Prompt**:
Style: [Overall visual style description—tone, color keynote, texture]
Phase 1 (0-Xs): [Description of motion / action / visual content]
Phase 2 (X-Ys): [Description of motion / action / visual content]
Phase 3 (Y-Zs): [Description of motion / action / visual content]
...
Lighting Requirements: [Lighting tone of this segment—natural light / studio light / special effects light, etc.]

**First-Frame Keyframe Reference**: [Corresponding keyframe asset ID or name]

**Transition Notes**:
- Connection with the previous segment: [Visual / motion / emotional transition method from end frame to first frame]
- Connection with the next segment: [How the end frame of this segment sets up the first frame of the next segment]
```

**Key Usage Points**:

- The first frame of each Segment should be anchored by the already generated keyframe asset to ensure the controllability of the video's starting scene.
- Phase division is based on the movement rhythm within the shot, rather than mechanically dividing the time equally.
- Transition notes are key to TVC fluidity—ensuring that the movement direction, color tone, and emotion between segments do not break.
- World Type annotations are used to quickly identify whether the segment belongs to product display logic or brand narrative logic.

---

## VII. Mode 5: End Frame Dedicated Output

Used when generating the **final freeze-frame (End Frame)** of a TVC commercial. The End Frame is the final visual resolution of the entire ad, carrying brand recall and call-to-action.

**Output Structure**:

```
### End Frame: [Product Name]
**Usage**: TVC final freeze-frame
**Aspect Ratio**: 16:9
**Text Overlay Area**: [Description of reserved space for Logo and Slogan—e.g., "Top 1/3 of the frame left blank for Logo centering, bottom 1/5 area for Slogan"]

**Nano Banana Pro Prompt**:
[Complete prompt ready to be copied and used directly—the frame must reserve space for text overlay, avoiding core visual elements occupying the text area]

**Reference Image Requirements**: [Whether brand VI reference images, Logo files, etc., are needed]

**Generation Recommendations**: [Generation notes unique to the End Frame, such as control of blank spaces, brand color accuracy, etc.]

**Post-Overlay Guidelines**:
- **Logo Position**: [Specific area description, e.g., "Top-center of the screen, occupying 30% of the screen width"]
- **Slogan Position**: [Specific area description, e.g., "Directly below the Logo, with a spacing of approximately 40px from the Logo"]
- **Recommended Font Style**: [Font style suggestions matching the brand tone, e.g., "Sans-serif / Modern / Handwritten"]
- **Recommended Text Color**: [Text color suggestions based on the frame's background color]
```

**Key Usage Points**:

- The End Frame prompt must deliberately reserve space for text overlays; this is the core difference from regular keyframes.
- The visual should be clean, premium, and restrained, avoiding complex scenes that compete with the product for visual attention.
- The presentation of brand colors in the End Frame must be highly accurate; referring to the brand VI manual is recommended.
- Post-overlay guidelines provide executable layout solutions for designers, reducing back-and-forth communication costs.

---

## VIII. TVC Sequence Generation Order Principles

Asset generation for TVC commercials follows a **product-first, layer-by-layer progression** order, ensuring visual consistency radiates outward from the core:

1. **Products Before Scenes**: The Product Hero Shot is generated first to lock in the product's visual baseline (shape, materials, lighting). All subsequent frames involving the product use this as a reference anchor.
2. **Products Before Brand World**: Once all product assets are confirmed, generate the environment, atmosphere, and narrative scenes of the brand world. Avoid generating scenes first, which leads to style mismatch between the product and environment.
3. **Multi-Grids Before Video Prompts**: Once all multi-grid storyboard keyframes are locked, generate the Multi-Phase video prompts segment by segment. Keyframes are the visual anchors for video prompts; the order cannot be reversed.
4. **End Frame Last**: The End Frame is generated last after all visual directions are locked. By this time, the color tone, texture, and brand expression of the entire TVC are fully clarified, allowing the End Frame to precisely resolve the film's overall tone.

---

## Part 2: Iterative Optimization Guide

Single-variable iteration principles, 11 common failure modes & correction schemes, fine-tuning tips, and version management.

---

## I. Core Principles of Iteration

### 1. Single-Variable Principle

Modify only **one variable** per iteration to observe changes in effect. If you change three places at the same time, it is impossible to determine which modification worked.

| Practice | Effect |
|------|------|
| ❌ Changing composition + lighting + color tone at once | Unable to attribute cause; might fix one but ruin two others |
| ✅ Modifying only the lighting description first | Clarifies whether the lighting description is the root cause of the issue |
| ✅ Adjusting composition after confirming lighting is OK | Progressively approaches the target |

### 2. Addition and Subtraction Principle

The first step of correction is determining whether the problem is "too much of something" or "not enough of something":

- **Unwanted elements added** → Subtraction: Delete words that might imply that element.
- **Desired effect missing** → Addition: Add more specific descriptive words.
- **Effect direction is wrong** → Replacement: Substitute with words that have more precise meanings.

### 3. Position Weight Principle

In Nano Banana Pro, **words positioned earlier have higher weight**. If a certain effect is not strong enough:
- Move the corresponding description **to a more forward position**.
- Or **add at the very beginning** the most important quality/style anchors.

### 4. Avoid "Getting Worse as You Edit"

| Pitfall | How to Avoid |
|------|---------|
| Finetuning the same sentence repeatedly over a dozen times | Take a step back to analyze the root cause when fine-tuning is ineffective after 3 attempts |
| Adding too many words to fix a single issue | Longer prompts do not equal better results; simplify and start over |
| Swinging from one extreme to another | Do not change directly from "too dark" to "bright"; use intermediate states as transitions |
| Forgetting previously successful versions | Retain the prompt text of each iteration so you can roll back at any time |

---

## II. Common Failure Modes & Correction Schemes

### Mode 1: Frame Too Bright / Not Dark Enough

**Symptoms**: Even though "extremely dark" was requested, the generated result is still bright or has unreasonable light sources.

**Root Cause Analysis**:
- Description contains words implying light sources (e.g., mentioning "torches", "lights", "sunlight", etc.)
- The description of "dark" is not strong enough.
- Did not explicitly state "almost entirely black".

**Correction Scheme**:
```
Add: Extremely dark environment / Almost entirely black environment / Most of the space engulfed in deep shadows
Add: Rapid light falloff
Delete: Any words that might imply extra light sources (torches, lights, bright XX)
Prepend: Move "extremely dark" to the very beginning of the description
```

### Mode 2: Unwanted Objects Appearing

**Symptoms**: Objects that were not requested (such as unwanted torches, characters, furniture, etc.) appear in the frame.

**Root Cause Analysis**:
- Certain descriptive words implicitly contain these objects (e.g., "cave" might automatically generate torches).
- Contextual implication (e.g., "hall" might automatically generate furniture).

**Correction Scheme**:
```
Method 1: Directly delete descriptions that might imply the object.
Method 2: If the object still appears after deletion, add negative instructions at the end of the description.
Method 3: Replace vague space-type words with more specific spatial descriptions.
```

**Example**: Do not want torches
```
❌ A dim underground cave hall
✅ An extremely dark underground abyss hall, without any artificial light sources, only faint blue bioluminescence
```

### Mode 3: Insufficient Spatial Depth / Not Grand Enough

**Symptoms**: Although "grand" was described, the generated space looks small and flat.

**Root Cause Analysis**:
- Lack of vertical dimension descriptions (ceiling/dome).
- Lack of atmospheric perspective (fog, dust).
- Camera angle is not extreme enough.
- Lack of reference objects to provide a sense of scale.

**Correction Scheme**:
```
Add: Ceiling towering into the clouds, disappearing into heavy darkness (vertical dimension)
Add: Extremely dense volumetric fog permeating the air, making the distance misty and ethereal (atmospheric perspective)
Add: Very low camera angle to highlight the terrifying height of the space (extreme angle)
Add: Giant biological pillars supporting the darkness like towers of Babel (reference object + scale metaphor)
```

### Mode 4: Character Face Looks Bad / Deformed

**Symptoms**: The character's face is deformed, unnatural, or differs significantly from the reference image.

**Root Cause Analysis**:
- Facial description is too complex; the AI cannot satisfy all requirements simultaneously.
- No reference image was provided.
- Lighting conditions are unfriendly to faces (too dark or too complex mixed lighting).

**Correction Scheme**:
```
Strategy 1: Simplify facial descriptions, retaining only 1-2 core features.
Strategy 2: Upload a character reference image, referencing it with "[Character Name] in the image".
Strategy 3: Use lighting that flatters the face—side lighting / backlight semi-silhouette yields better results than flat front lighting.
Strategy 4: If it is a keyframe rather than a setting sheet, use profile views / semi-silhouettes to bypass front-face details.
```

### Mode 5: Incorrect Color Tone

**Symptoms**: The screen tone does not match expectations (too warm / too cold / too saturated / not saturated enough).

**Root Cause Analysis**:
- Color tone descriptions are not explicit enough.
- Light source color contradicts the target color tone.
- Art style anchors imply a different color tone.

**Correction Scheme**:
```
Explicit tone words: Desaturated cold gray-blue / Blood orange deep red / Amber warm gold / Cold blue-green
Ensure light source colors are consistent: If a cold tone is desired, the light source should also be blue/white, not warm yellow
Check art style anchors: Certain style words carry inherent tone tendencies (e.g., "Golden Hour" naturally leans warm)
```

### Mode 6: Scattered Composition / Subject Not Prominent

**Symptoms**: The frame has no focus, elements are distributed chaotically, and it's unclear where to look.

**Root Cause Analysis**:
- No composition rules were specified.
- Described too many elements of equal weight.
- Lack of depth of field control.

**Correction Scheme**:
```
Add explicit composition: Character located at [position] rule of thirds / Centered symmetrical composition
Reduce elements: Delete non-core elements to make the subject stand out
Add depth of field: Extremely shallow depth of field, focus on [subject], with the rest blurred
Specify visual guidance: Use [light / roads / lines] to guide the eye to the subject
```

### Mode 7: Material Texture Insufficient / Too Fake

**Symptoms**: Metal looks like plastic, skin looks like wax, and fabric looks like cardboard.

**Root Cause Analysis**:
- Material descriptions are too general.
- Lack of micro-level physical details.
- Lighting is not complex enough (lacks reflection, sub-surface scattering, etc.).

**Correction Scheme**:
```
Metal: Add "brushed texture", "worn sheen", "micro-oxidation marks"
Skin: Add "pores", "fine sweat droplets", "natural flush of uneven skin tone"
Fabric: Add "woven texture", "folds and creases", "frayed/worn edges"
General: Add "wet reflection" (adding a layer of wetness to all surfaces will look more realistic)
```

### Mode 8: Generated Image Too Flat / Lacking Layering

**Symptoms**: The screen feels like a flat texture map, lacking spatial depth.

**Root Cause Analysis**:
- Lack of foreground, midground, and background layering.
- No atmospheric perspective effects.
- All elements reside on the same focal plane.

**Correction Scheme**:
```
Add layering: Foreground: [out-of-focus elements]. Midground: [subject]. Background: [environment]
Add atmosphere: Volumetric fog / dust particles permeating the air
Add depth of field: Specify focal point location, allowing other layers to blur naturally
Add lighting layers: Strong light in the foreground fading in the distance, or use backlighting to create layers
```

### Mode 9: Excessive CG Feel / Not Looking Like a Real Person

**Symptoms**: Even though real-life photographic effects were desired, the generated result looks like a 3D model / CG rendered character. The skin is overly smooth, lighting is too uniform, and there is an overall "digital feel".

**Root Cause Analysis**:
- Art style anchors lean toward CG (e.g., "hyper-realistic cinematic style" is interpreted by the model as "hyper-realistic CG rendering").
- Three-view drawings/setting sheets themselves are design/modeling concepts; the model naturally inclines toward CG outputs.
- Lack of photographic anchors to pull toward real-life.
- Directorial contradiction between quality anchors and art style anchors.

**Correction Scheme**:
```
Core Replacement: Replace all CG-leaning anchors with real-life photographic anchors
  ❌ Hyper-realistic cinematic style / 3A game 3D gaming style
  ✅ Real-life shoot, cinematic photography, real skin pore texture, natural lighting

Add Real-Life Reinforcements (choose as needed):
  + Real skin pore texture (forces microscopic details of real skin)
  + Natural lighting (avoids CG-style uniform lighting)
  + RAW photo texture (unprocessed raw photographic feel)
  + Cinematic film colors (film-like color tone)

Check and Delete All CG-leaning Words:
  Delete: "master-class CG rendering", "Unreal Engine 5 render", "3A game", etc.
```

**Example**:
```
❌ Alvin character three-view drawing... style is hyper-realistic cinematic style.
✅ Alvin character three-view drawing... real-life shoot, cinematic photography, real skin pore texture, natural lighting.
```

### Mode 10: Excessive Realism / Wanting CG But Too Realistic

**Symptoms**: Desired 3A game CG texture, but the generated result looks too much like a real photo, lacking the refinement and artistry of CG.

**Root Cause Analysis**:
- Art style anchors lean toward real-life.
- Used anchors like "real-life shoot", "photography", etc.
- Lack of CG-leaning anchors.

**Correction Scheme**:
```
Core Replacement: Replace real-life anchors with CG anchors
  ❌ Real-life shoot, cinematic photography
  ✅ 3A masterpiece 3D game style / Master-class CG rendering

If more refined CG is wanted:
  ✅ Unreal Engine 5 render, subsurface scattering skin, PBR materials, global illumination

Delete All Real-Life Leaning Words:
  Delete: "real-life shoot", "real skin pore texture", "natural lighting", "RAW photo", etc.
```

### Mode 11: Style Mismatch / Oscillating Between Real-Life & CG

**Symptoms**: The generated results are unstable between real-life and CG; some outputs look real, while others look like CG, or certain areas in a single image look real while others look like CG.

**Root Cause Analysis**:
- Conflicting internal directions in art style anchors (containing both real-life and CG keywords simultaneously).
- Directional inconsistency between quality anchors and art style anchors.
- Double-meaning words like "hyper-realistic movie quality" are not constrained by explicit directional words.

**Correction Scheme**:
```
Diagnosis: Check all style/quality-related words in the prompt, marking their directional category
  Real-life directional words: real-life shoot, cinematic photography, skin pores, natural lighting, RAW photo
  CG directional words: 3A game, CG render, Unreal Engine, PBR materials
  Double-meaning words (need attention): hyper-realistic movie quality, cinematic color grading, 8K ultra-clear

Correction: Ensure all directional words point in the same direction
  ❌ Hyper-realistic movie quality... 3A masterpiece 3D game style... real skin pore texture
  ✅ Real-life shoot, cinematic photography... real skin pore texture, natural lighting (All real-life directions)
  ✅ Master-class CG rendering, 8K ultra-clear resolution... 3A masterpiece 3D game style (All CG directions)
```

---

## III. Fine-Tuning Techniques

### Impact Rules of Adding Words

| Added Word | Typical Impact |
|---------|-----------|
| "extremely", "intensely" | Enhances the effect of the immediately following descriptive words |
| "faint", "weak" | Weakens the intensity of the light source / effect |
| "dense", "thick" | Increases the density of fog / smoke |
| "almost entirely black" | Heavily darkens the overall frame |
| "disappearing into darkness" | Blurs the boundaries of distant / high areas |
| Specific numbers (e.g., "60 meters") | Helps AI establish scale concepts |
| Frame proportion (e.g., "occupies 70% of the screen") | Precisely controls the size of elements |

### Impact Rules of Deleting Words

| Deleted Word | Typical Impact |
|---------|-----------|
| Delete extra light source descriptions | Frame becomes darker |
| Delete specific objects | Object disappears (but not guaranteed, AI might infer from context) |
| Delete color adjectives | AI chooses the color tone automatically (can be unstable) |
| Delete composition instructions | AI randomizes composition (not recommended) |

### Word Replacement Tips

| Original Word | Replaced With | Effect Change |
|------|--------|---------|
| dim | extremely dark / almost entirely black | darker |
| grand | extremely grand, ceiling towering into the clouds | more sense of space |
| blue light | faint blue light source | weakened light |
| smoke/fog | extremely dense volumetric fog | thicker fog |
| wide-angle | wide-angle lens, very low angle | more extreme perspective |

---

## IV. Iteration Workflow

### Standard Iterative Flow

```
1. First Generation: Use the complete prompt
   ↓
2. Evaluate Results: Compare with target visuals, find discrepancies
   ↓
3. Diagnose Issues: Which dimension is problematic?
   - Color tone? Lighting? Composition? Subject? Environment? Material?
   ↓
4. Single-Variable Modification: Only modify descriptions of the problematic dimension
   ↓
5. Second Generation: Observe changes
   ↓
6. If OK → Move to fine-tuning the next dimension
   If not OK → Return to Step 3, choose a different modification strategy
   ↓
7. Over 3 Ineffective Modifications → Take a step back, check if it's a fundamental concept issue
```

### Quick Diagnosis Checklist

When generated results are unsatisfactory, troubleshoot item by item using the following checklist:

- [ ] **Is the art style direction correct?** → Check if the art style anchors point in the correct direction (real-life/CG/engine grade), and whether there are conflicting directional words.
- [ ] **Is the quality up to standard?** → Check if quality anchor words are at the very beginning.
- [ ] **Is the subject correct?** → Check if the subject description is clear and accurate.
- [ ] **Is the spatial depth correct?** → Check the scale and atmospheric effects of the environment description.
- [ ] **Too bright or too dark?** → Check light source quantity, intensity, and light/dark descriptive words.
- [ ] **Is the color tone correct?** → Check color descriptive words and light source colors.
- [ ] **Is the composition correct?** → Check if composition instructions are explicit.
- [ ] **Are there unwanted elements?** → Check if any descriptive words imply unwanted objects.
- [ ] **Is the material texture sufficient?** → Check if there are microscopic physical detail descriptions.
- [ ] **Is the spatial layering sufficient?** → Check if there is foreground/midground/background layering and depth of field control.

---

## V. Real-World Failure-to-Success Path Examples

### Example: Dark Underground Hall

**Target**: Extremely dark, grand underground space with only faint blue light.

**Attempt 1**:
```
A dim underground cave hall, blue light. 3A game style.
```
❌ Result is too bright, the space is not big enough, and torches appeared.

**Diagnosis**: Description too simple; "cave" implies torches; "dim" is not strong enough.

**Attempt 2**:
```
Extremely grand underground abyss hall, ceiling towering into the clouds. Extremely dark environment, almost entirely black. Faint blue light source. 3A game masterpiece quality.
```
❌ Space grew larger, but texture and volume are insufficient.

**Diagnosis**: Lacks atmospheric effects and material descriptions.

**Attempt 3**:
```
Extremely grand underground abyss hall, ceiling towering into the clouds, disappearing into heavy darkness. 3A game masterpiece quality. Extremely dark environment, almost entirely black. Faint blue light source outlining the grand silhouette of the space. Extremely dense volumetric fog permeating the air. Walls covered in wet, reflective chitinous shell textures, giant biological pillars supporting the darkness like towers of Babel. Wide-angle lens, very low angle to highlight the terrifying height of the space.
```
✅ Achieved target effect.

**Key Improvements**: Added volumetric fog (spatial depth), material description (texture), very low angle (height perception), and "disappearing into darkness" (infinite extension feel).

---

## VI. Version Management Recommendations

To avoid "getting worse as you edit" or "forgetting previously successful versions", it is recommended to:

1. **Number each prompt**: v1, v2, v3...
2. **Record what was modified each time**: v2 vs v1 = added volumetric fog description
3. **Mark satisfaction**: ★★★☆☆
4. **Retain the best version**: Ready to roll back to previous optimal states at any time
5. **Record successful patterns**: If a certain combination of descriptions yields excellent results, document it as a template for the future.
