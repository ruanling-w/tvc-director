# TVC Storyboard & Video Engineering Knowledge Base

> **Responsibility**: The sole reference for storyboarding and filming stages. Covers multi-grid storyboards, video prompt syntax, cinematic product breakdowns, and brand world shots. Multi-grids and video prompts are matching deliverables—each multi-grid corresponds to a segment of video prompts.
> **Out of Scope**: Creative strategies (refer to [treatment_en.md](treatment_en.md)), image prompt syntax (refer to [shot-language_en.md](shot-language_en.md)), output formats and iterations (refer to [delivery_en.md](delivery_en.md)).

---

## Part 1: Multi-Grid Storyboards

---

## I. Multi-Grid Prompt Four-Layer Structure

A complete multi-grid prompt consists of four layers, ordered as follows:

### Layer 1: Global Style

Defines the visual tone and physical format of the entire image. Must include:

- **Grid Declaration**: `Generate an image containing N storyboard panels, arranged in a RxC grid`
- **Art Style Anchor**: Consistent with the art style direction confirmed in Phase 3 (refer to `art-style-library.md`)
- **Aspect Ratio**: Aspect ratio of the entire multi-grid image (typically 16:9 or 1:1)
- **Rendering / Shooting System** (optional): E.g., `shot on ARRI Alexa cinematic camera` or `real-time rendered in Unreal Engine 5`, used to lock in image quality

Example Writing:
> Generate an image containing 9 storyboard panels, arranged in a 3x3 grid. 3D fantasy animation style, shot on ARRI Alexa cinematic camera, 16:9 widescreen.

### Layer 2: Reference Image Mapping

When using `edit` mode to reference Phase 4 asset images, establish mapping relationships in this layer.

Format: `(Image 1)[Asset Type/Name], (Image 2)[Asset Type/Name]...`

If there are no reference images (pure text-to-image), skip this layer and describe the key appearance features of the character/environment in text within Layer 1.

### Layer 3: Narrative Line + Grid-by-Grid Descriptions

This is the core of the multi-grid prompt. The writing style varies with plot density—see Section IV for details.

### Layer 4: Consistency Anchor

After all grid-by-grid descriptions, append global consistency requirements:

- **Style Unity**: `Keep overall style consistent` (must have)
- **Visual Motif**: Elements that repeatedly appear throughout all panels (e.g., a certain color, a certain lighting effect, a certain prop)
- **Color Tone Continuity**: Describes the color/lighting gradient trends across panels
- **Character Consistency**: If characters appear across multiple grids, emphasize that their appearance must not change
- **Video Stream**: Brief summary of how the 9 grids flow as a video—camera movement trajectories, product state changes, key transition points (e.g., `Video Stream: Panorama entry (P1) -> Arc around bottle (P2-P3) -> Macro dive (P4) -> ... -> Freeze frame (P9)`). This is not a command for the image generation model, but a cognitive anchor for downstream video prompt writing.

---

## II. Video Thread First

Multi-grids are not a platter of 9 beautiful images—they are 9 keyframes frozen from a 15-second video. **Flow first, then frames.**

### Core Principles

Before writing grid-by-grid descriptions, outline the 1-2 sentence **video thread** of these 15 seconds: how the camera language is continuous, how the product state changes, and how frames connect. The video thread is the causal chain on the timeline—what each grid inherits, what it transitions to—not just "9 grids looking good together".

The video thread **is not equivalent to a single long take**. It can include hard cuts, match cuts, dissolves, jump cuts, and various transitions—the key is the continuity of the camera language, not the physical continuous movement of the camera. A single long take is a choice, and multi-shot editing is another choice, but each grid must know its position on the timeline.

Multi-grids are the **freezing** of the video thread, and video prompts are the **expansion** of the video thread. Both grow from the same thread; there is no sequence of "generating images first then matching video".

### Three Densities, Same Principle

- **High Density** "narrative lines" are naturally the video thread—character actions flow across grids, and temporal causality is embedded in the narrative.
- **Medium Density** "journey overviews" approach the video thread—scene progression itself contains a temporal flow.
- **Low Density has no story, but must have a video thread**—camera language continuity, lighting changes, and product state transitions are the temporal causalities of low density. "No narrative arc" does not equal "no temporal flow".

### Video Thread Writing (Low Density Example)

Before the grid-by-grid descriptions, add a line for the video thread:

> Video Thread: Slow push into balcony panorama -> tabletop still life -> side low-angle penetrating bottle caustic -> silhouette of bottle in front of backlit curtain -> cat looking up echoing with the amber color of the out-of-focus bottle in the foreground -> high-angle shot of tabletop still life anchor -> bottle cap macro -> bottle on railing with distant view -> she walks over, bottle on the table in the background

### Video Thread is Not Part of the Prompt

The video thread is a **cognitive step** before writing, not a text output to the image generation model. It can be written in the "Video Stream" annotation of Layer 4's consistency anchor (for downstream video prompt reference), but it will not appear in the main prompt text of Layers 1 to 3.

### Division of Labor for Dynamic Special Effects

When the creative pitch includes dynamic visual special effects (material deformation, particle aggregation, energy flow, etc.): **multi-grids only freeze the final state of the effects, while video prompts describe the complete process of the effects.** Multi-grids are static keyframes and cannot express "change"—forcing process descriptions will only clutter the image.

| Dynamic Concept | Multi-Grid (Freeze Final State) | Video Prompt (Describe Complete Process) |
|------|------|------|
| Liquid metal condensing into product | Product fully formed | Liquid metal flowing -> decelerating -> condensing -> surface texture changing -> forming |
| Product suspended disassembly | Exploded view with separated components | Components slowly separating, hovering, connected by energy lines animation |
| Screen lighting up | Screen lit, displaying interface | Pixels lighting up from center -> waves diffusing -> interface elements emerging |
| Particles aggregating into form | Product fully presented | Particles aggregating from all directions -> silhouette emerging -> surface solidifying |
| Water droplets rolling down shoe upper | Water droplets condensing on a certain spot of shoe upper | Water droplets sliding along fabric -> proving waterproof performance |
| Liquid spilled (coffee/wine) | Liquid suspended in mid-air, forming a frozen curved liquid column | Cup knocked over -> liquid flying out -> solidifying in mid-air -> caught/straightened |
| Character "frozen" | Character stays in walking/motion posture still, clothing corners suspended | Everyone suddenly stops moving -> environmental sound disappears -> only the protagonist moves freely |
| Paper/fragment storm | Papers suspended in mid-air at various angles still | Wind rising -> papers fluttering -> suddenly stopping and hovering -> taken away sheet by sheet |

---

## III. Grid Specification Selection Strategy

| Specification | Grids | Duration Coverage | Applicable Scenario |
|------|-----------|-------------|------|
| **3x3** | 9 grids | ≈15 seconds | Standard narrative segments, complete product promo flow, most common |
| **2x2** | 4 grids | ≈5-8 seconds | Short transition sequences, simplified clips, opening/closing |
| **2x3** | 6 grids | ≈10 seconds | Medium density narrative, vertical video |
| **3x2** | 6 grids | ≈10 seconds | Horizontal medium density |

Selection Principle: Default to **3x3**; use **2x2** or **2x3** when content is less than 6 frames; vertical prefers **2x3**, horizontal prefers **3x2** or **3x3**.

---

## IV. Plot Density Spectrum: Grid-by-Grid Description Writing

Multi-grids' core difference lies in **plot density**—how much weight character actions/story progression occupy vs. how much weight camera instructions/visual design occupy.

**TVC Density Statement**: TVC commercials only use **Low Density** and **Medium Density** modes, with low density as the default. High density mode (letting the AI decide shot size) does not apply to TVCs—every single frame of the commercial requires precise aesthetic control; composition decisions must not be left to the AI.

### 4.1 Medium Density: Scene Progression

**Characteristics**: Has narrative progression (journey/process), but each grid is also a relatively independent scene. Mixed actions and camera instructions.

**Writing Style**: First write a narrative line summarizing the journey, then describe grid by grid. Shot sizes are optional.

**Complete Example (Pasture Morning · Entering the Pasture)**:

```
Generate an image containing 9 storyboard panels, arranged in a 3x3 grid.
Real-life shoot, cinematic photography, natural lighting, 16:9 widescreen.

Narrative Line: A complete early morning of a mountain pasture before dawn, with the pasture owner getting up alone, going out, and walking through the thin mist toward the cattle herd.
The color tone gradually transitions from cold blue-gray in Panel 1 to warm golden-green in Panel 9, simulating the process of morning light illuminating the pasture.

1. Rolling hills shrouded in blue-gray thin mist, the sky transitioning from deep blue to faint gold. At the very bottom of the frame, the orange lamp light shining through the window of the log cabin is the only warm color.
2. The pasture owner's rough hands turning on an old brass tap under dim yellow light, clean water washing through the finger gaps, water droplets rolling along the rough skin.
3. The wooden fence disappearing into the distance in thin mist, water droplets condensing on the fence, an old leather glove slung on the horizontal bar—he just passed here.
4. Low angle tracking the old brown leather boots stepping on wet grass, with grass blades bending and dew drops splashing and bouncing at each step. The light gradually turns warmer.
5. The pasture owner pushing open the heavy wooden door of the cowshed, golden morning light pouring from the door crack forming radial rays, illuminating fine dust dancing in the air.
6. Dew drops on a cobweb illuminated by the pouring morning light, silk threads shimmering like silver strings. A dew drop slowly sliding down under slight vibration.
7. Golden Tyndall rays penetrating dense fog to illuminate the foreground grass, fine dust particles floating in the light beams. In the depths of the fog, the silhouette of a person in a work jacket is walking toward the deep pasture.
8. Golden morning light filtering through the gaps of oak branches and leaves, the leaf edges translucent golden-green. A shiny metal milk pail in the shadow under the tree, its wall reflecting a warm light.
9. Pasture panorama, thin mist dispersing, golden sunlight covering the pasture. In the distance, the figure of the pasture owner has walked near the cattle herd, both human and cattle outlined with golden edges by the warm light.

Keep overall style consistent. Visual motif: the pasture owner's "hands" and "footsteps" run throughout all panels.
Tyndall rays and grass tip dew drops appear repeatedly as environmental clues. Cinematic color grading.
```

### 4.2 Low Density: Visual-Driven (TVC Default)

**Characteristics**: No narrative arc, but has a **video thread**—each grid is a keyframe extracted from a video with continuous camera language, rather than an independent visual design. Pure product/atmosphere display, precise camera instructions.

**Writing Style**: First write a **video thread** (camera language continuity + product state flow), then describe grid by grid. Each grid begins with `[Shot Size · Angle]`, precisely specifying camera language, lighting design, and product angle.

**Complete Example (Perfume Commercial · Multi-Angle Light and Shadow Display)**:

```
Generate an image containing 9 storyboard panels, arranged in a 3x3 grid.
With the perfume product of Image 1 as the subject, pure black background, warm gold side light + white smoke, luxury texture.

Video Thread: Panorama entry -> rotate to display facets -> push through smoke -> wide shot engulfed in smoke -> macro nameplate -> rising through smoke -> shaking light and shadow -> warm/cold alternating scan light -> fall back to freeze frame

1. Wide angle panorama · High angle: A square amber bottle of perfume sits at the center of a pure black background, warm gold side light sweeps over the bottle, white smoke rises slowly from the bottle crevices, the amber liquid shakes slightly, highlighting the heavy and warm texture of agarwood.
2. Close-up · Side low angle: The perfume bottle slowly rotates clockwise 30°, facets reflecting the pure black background and lingering smoke, the golden nameplate illuminated by a spotlight, smoke wrapping the bottle wall as it turns.
3. Medium shot · Eye level: The perfume bottle slowly pushes toward the camera, smoke diffusing and dispersing with the push speed, warm light gradually shifting to deep golden warm tone, lighting forming layered warm halos between smoke and bottle body.
4. Wide shot · Side angle: The perfume bottle is half-wrapped by white smoke, warm gold side light gradually shifts to dusk deep gold tone, amber liquid shakes gently in light and shadow, smoke swaying like ink ripples.
5. Extreme close-up · High angle: Spotlight locks onto the golden nameplate text, smoke flickering and dancing on the lettering, background pure black and smoke completely blurred, highlighting the heavy premium feel of agarwood.
6. Panorama · Low angle: The perfume bottle slowly rises through the gaps of smoke, the warm light above gradually shifts to soft gold, the bottle body refracting a warm luster, lighting shifting from sharp to soft.
7. Medium shot · Side view: The perfume bottle shakes slightly left and right, smoke forming wave-like surges with the shaking, the bottle body facets rapidly switching between light and dark.
8. Close-up · Eye level: The perfume bottle rests at the center of the background, warm gold and cold black lights sweep over the bottle alternately, warm light first highlighting the wood warmth, then cold light highlighting the glass transparency.
9. Wide angle · Side high angle: The perfume bottle slowly falls back to the center of the screen, warm gold soft light wraps the bottle body, smoke gradually dissipating, lighting returning to soft and serene.

Keep overall style consistent. Light and shadow arc: warm gold -> deep gold -> cold black -> warm gold cycle.
Smoke as a visual motif running throughout all panels.
Video Stream: Panorama entry (P1) -> rotate display (P2) -> push through smoke (P3) -> wide shot engulfed (P4) -> macro nameplate (P5) -> rise break (P6) -> shaking rhythm (P7) -> warm/cold alternate (P8) -> fall back freeze (P9).
```

### 4.3 Density Comparison Quick Reference

| Dimension | Medium Density | Low Density (TVC Default) |
|------|--------|--------|
| Narrative Main Line | Recommended (1-sentence journey overview) | **Video Thread** (1-2 sentences of camera language continuity / product state flow) |
| Shot Size Specification | Optional | **Must write**, at the beginning of each grid |
| Driving Force per Grid | Mixed scene + action | Camera instructions |
| Inter-grid Relationship | Theme clue connection | **Visual rhythm driven by video thread** |
| Length per Grid | 2-3 sentences | 2-4 sentences |

### 4.4 Mixed Density in the Same Project

Different grids in a project can use different densities. TVC defaults to all low density.

| Project Type | G1 | G2 | G3 | G4 |
|---------|----|----|----|----|
| **TVC Product Ad** | **Low (Product + Scene Establish)** | **Low (Product Display / Cross)** | **Low (Details + Climax)** | **Low (Ending Freeze Frame)** |
| Brand Story Film | Medium (Character Opening) | Low/Medium (Product Journey) | Low (Product Display) | Low (Ending Freeze Frame) |

---

## V. General Writing Specifications (Shared by All Densities)

### 5.1 Narrative Arc Choreography

Standard rhythm for 9 grids:

| Position | Grids 1-3 | Grids 4-6 | Grids 7-8 | Grid 9 |
|------|-------|-------|-------|-----|
| Function | Establish | Development | Climax | Ending / Resolution |

4-grid narrative: Establish -> Development -> Climax -> Resolution, one grid each.

### 5.2 Light and Shadow Arc

Light and shadow across panels should form a continuous flow of atmosphere: light/dark progression, color temperature drift, with the climax grid featuring the strongest light and shadow contrast. In medium density, light and shadow can be integrated into narrative descriptions, while in low density, they must be explicitly specified for each grid.

### 5.3 Visual Motifs

Design 1-2 visual elements that run throughout all panels. The motif can be: a certain lighting effect, a certain prop, a certain color, or a certain composition method.

---

## VI. Coordination with Phase 4 Asset Images

### Text-to-Image Mode (No Asset Reference)

Write the appearance features of characters/products in Layer 1 (Global Style):

> Protagonist: A young female warrior in black armor, long silver hair, holding a scimitar, with a scar on her right cheek.

### Image-to-Image Mode (Referencing Asset Images)

Use `edit` mode in Nano Banana Pro and upload asset images:
- Layer 1 writes global style normally
- Layer 2 maps asset images: `(Image 1) female warrior character three-view, (Image 2) snow mountain environmental concept`
- Layer 3 grid-by-grid descriptions reference them directly: `The female warrior in Image 1 stands on the summit of the snow mountain in Image 2...`

---

## VII. Planning Strategy for Multiple Grids

Slice the video in units of 15 seconds, with each segment corresponding to a 3x3 grid. **Each grid independently chooses its plot density.**

### Cross-Grid Consistency

- **Global Style**: All grids use the exact same Layer 1
- **Reference Image Mapping**: All grids reference the same set of asset images
- **Transition**: The atmosphere of Grid N's panel 9 ≈ Grid N+1's panel 1 atmosphere
- **Color Continuity**: Color temperature changes across grids remain progressive, with no sudden jumps

---

## VIII. Prompt Template for Splitting Single Frames

When downstream video models do not support multi-grid input, split grid by grid:

```
Separately generate the storyboard image of [Row X, Column Y], maintaining the style and character appearance completely consistent with the original image
```

Use `edit` mode in Nano Banana Pro, uploading the original multi-grid image as the reference image. Split grid by grid in reading order.

---

## IX. TVC-Specific Multi-Grid Writing Styles

TVC commercial multi-grids, based on the general writing style, require additional handling of **interweaving product and brand worlds**, **resolving the End Frame**, and **maintaining product consistency across grids**.

---

### 9.1 Product World Grid Writing

**Positioning**: Low Density (visual-driven), each grid beginning precisely with `[Shot Size · Angle]:`.

**Key Writing Points**:
- Product angles arranged logically: from whole to part, from exterior to interior, from static to functional state
- Unified global lighting system, with only subtle changes in color temperature/intensity
- Restrained background: solid color gradient or pure black
- Material keywords kept consistent

**Complete Example (Action Camera · Product World 9-Grid)**:

```
Generate an image containing 9 storyboard panels, arranged in a 3x3 grid.
With the action camera product of Image 1 as the subject, pure black gradient background, Low-key studio lighting, cinematic product photography texture.

1. Panorama · 3/4 low angle high view: The action camera is suspended at the center of the frame at a classic 3/4 angle, a soft softbox on the left 45° illuminates the front of the body, a rim light on the right outlines a sharp white light border on the edge of the aluminum alloy body, and the glass lens surface reflects a cold white highlight.
2. Medium shot · Side view flat view: Pure side view of the action camera, showing body thickness and side button layout, the matte texture of the button surface clearly distinguishable under side lighting, a long narrow highlight band formed on the chamfered edge of the body waistline.
3. Extreme close-up · Front macro high angle: Extreme macro focusing on the lens surface, multi-layer coated glass presenting purple-blue optical interference colors under side lighting, the metal ring around the lens edge reflecting a circular highlight, extremely shallow depth of field of only millimeter scale.
4. Medium shot · Front view: The camera screen lights up, displaying the POV extreme sports interface—center is the viewfinder screen, the waterproof icon at the top-left emits blue micro-glow, the recording duration numbers at the bottom are visible, and screen light spills over to illuminate the front of the body.
5. Panorama · 3/4 high view: Exploded view of camera components, outer casing separating upwards, lens module rotating and unfolding forwards, waterproof seal ring suspended in the middle layer, motherboard and sensors emitting green micro-glow at the bottom, blue energy lines connecting components.
6. Medium shot · 3/4 front view: The product packaging box is placed on the left side of the frame, tilted 20°, with a silver brand logo on the matte black box face, and the camera body shown on the right side at a Hero Shot angle, box lid slightly open revealing dark gray velvet lining.
7. Extreme close-up · Back macro side light: Extreme macro of the camera back cooling grille, the cross-woven carbon fiber texture clearly distinguishable, each fiber bundle reflecting light at different angles, low-angle side lighting highlighting the texture's light and shadow.
8. Medium shot · Front view: The camera is in night mode, the recording indicator on the front lights up with a dark red pulse light, the screen displays the night vision interface at low brightness, overall environment extremely dark, only product self-glow illuminating local areas.
9. Panorama · Front view: The camera rests stably at the lower-left rule of thirds, soft side light illuminating the product, leaving 40% clean black space at the top-right for post-overlay of Logo and Slogan.

Keep overall style consistent. Lighting system: Low-key dark studio lighting runs throughout all panels.
Visual motif: aluminum alloy brushed texture highlight reflections repeatedly appear in different panels.
```

---

### 9.2 Brand World Grid Writing

**Positioning**: Low Density (TVC default) or Medium Density, with the character using the product in the brand world scene.

**Product Visibility Iron Rules** (must not be violated):
- **The product must be visible in every single panel**—the brand world does not mean a "landscape film without products". The TVC brand world is "the world where the product lives".
- The product occupies 10%-25% of the frame, naturally integrated into the scene but must be distinguishable.
- The product's position in the frame must be explicitly described (`chest-mounted camera`, `camera on left wrist`, `perfume bottle on table`).
- The glow color of the product screen/indicators must be written to enhance recognition.

**Key Writing Points**:
- Under low density: each grid begins precisely with `[Shot Size · Angle]:`, precisely specifying scene, product state, and lighting.
- Under medium density: each grid is described through three elements: **scene environment + character action + product state**.

**Complete Example (Action Camera · Brand World 9-Grid)**:

```
Generate an image containing 9 storyboard panels, arranged in a 3x3 grid.
Real-life shoot, cinematic photography, natural lighting, 16:9 widescreen.

Narrative Line: A sports camera follows an extreme athlete conquering nine extreme environments—
from sky to deep sea, from snow mountain to desert, recording every impossible moment.

1. At ten thousand meters high, the frozen moment of a skydiver jumping out of the cabin, body fully spread in a star shape, the chest-mounted action camera clearly visible, lens pointed down at the earth, recording indicator emitting red micro-glow. Below are white clouds and blue horizon.
2. In the deep sea canyon, a diver descends vertically along a coral cliff, fins kicking up bubbles swirling upwards, the screen of the action camera on the left wrist emitting green micro-glow in the blue underwater light, showing depth stats. Sunlight refracts from water surface into wavy light patterns.
3. At the Alpine ski resort, a skier turns at high speed kicking up an arc-shaped snow wall, body extremely low and tilted, the action camera mounted on top of the helmet capturing POV angle, snow particles twinkling like crushed diamonds in backlight.
4. On a vertical rock wall, a close-up of the moment a climber grips a hold with one hand, knuckles whitening, the action camera on the wrist close to the rock face, lens dusted with fine chalk dust and sweat drops, background of abyss blurred.
5. In the desert goby, the moment an off-road motorcycle leaps over the peak of a sand dune, rider and bike completely airborne, sand spraying from under wheels forming a golden dust tail, the handlebar-mounted action camera illuminated by the setting sun, aluminum alloy body reflecting orange-gold light.
6. In a turbulent canyon, a kayaker traverses white water rapids, water splashing violently in front of the lens, the bow-mounted action camera covered with water droplets, droplets refracting micro-prism effects through sunlight.
7. In a city night scene, the moment a parkour athlete leaps from the edge of a rooftop, below is the neon-flashing city skyline, the chest camera screen light reflecting and echoing with the city lights.
8. On a blizzard mountain ridge, a climber trudges through whiteout storm, ice crystals hitting the visor, the action camera held in glove still recording, indicator stubbornly flashing red in the snowstorm.
9. At a sunrise mountain peak, the athlete stands on the summit looking back at the path, golden morning light pouring from behind, lifting the action camera toward the sunrise, screen reflecting the entire golden sky.

Keep overall style consistent. Visual motif: the red recording indicator of the product stubbornly lights up in every extreme environment.
Color tone arc: gradually transitioning from cold blue high sky in Panel 1 to warm golden sunrise in Panel 9.
```

---

### 9.3 Cross-Grid Writing

**Positioning**: Mixing "brand world" and "product world" panels in the same Grid, simulating the TVC cross-cutting rhythm.

**Key Writing Points**:
- Odd-numbered grids (1/3/5/7) are brand world scenes—high/medium density, character using the product
- Even-numbered grids (2/4/6/8) are product world close-ups—low density, precise camera instructions
- Grid 9 is fixed as the End Frame
- Neighboring grids designed with visual transitions (shape match / color match / texture match)

**Complete Example (Action Camera · Cross 9-Grid)**:

```
Generate an image containing 9 storyboard panels, arranged in a 3x3 grid.
Cinematic photography, 16:9 widescreen.
Brand world panels are real-life shoot natural light, product world panels are Low-key studio light with pure black background.

(Image 1) Action camera product reference image.
Brand world and product world crosscut, odd-numbered panels are usage scenes, even-numbered panels are product close-ups, panel 9 is ending freeze-frame.

1. Ski resort backlight, frozen moment of a skier high-speed carving turn, snow mist swirling like a white wave wall, the action camera on the helmet flashing in sunlight.
2. Close-up · 3/4 side view: Pure black background, close-up of the chamfered edge of Image 1 action camera body, side lighting outlining a smooth surface similar to the snow wave wall, aluminum alloy brushed texture reflecting cold white highlights.
3. Over the sea, moment of a diver backflipping into the water, body curled, splashing out a circular water crown around, the waist-mounted action camera about to submerge.
4. Extreme close-up · Front view: Pure black background, front view of action camera lens, circular lens outline centered, multi-layer coating reflecting blue-purple optical colors similar to seawater, water droplets remaining on lens edge.
5. Desert dusk, silhouette of an off-road bike leaping over a sand dune, behind is a burning orange-gold sunset, the handlebar-mounted action camera gilded by the setting sun.
6. Medium shot · Side view flat view: Pure black background, warm gold side light sweeps over the product aluminum alloy body from the left, presenting the same amber gold tone as the desert dusk, highlights on the material texture flowing slowly.
7. Vertical rock wall, extreme close-up of climber's fingertips gripping rough rock, knuckles whitening, the action camera on the wrist close to the rock face, background is deep abyss blur.
8. Extreme close-up · Front macro: Pure black background, extreme macro of the product's side non-slip rubber grip area, the diamond embossed texture having a rough texture similar to the rock surface, low-angle side lighting sculpting each raised highlight and groove shadow.
9. Panorama · Front view: Pure black gradient background, the action camera rests at its best angle at the lower-left rule of thirds, soft side light illuminating the product, large area blank space at the top-right for Logo and Slogan overlay.

Keep overall style consistent. Odd panels maintain real-life natural light texture, even panels maintain Low-key studio product photography texture.
The two worlds are connected through visual matches of shape/color/texture.
```

---

### 9.4 End Frame Grid

**General Principle**: Layout depends on brand guidelines—both **product centered** (Hero Pose) and **product offset with blank space** are valid schemes.

**Core Rules**:
1. Composition must reserve space for post-production text overlay (approx. 30%-40% clean area)
2. Product state must be the "final state": screen lit, exterior intact, posture stable and serene
3. Lighting clean and premium; do not write Logo/Slogan text content in the prompt, only describe the blank area

**End Frame Grid Prompt Template**:

```
[Grid Number]. [Shot Size] · [Angle]: [Background Description], [Product Name] resting at [Position] of the frame in [angle/posture], [Product Final State Description]. [Clean Lighting]. [Blank Area Location] leaves [Percentage] of clean space in the frame, background gradient uniform with no clutter.
```

**Example**:

```
9. Panorama · Front view: Dark gray gradient background, the action camera rests at a 3/4 low angle at the lower-left rule of thirds, the screen displaying the brand primary blue interface, all indicators glowing slightly. Soft side light from the left illuminates the product, creating a naturally transitioning shadow on the right. A clean space occupying 40% of the screen is left at the top-right, background gradient uniform with no clutter.
```

---

### 9.5 TVC Multi-Grid Planning Example

The following example shows how a 30-second TVC (Action Camera) uses 2 grids to cover the complete content.

**Project Info**:

| Dimension | Content |
|------|------|
| Product | Professional Action Camera |
| Duration | 30 seconds |
| Narrative Model | Brand World Crosscut (Model C) |

**Grid Planning Table**:

| Grid | Timeframe | Type | Plot Density | Narrative Function |
|------|------|------|---------|---------|
| G1 | 0-15s | Brand World Grid | Low Density | Extreme sports scene montage |
| G2 | 15-30s | Product World Grid + End Frame | Low Density | Product multi-angle studio display + Resolution |

**Cross-Grid Consistency Checklist**:

- [ ] **Global Style**: G1 and G2 use the same quality anchors
- [ ] **Reference Image**: Both grids reference the same product reference image (`Image 1`)
- [ ] **Transition**: G1 panel 9 tone -> G2 panel 1 tone, color temperature continuous
- [ ] **Product Description**: Product material keywords in both grids are completely identical
- [ ] **Product Color**: Product color scheme descriptions are identical in all panels
- [ ] **Presenter Clothing**: Presenter clothing descriptions are identical in all panels

---

### 9.6 Product Consistency Maintenance

Maintaining product appearance consistency across grids in TVC multi-grids is critical.

#### Rule 1: Lock in Product Description Template

```
Standard Product Description Template:
[Product Name], [Core Material A] + [Core Material B] body, [Color / Color Scheme], [Key Design Feature 1], [Key Design Feature 2], [Size / Proportion Feature].
```

Example:
```
Standard Product Description:
XX Pro Action Camera, aluminum alloy brushed body + carbon fiber back shell, space gray color scheme, front ultra-wide-angle lens module (circular, multi-layer coated), three red function buttons on the side, body square and robust, palm-sized.
```

#### Rule 2: Unified Light and Shadow Keywords

The same product in product world panels across different Grids should use the same set of lighting vocabulary (key light direction, rim light direction, material highlight descriptions, and color temperature baseline globally consistent).

#### Rule 3: Angle Description Standardization

The same angle across different grids must use the exact same angle description text; do not write `slightly high` in G1 and `30° above angle` in G2.

#### Rule 4: Minimum Product Description Requirements in Brand Worlds

Even if the product occupies only 10% of the frame, it must still include four information points: product mounting location, material keywords, functional state cues, and product color scheme.

#### Rule 5: Global Reference of Product Reference Images

All grids must reference the same product asset image; do not use different product reference images.

#### Rule 6: Presenter Clothing Consistency

When a character appears in brand world panels (whether full-body/lower-body/back view/silhouette), the clothing description of this character must be completely consistent across all grids. The **presenter standard description** established during Pre-production is the sole authority—it must be reused in every grid involving the character; do not write "black shorts" in G1 and "black pants" in G2. The style, color, and material of the clothing must not change across grids; only postures and actions are allowed to change.

#### Rule 7: Figurative Language Prohibited

**Using metaphors, personifications, analogies, and other figures of speech in multi-grid prompts is prohibited.** AI image models interpret literally—"like a sculpture" will generate plaster/marble texture bodies, "like a garden" will generate floral plants, and "like silk" will change material rendering.

| Incorrect Writing | Issue | Correct Writing |
|---------|------|---------|
| Passersby frozen like **sculptures** | Model might generate plaster/marble texture bodies | Passersby keep walking posture still, expressions frozen, clothing corners suspended in motion |
| Walking among papers like **plucking flowers** | Model might generate floral elements | Plucking suspended papers from the air one by one |
| Droplets like **amber beads** | Model might render droplets as amber-colored solids | Droplets appear translucent and dark under lighting, surface reflecting highlights |

Principle: **Describe what you want, not what it looks like.**

#### Rule 8: Multi-Grids Only Write States, Not Processes

Multi-grids are static keyframes; each grid can only describe the **visual state at one point in time**, not a dynamic process. Verbs must be static (suspended, still, resting, frozen) rather than process-oriented (flying out, pouring out, splashing, falling). Process-oriented actions are left for video prompts.

| Incorrect Writing (Process State) | Issue | Correct Writing (Final State) |
|----------------|------|----------------|
| Coffee cup **flying out of hand**, liquid **beginning to spill** from cup mouth | "Flying out" and "spilling" are dynamic processes, static frames cannot express | Coffee cup suspended in mid-air, liquid solidified into an arc, cup mouth facing down |
| Red wine **beginning to pour** from cup mouth, forming an arc **about to spill** | "Pouring" and "spilling" are ongoing actions | Red wine liquid column suspended between tilted glass and tabletop, liquid surface reflecting candlelight |
| Papers **fluttering** in the air | "Fluttering" is dynamic | Dozens of papers suspended in the air at various angles |

This rule is complementary to "Division of Labor for Dynamic Special Effects": the division of labor handles "what to write", while this rule handles "how to write".

---

## Part 2: Video Prompt Syntax

---

## I. Video Prompts vs. Static Keyframe Prompts

Core transition mindset: converting "what it is" into "how it changes".

| Dimension | Static Keyframe | Video Prompt |
|------|-----------|-----------|
| Time | None | Has time code, precise to seconds |
| Subject | Frozen state/posture | Process in motion (action + change) |
| Camera | Fixed shot size + angle | Camera movement trajectory (push/pull/orbit/follow) |
| Transition | None | Transition instructions (hard cut / dissolve / match cut) |
| Lighting | Fixed light source direction | Light and shadow variations over time (gradient / flicker / day-night) |

---

## II. Video Prompt Writing Logic & Output Format

Video prompts follow a three-part logic, using natural language.

### Section 1: Style & Constraints Statement

**Must cover**: visual style, color tone, constraints, **"no background music" (required)**, and **product@product_multiview_image**.

> **Video Model Dual-Image Input**: The video model receives two images—the multi-grid storyboard image (first frame) + the product multi-view image (product anchor). At the end of the style statement in the video prompt, use `Ad for product@product_multiview_image` to reference the product multi-view, letting the model understand the product's appearance. The `(Image 1)(Image 2)` reference image mapping is the syntax for the image generation stage (multi-grid prompts) and is not used for video prompts.

> **Audio Iron Rule**: Video models generate BGM by default; it will appear if not explicitly written. In multi-segment splicing, the BGM breaks at the joints. BGM is laid down uniformly as a separate audio track in post-production. Character dialogue is marked with quotes in the shot description.

> **Do Not Write Post-Production Instructions**: Video prompts only describe visual content that the video model can generate. The following belong to post-production and are not written in video prompts: Logo/brand mark overlays, Slogan/text fades, color grading instructions, sound effect design, and subtitle typography. The End Frame in video prompts only needs to describe pure visual states such as "product centered and frozen, frame clean with blank space"; space reservation for Logo and Slogan belongs to the multi-grid image prompt (End Frame panel).

**Output Example**:
> Style: Dark fairy tale farewell scene / Red and black high-contrast forest colors / Stop-motion texture / Strong light source opposing composition (white light inside door vs. crimson forest outside door) / Exquisite facial expression close-up / Emotionally restrained farewell atmosphere / No subtitles / No background music. Ad for product@product_multiview_image.

### Section 2: Shot Script

Choose one of two formats based on the target video model:

#### Format A: Simplified Shot List

```
Shot 1 [0-2s] [Medium shot] A huge tree door embedded in a thick tree trunk, surrounded by a red forest. A little girl and a small mouse stand side by side in front of the door, the girl lowering her head slightly, the mouse looking up at her.
Shot 2 [2-4s] [Close-up] The small mouse lifts its paw to wave, saying "squeak squeak squeak" in a soft farewell, the girl looks at it, her expression warm and reluctant.
Shot 3 [4-7s] [Medium shot] The girl slowly turns to walk toward the tree door, reaching out to push it. Strong white light pours from the door crack, outlining her silhouette. She takes two steps out and stops, turning back to look at the mouse.
...
```

#### Format B: Detailed Segmented Descriptions

```
【0-3s: Mountain Source, Grape Rolling】
Camera: Camera slowly pushes forward from a wide shot, then cuts to a macro tracking shot.
Visuals: The overall visual tone is a black-and-white minimalist mountain wilderness, a hand-drawn line-art young girl carrying a bamboo basket walks into the frame with a shovel. As she steps onto a rock, the basket tilts, and several fruits outlined in lines roll out.

【4-7s: Pink Pouring, Fruit Aroma Awakening】
Camera: Camera shoots up from a low angle, then pans down rapidly following the path of the water flow.
Visuals: A huge realistic transparent cup body stands on the rocks in the mountains, the cup bottom already filled with fresh green grapes. Suddenly, a stream of pink peach juice with realistic luster pours down from above like a waterfall...
```

### Section 3: Transitions & Continuity (Natural Integration)

Two processing methods:

1. **Integrated into Shot Descriptions**: Naturally mention transitions and continuous elements in each shot description
   > Shot 1 [0-2.5s] [Wide shot · Backlight] (corresponding to P1) **Dissolve transition from previous segment.** Fixed camera, three cows in silhouette slowly walking to the right in golden morning light...

2. **Append Notes at the End** (only when information density is high):
   > All clips are mainly hard cuts, with dissolves used to establish shots. Golden rim light consistently outlines the edges of cows in each shot. The G9 warm golden pasture panorama naturally transitions to the next segment.

---

## III. Shot-by-Shot Description Formula

### Seven-Element Formula

```
[Time Code] [Shot Size + Angle] + [Camera Movement] + [Subject Motion] + [Environment/Lighting Variation] + [Character Dialogue (if any)] + [Transition Instruction]
```

### Writing Points

- **Verbs are King**: The core of video prompts is verbs—sweep, rise, rotate, push, diffuse, dissipate.
- **Gradual Over Sudden**: Use "gradually", "slowly", and "progressively" to describe transition processes.
- **Specific Over Vague**: `rotate 30°` is better than `slowly rotate`.
- **Causality Chain**: Camera movement triggers subject changes, and subject changes affect lighting reactions.
  - Example: `product pushes toward camera` -> `smoke diffuses with push speed` -> `warm light gradually shifts to deep gold`.

---

## IV. 15-Second Standard Rhythm Choreography

### Four-Stage Rhythm Model

| Stage | Duration | Function | Rhythm |
|------|------|------|------|
| **Establish** | 0-3s | Setting scene/atmosphere | Slow |
| **Development** | 3-7s | Narrative unfolding / display | Medium speed |
| **Climax** | 7-12s | Emotion/action peak | Fast |
| **Resolution** | 12-15s | Blank space / resolution / CTA | Decelerating |

### Non-standard Rhythms

| Variant | Structure | Applicable |
|------|------|------|
| **Slow Build-up** | 5s establish + 5s development + 3s climax + 2s resolution | Atmospheric clips, art films |
| **Impact Type** | 1s establish + 4s development + 8s climax + 2s resolution | Action films, game CG |
| **Cyclic Type** | establish -> climax -> establish -> climax -> resolution | Music MVs, rhythm-driven |
| **Flashback Type** | climax -> flashback development -> return to climax -> resolution | Suspense, twist narratives |

---

## V. Reference Specifications with Multi-grids

Video prompts can reference panel positions in the multi-grid directly:
- By panel number: `(corresponding to storyboard P1)`, `(corresponding to P5-P7)`
- By row and column position: `(corresponding to Row 2, Column 3)`

Reference Example:

```
Shot 1 [0-2s] [Panorama · High angle] (corresponding to P1) Product rests at the center of the frame, warm gold side light slowly sweeping...
Shot 2 [2-4s] [Close-up · Side low angle] (corresponding to P2) Product slowly rotates, facets reflecting changing light and shadow...
```

Multi-panel corresponding to a single shot:
```
Shot 3 [4-8s] [Medium shot · Eye level] (P3 -> P4 transition) Product pushes toward the camera, scene gradually transitioning from P3 state to P4...
```

---

## VI. Cross-segment Continuity of Multi-segment Videos

### Cross-segment Consistency Elements

| Element | Requirement |
|------|------|
| **Style Statement** | All segments share identical style and constraints statements |
| **No Background Music** | Must be written in every segment |
| **Character Appearance** | Maintained consistent by referencing the same asset image |
| **Tone Continuity** | Previous segment end tone ≈ next segment start tone |
| **Motion Continuity** | Character motion direction does not jump abruptly between segments |

### Segment Independence

Each video prompt segment is fed into the video model independently; the model does not know the content of other segments. The Phase numbering of each segment starts from Phase 1, and seconds start from 0s, without inheriting numbering or timelines from previous segments. Do not reference events that have already occurred in other segments in the current description (e.g., "returning to the previous balcony", "everything as before", "more soft mist compared to the previous segment"). Cross-segment consistency is achieved by repeating identical style statements and product descriptions, not through text referencing.

### Segment Transition Types

Transition types describe the **editing level** visual transition strategy (used to guide post-production splicing), not referencing other segments in text:

| Transition Type | Applicable |
|---------|------|
| **Action Continuity** | Continuous narratives |
| **Atmospheric Continuity** | Emotional clips |
| **Scene Jump** (fade to black / fade to light) | Multi-scene narratives |
| **Call-back Echo** | Cyclic/elevated narratives |

---

## Part 3: Cinematic Product Breakdown

---

### I. Video Prompt Structure

TVC product videos use a multi-phase structure.

#### Standard Phase Structure

```
Phase [Number] ([Start]s-[End]s): [Phase Name]
├─ Camera Movement: [Camera movement method + speed + direction]
├─ Product State: [Current product morphology/dynamic change]
├─ Feature Reveal: [Core selling point displayed in this stage]
├─ Lighting Design: [Light source type + direction + variation]
├─ Material Focus: [Material/texture highlighted in the current stage]
└─ Visual Effects: [Particles/energy flow/digital overlays, etc.]
```

#### Rhythm Choreography Principles

| Stage Type | Typical Duration | Rhythm | Function |
|---------|---------|------|------|
| Suspense Opening | 1-2s | Extremely slow / still | Building anticipation, hinting at product silhouette |
| Disassembly / Unfolding | 2-3s | Slow -> accelerating | Displaying internal structure, conveying tech depth |
| Feature Activation | 1-2s | Explosive | Screen lighting up, digits ticking, sensors glowing |
| Explosive Rotation | 1-2s | Fast | 360° all-round display of product appearance |
| Macro Dive | 1-2s | Super slow | Material texture resolution, establishing premium feel |
| Brand Freeze-frame | 1-1.5s | Still | Logo + Slogan + product final posture |

#### Format Points

- **Style statement** ends with "no background music"
- **Phase numbers** increase from 1, with precise seconds marked in parentheses
- **Seconds continuous**: previous Phase end second = next Phase start second, no gaps or overlaps

---

## II. Component Disassembly/Assembly Animation Choreography

#### 1. Suspended Disassembly

```
Product suspended at the center of the frame, components slowly separating—the outer shell hovering and drifting to the top-left, the lens module separating and rotating to the right, the motherboard suspended and unfolding downwards, and the battery pack sliding out to the back. Faint blue energy lines connect all parts, implying internal synergy. Background pure black, component surfaces outlined by precise side lighting.
```

#### 2. Exploded View

```
Product explodes and expands instantly, all components ejecting along the central axis to their positions—Top: lens component suspended and rotating, glass lens refracting iridescent spots; Middle: motherboard and chipsets expanding horizontally, circuit textures emitting green micro-pulse light; Bottom: battery module and cooling system sinking vertically, metal cooling fins reflecting sharp silver highlights. Overall symmetrical exploded view, strong industrial design feel.
```

#### 3. Precision Assembly Snap-back

```
Components snap back at high speed—cooling module home first with a metal collision micro-vibration; motherboard sliding precisely into slot, circuits immediately lighting up with pulse lights; lens module rotating and screwing in, glass surface flashing a highlight; outer casing locking final, a white light flash along the seam, product returning to complete form with surface reflecting like new.
```

**Rhythm Points**: disassembly takes 2-3 seconds (slow), assembly snap-back takes 0.8-1.2 seconds (fast), speed contrast creates impact.

---

## III. Feature Visualization Design

#### 1. Screen Activation

```
Product screen starts from completely black, a pixel lights up from the center, light diffusing outwards in a wave pattern, screen content gradually emerging—interface elements appearing in sequence, icons sliding in from below, screen light illuminating the front of the product and surrounding environment, casting a colored screen reflection on the tabletop.
```

#### 2. Digits Ticking

```
Frame focuses on the product screen, digits ticking at high speed—numbers next to the battery icon rising rapidly from 00:00:00, numbers rolling like an old flip-clock, each digit with faint motion blur, finally freezing at 04:00:00, digits emitting pulsating golden light, implying ultra-long battery life. The entire process completes in 1.5 seconds.
```

#### 3. Sensor Glow

```
Sensors on the product surface emit faint glow—infrared sensor lighting up with a dark red pulse, lidar emitting a green scanning line, multiple sensors activated in sequence, light points breathing, implying the product is sensing surroundings. Light forms colored reflections on the metal surfaces.
```

#### 4. Energy Flow

```
A blue energy line injected from the charging port, flowing rapidly along the circuit board textures inside the product, branching, converging, and branching again, illuminating chips and components along the way, finally gathering at the battery module, the battery icon transitioning from red to full grid green, emitting a circle of diffusing energy pulse waves.
```

---

## IV. Material Macro System

#### Material Macro Quick Reference

| Material Type | Macro Description Keywords | Lighting Match |
|---------|-------------|---------|
| Brushed Metal | Dense parallel brushed textures, each scratch reflecting light at different angles | Side light sweeps slowly at 45° |
| Glass Refraction | Light penetrating to form rainbow dispersion, micro-prism effects at edges | Backlighting / penetrating light |
| Carbon Fiber Weave | Cross-woven forming regular diamond patterns | Low-angle side lighting |
| Liquid Fluid | Viscous liquid flowing slowly, liquid surface reflecting like a mirror | Top lighting + environmental reflections |
| Ceramic Glaze | Jade-like warm sheen, micro-bubbles shimmering under the glaze layer | Soft light scattering |
| Leather Texture | Pores, creases, and usage marks, manual stitching at edges | Warm side lighting |
| Anodized Aluminum | Fine matte texture, subtle color shifts at different angles | Gradient light sweeping |

#### Material Macro Camera Movement

```
Camera close to the product surface to extreme macro (simulating macro lens 1:1 magnification), sliding slowly along the material texture direction, extremely shallow depth of field of only millimeter scale focal plane, focus moving with the slide, revealing different layers of material details in sequence—from brushed texture to chamfer highlights to seam precision, finally camera pulling back slowly, material details gradually gathering into the complete outline of the product.
```

---

## V. Six-Stage Rhythm Model

Pure product display TVC standard rhythm:

```
Ultra-slow Reveal → Suspended Disassembly → Precision Closure → Feature Activation → Macro Dive → Brand Freeze-frame
```

| Stage | Rhythm | Camera Movement | Product State |
|------|------|------|---------|
| **Ultra-slow Reveal** | Extremely slow / still | Fixed -> micro push | Outlined by rim light step-by-step in pure black |
| **Suspended Disassembly** | Slow -> gradually faster | Arc orbit | Components separating, interior exposed |
| **Precision Closure** | Explosive | Multi-angle quick cuts | Components snapping back at high speed |
| **Feature Activation** | Medium speed pulse | Push close to close-up | Screen lighting up / sensors glowing |
| **Macro Dive** | Ultra-slow | Macro sliding | Material micro details magnified |
| **Brand Freeze-frame** | Still | Eject pull back -> freeze | Product perfect form + Logo |

#### Stage Transitions

- Ultra-slow Reveal -> Suspended Disassembly: After the rim light illuminates the whole view, components "breathe" micro-vibrate -> separate.
- Suspended Disassembly -> Precision Closure: Components hover for 0.3s still -> sudden acceleration snap-back.
- Precision Closure -> Feature Activation: White light flash at the snap-back moment -> screen diffusing and lighting up from the light point.
- Feature Activation -> Macro Dive: Screen pixels -> camera lens penetrating -> entering material micro world.
- Macro Dive -> Brand Freeze-frame: Material texture gradually blurring -> eject pulling back to panorama.

---

## VI. Complete Multi-Phase Product Video Examples

#### Example 1: Action Camera (10s, 5 Phases)

**Product**: High-end action camera, waterproof, ultra-wide-angle, ultra-strong stabilization

```
Phase 1 (0s-2s): Dark Suspense Reveal
Camera Movement: Still -> micro push
Product State: Pure black background, a sharp rim light lights up from the product edge, slowly outlining the square silhouette of the action camera.
Lighting Design: Rim Light wraps 270° from the rear, front almost completely black, only outline visible.
Material Focus: When the rim light sweeps, brushed texture of the aluminum alloy body is faintly visible.

Phase 2 (2s-4s): Suspended Disassembly
Camera Movement: Arc orbit, from front to 3/4 high view
Product State: Camera components begin to suspend and separate—waterproof case drifting upwards, revealing internal precision structure; ultra-wide-angle lens module rotating and separating forwards, multi-layer coated glass refracting iridescent spots; stabilization gyroscope module suspended and rotating. Blue energy lines connect components.
Lighting Design: Side light gradually rises, precisely illuminating each separated component.
Feature Reveal: Multi-layer coated structure of the ultra-wide-angle lens, mechanical stabilization gyroscope module.

Phase 3 (4s-5.5s): Feature Activation
Camera Movement: Rapid push to screen close-up
Product State: Components snap back and assemble at high speed (0.5s), outer case locking with a white light flash; rear screen immediately lights up, interface displaying POV extreme sports footage (skydiving first-person perspective), waterproof icon at the screen top-left glowing blue.
Lighting Design: Screen light becomes primary light source, illuminating the front of the product and surroundings.
Feature Reveal: Screen display effect, waterproof performance hint.

Phase 4 (5.5s-7.5s): Explosive Rotation
Camera Movement: High-speed 360° orbit rotation
Product State: Camera suspended at the center of the frame, rotating at high speed to display all aspects—front lens, side buttons, bottom tripod mount, top recording button. Each face illuminated by a spotlight in sequence.
Lighting Design: Spotlight rotates, highlights always locked on key features rotating past.
Material Focus: Contrast between brushed aluminum texture and non-slip rubber grip area clearly visible in rotation.

Phase 5 (7.5s-10s): Macro Dive + Brand Freeze-frame
Camera Movement: Rapid push to lens glass surface -> penetrate lens group -> eject pull back to panorama
Product State: Lens dives into the camera lens interior, traversing multi-layer coated glass (light refracting and dispersing between lenses), traversing CMOS sensor surface (microscopic pixel array macro), ejecting and pulling back to panorama—product suspended at the center, brand Logo and Slogan emerging below.
Lighting Design: Light refracts inside during penetration; returns to Low-key studio lighting upon ejection.
Material Focus: Optical dispersion of lens coatings, microscopic pixel array of CMOS sensor.
```

#### Example 2: Luxury Essence Serum (10s, 5 Phases)

**Product**: High-end skincare essence serum, gold ingredients, luxury texture, anti-aging repair

```
Phase 1 (0s-2s): Luxury Veil Reveal
Camera Movement: Slow pan down
Product State: At the top of the frame, a drop of golden essence slowly falls in a pure black background, the droplet surface reflecting the entire environment, liquid viscous and plump, with a honey-like stretch texture. The falling path of the droplet leaves a golden light trace.
Lighting Design: Single spotlight from top tracks the droplet, droplet like a miniature golden planet.
Material Focus: Viscosity, surface tension, and luster refraction of the essence.

Phase 2 (2s-4s): Bottle Emergence
Camera Movement: Arc orbit, from side to 3/4 front view
Product State: Golden droplet falls into the essence bottle mouth below, ripples spreading; camera pans down to reveal the entire bottle—matte glass bottle body, golden liquid inside flowing slightly, metal cap reflecting sharp highlights, bottle face embossed with brand pattern.
Lighting Design: Side lighting from the left 45°, glass bottle creating translucent light and shadow layers, warm amber glow refracted inside the liquid.
Material Focus: Translucent texture of matte glass, mirror reflection of the metal cap.

Phase 3 (4s-6s): Liquid Flow Macro
Camera Movement: Extreme macro push into bottle glass surface
Product State: Camera close to bottle body, penetrating matte glass layer, entering the bottle's liquid world—golden essence with tiny gold foil particles suspended and flowing, liquid forming a slow convection vortex, gold foil shimmering in the light.
Lighting Design: Backlight penetrates the liquid, gold foil particles like floating stars.
Feature Reveal: Visualization of active gold foil micro-particles.

Phase 4 (6s-8s): Skin Metaphor
Camera Movement: Constant speed side shift + shallow focus transition
Product State: Frame transitions to abstract skin macro metaphor—smooth skin texture surface, a drop of essence falls on skin, rapidly absorbing and diffusing, diffusion path emitting faint golden light, skin texture becoming finer and smoother (visual metaphor: anti-aging repair).
Lighting Design: Soft warm scattered light, SSS subsurface scattering effect on skin surface.
Feature Reveal: Visualization of penetration absorption and skin repair effects.

Phase 5 (8s-10s): Brand Freeze-frame
Camera Movement: Slow pull back to medium shot freeze
Product State: Product bottle placed center-right, a branch of dried flower/golden leaf on the left as foreground decoration, bottle body illuminated by warm side light, background dark gradient (dark brown -> black). Brand Logo elegantly emerges on the left, Slogan arranged in thin serif font below.
Lighting Design: Classic beauty ad lighting—soft key light + side rim light + bottom reflection light.
```

#### Example 3: Avant-garde Silver Bracelet (10s, 5 Phases)

**Product**: Hand-forged silver bracelet, independent attitude, craft texture, avant-garde design
**Presenter Strategy**: Hand/wrist close-up of a female (no face shown), wearing minimalist black clothing, skin clean

```
Phase 1 (0s-2s): Craft Source—Forging
Camera Movement: Macro still -> slow push
Product State: Pure black background, a rough silver block at the center. Side lighting slowly rises, outlining the hammered texture on the silver block surface. Edges of the silver block begin to glow with faint hot red light—implying just taken out of the forge. Surface showing irregular dents left by hand-hammering, each mark the artisan's signature.
Lighting Design: Single side hard light, emphasizing silver block's rough texture. Faint red light penetrating upwards from bottom.
Material Focus: Graininess of raw silver, irregular texture of hammered dents.

Phase 2 (2s-4s): Transformation—From Raw Silver to Finished Product
Camera Movement: Fast push -> dissolve transition
Product State: Camera rapidly pushes to silver block surface macro—silver particles filling the screen; dissolve transition to finished bracelet macro close-up: same silver color, but surface polished to a matte brushed texture, joint structures between links casting precise shadows under side lighting.
Lighting Design: Light source direction consistent before and after transition (side light), achieving material change but continuous lighting.
Material Focus: Matte brushed silver surface, precise gaps at link joints.

Phase 3 (4s-6s): Wear—Wrist Appearance
Camera Movement: Slow pull back -> micro arc shift
Product State: Camera slowly pulls back from bracelet macro, silver chain gradually fully revealed—wrapped around a female wrist. Wrist slowly turns, silver chain flowing with the gesture, subtle metallic collision sparks generated between links. Wrist skin clean, nails colorless, black clothing sleeve edge just exposing wrist.
Lighting Design: Side lighting from one side of the wrist, silver chain reflecting a flowing light band, skin presenting warm ivory tone.
Material Focus: Touch contrast between silver and skin—cold hard metal and warm skin.

Phase 4 (6s-8s): Posture—Avant-garde Attitude
Camera Movement: Tracking hand motion
Product State: Hand slowly raises from the bottom, fingers slightly open in a relaxed posture—silver chain hanging naturally on the wrist under gravity, one side snug to skin, other side naturally suspended. Hand slightly fists then relaxes, silver chain generating slight displacement and lighting changes. Background transitions from pure black to blurred concrete gray—implying architectural aesthetic space.
Lighting Design: Side lighting primary tone unchanged, faint environmental scattered light in background.
Dynamic Focus: Natural drape and lighting flow of the silver chain with hand gestures.

Phase 5 (8s-10s): Freeze Frame
Camera Movement: Slow push back to macro -> still
Product State: Wrist still center-left, silver chain draping naturally at the narrowest part of the wrist. Camera pushes to silver chain close-up—finally freezing on the macro of a single link: matte brushed surface, precise gaps at joints, silver outline sculpted by side lighting. Large area blank space on the right of the screen for brand logo.
Lighting Design: Returning to single side hard light at the opening, echoing start and end. Clean, restrained, ample blank space.
```

---

## Part 4: Brand World Shots

---

### I. Brand World ↔ Product World Transition Techniques

The brand world is the usage scene of the product; the product world is the studio close-up. The two worlds switch repeatedly in TVC, and the quality of the switch determines the premium feel of the ad.

#### Three Core Transition Techniques

##### Technique 1: Match Cut Motion Transfer

**Brand World → Product World**:

```
[Brand World] Skier flies off snow slope, body rotating in air—
At the moment of rotating 180°, seamless transition to—
[Product World] Product appears in a pure black background at the same angular velocity, continuing the rotation motion to complete a 360° display, decelerating to freeze at 3/4 side view.
```

**Product World → Brand World**:

```
[Product World] Product screen lights up, light diffusing outwards—
At the moment light fills the entire screen, seamless transition to—
[Brand World] From white overexposure, wide snow mountain panorama gradually emerges, an off-road vehicle racing on snow, kicked-up snow mist seamlessly connecting with the white screen light.
```

**Prompt Template**:
```
[Motion subject of former world] performing [specific motion] in the frame—
At the moment of [motion reaching specific position/angle/speed], seamless transition to—
[Latter world] continuing the motion with same [motion direction/angular velocity/velocity vector], [subsequent visual unfolding]. The [shape/motion trajectory/speed] of the two frames connect perfectly, camera flowing smoothly.
```

##### Technique 2: Scale Shift

**Macro → Micro**:

```
[Brand World] Aerial view of city night scene, thousands of lights twinkling—
Camera rapidly dives toward a glowing point in the city—
[Product World] After traversing layers of scale, the glowing point becomes a pixel on the product screen, camera stabilizing on the product screen macro, interface details clearly visible.
```

**Micro → Macro**:

```
[Product World] Camera close to product surface macro, material texture filling the frame—
Camera suddenly ejects back, rapidly pulling away—
[Brand World] Product texture transitions to high-altitude ground texture (desert cracks/agricultural geometry), revealing the product is in the middle of vast natural landscapes.
```

##### Technique 3: Medium Penetration

**Penetrate into Product → Emerge into Brand World**:

```
[Product World] Camera aligned with lens group front, slowly pushing in—
Traversing first layer coated glass (iridescent dispersion on surface),
Traversing second layer lens (light refracting and bending),
Traversing CMOS sensor array (microscopic pixel grid)——
[Brand World] Emerging to reveal a magnificent landscape shot from the camera's perspective, implying "the world through the product's eyes".
```

**Brand World → Penetrate into Product**:

```
[Brand World] Essence serum slowly drops at fingertip—
At the moment droplet falls into bottle mouth, camera follows droplet penetrating bottle—
[Product World] Entering bottle liquid micro world, gold foil particles suspended and flowing like stars in amber liquid.
```

#### Transition Frequency & Rhythm Control

| Video Duration | Recommended Transitions | Rhythm Strategy |
|---------|------------|---------|
| 10s | 1-2 times | Brand world opening -> product world resolution |
| 15s | 2-3 times | Brand -> product -> brand -> freeze frame |
| 30s | 4-6 times | Free crosscut, brand-dominant first half, product-dominant second half |

**Transition Rhythm Principles**:
- Remain in each world for at least 2-3s after transitioning before switching back.
- The final transition must be **into the product world**—the TVC final resolution is always the product itself.

---

## Part 5: TVC Duration Templates

---

### I. TVC 30s Dual-segment Rhythm Templates

#### Template A: Brand World Crosscut 30s

```
═══ Segment 1 (0-15s): Brand World Dominant, Establishing Emotion ═══

Phase 1 (0-3s): Brand World Opening
  Wide shot of extreme sports / lifestyle scene, establishing world view and energy. Fast-paced camera movement (aerial/tracking/handheld), subject in motion.

Phase 2 (3-6s): Product Debut
  [Match Cut] Scene motion -> product rotation. Product slowly orbits and displays at a 3/4 angle, rim light outlining styling. First reveal of product full view.

Phase 3 (6-10s): Brand World Upgrade
  [Match Cut] Product material texture -> scene element texture. Scene upgraded (more extreme/dynamic/emotional), product appearing naturally in use (handheld/worn/environment integrated).

Phase 4 (10-15s): Feature Reveal + Segment Transition
  [Match Cut] Scene action -> product feature activation. Feature visualization display, screen lighting up / sensors glowing. End action reserves transition point for next segment (not resolving in rotation/diffusion).

═══ Segment 2 (15-30s): Product Dominant, Resolving Brand ═══

Phase 5 (15-19s): Inheritance + Deep Disassembly
  Inheriting previous segment end motion. Product suspended disassembly, components separating to display internal structure, conveying tech depth.

Phase 6 (19-23s): Precision Closure + Explosive Rotation
  Components snap back -> explosive 360° rotation display. Speed from extremely fast (closure) to fast (rotation) to decelerating.

Phase 7 (23-27s): Macro Dive
  Camera dives into product surface macro—material textures, chamfer highlights, light reflection/refraction on surface. Super slow camera movement, quality resolution.

Phase 8 (27-30s): Brand Freeze-frame
  Eject pulling back to panorama, product perfectly frozen. Logo + Slogan emerging. Visual clean and high-end.
```

#### Template B: Pure Product Cinematic 30s

```
═══ Segment 1 (0-15s): From Dark to Light, Revealing Entirety ═══

Phase 1 (0-3s): Dark Suspense
  Pure black, rim lights lighting up gradually, outlining product silhouette. Extremely slow rhythm, building anticipation.

Phase 2 (3-7s): Light Awakening
  Key light slowly rises, product emerging from darkness. Arc orbit from side to 3/4 front, first full display.

Phase 3 (7-11s): Suspended Disassembly
  Components separate, arc orbit with depth of field switching to focus individually. Blue energy lines connect components, implying internal synergy.

Phase 4 (11-15s): Precision Closure
  Components explode back to position, each snap-fitting. White light flash at closure -> reserved for screen activation in next segment.

═══ Segment 2 (15-30s): From Activation to Freeze-frame ═══

Phase 5 (15-19s): Feature Activation
  Inheriting closure flash -> screen diffusing and lighting up from the light point. Interface elements emerging, digits ticking, sensors activated.

Phase 6 (19-23s): Explosive Rotation
  High-speed 360° orbit, spotlight tracking key features rotating past (front -> side -> bottom -> back).

Phase 7 (23-27s): Macro Dive
  Decelerating from rotation -> lens diving to material macro. Extremely shallow depth of field revealing details (brushed -> chamfer -> seam -> coating). Super slow camera movement.

Phase 8 (27-30s): Brand Freeze-frame
  Material texture gradually blurring -> eject pulling back to panorama freeze. Product perfect posture + Logo + Slogan.
```

#### 30s Dual-segment Transition Design

| Transition Strategy | Description | Applicable |
|---------|------|------|
| **Motion Continuity** | Motion at the end of segment 1 continues at the start of segment 2 | All types |
| **Lighting Causality** | Lighting effects at the end of segment 1 become the light source at the start of segment 2 | Pure product type |
| **Scene Crosscut** | Lens penetrates product -> emerges into new scene | Brand world type |
| **Emotional Springboard** | Charge up at the end of segment 1 -> explode at the start of segment 2 | Requires climax feel |

---

### II. TVC 15s Compact Rhythm

#### Compressed Five-Stage Model

| Stage | Duration | Function | Product State |
|------|------|------|---------|
| **Flash Reveal** | 0-2s | Establish product impression in shortest time | Rim light rapidly lighting up / Match Cut entrance |
| **Core Selling Point** | 2-6s | Focus on displaying 1-2 core features | Feature activation / disassembly display (choose one) |
| **Visual Climax** | 6-10s | Most impactful frames | Explosive rotation / extreme scenes / macro wonder |
| **Emotional Anchor** | 10-13s | Leave a memory point | Extreme macro / emotional high point |
| **Brand Freeze-frame** | 13-15s | Logo + product + Slogan | Product final form freeze-frame |

#### 15s Iron Rules

- **Single Focus Principle**: 15s only conveys 1 core memory point.
- **No Empty Shots**: Every frame has product or brand info.
- **Transition is Content**: Match Cuts themselves are information delivery.
- **2s Freeze Rule**: The final 2s must be a static freeze frame.

#### 15s Compact Example (Wireless Earbuds)

```
Style: Tech minimalist / Pure black + pearl white + ice blue breathing light / Low-key studio shot / No background music. Ad for product@product_multiview_image.

Phase 1 (0-2s): Lid Opening Reveal
The charging case is in a pure black background, the lid slowly opens—interior ice blue breathing light lights up, two earbuds rise slightly in magnetic suspension out of slots. Camera micro pushes from front. The arc of lid opening guides the eye upwards.

Phase 2 (2-6s): Suspension + Feature Activation
Two earbuds completely separate from case, suspended and rotating. Left earbud cross-section lights up—internal chipset circuits emit pulse lights, noise-canceling mic arrays light up green points (active noise cancellation). Right earbud surface touch zone lights up an ice blue arc (touch control).

Phase 3 (6-10s): Explosive Rotation + Macro
Two earbuds rotate counter to each other 360° at high speed to show full view—after decelerating, camera pushes to earbud casing macro, pearl white ceramic surface nanometer grain texture filling the frame, color shifting slightly from pure white to light blue iridescence under side lighting.

Phase 4 (10-13s): Return to Charging Case
Camera ejects and pulls back. Two earbuds slowly descend back into charging case, emitting a faint white pulse at magnetic alignment. Lid closes slowly, brand Logo on the lid surface illuminated by rim light.

Phase 5 (13-15s): Brand Freeze-frame
Charging case rests at a 3/4 low angle at the center of the frame. Lid crack filters a slice of ice blue breathing light. Brand Logo emerges above, Slogan below in thin font.

Lighting Requirements: Low-key pure black background, product self-glow (breathing light / indicators / pulse lights) as main light source, with precise rim lighting outlining product edges.
```

---

## Appendix: Product Video Prompt Self-Check Checklist

- [ ] Each Phase has precise seconds marked (total duration = sum of Phase seconds)
- [ ] Camera movement has speed variation (fast and slow tempo contrast)
- [ ] At least one Phase contains material macro
- [ ] At least one Phase contains feature visualization
- [ ] Lighting has a narrative arc (variation and progression)
- [ ] Has Match Cut or visual transition (continuity of motion/color between Phases)
- [ ] End Frame elements are streamlined (only product + Logo + Slogan)
- [ ] Material descriptions have physical details (not "metal texture", but "brushed texture forming flowing highlights under side light")
- [ ] Product state has variation arc (from still -> disassembly -> activation -> display -> freeze frame)
- [ ] Brand tone is consistent
