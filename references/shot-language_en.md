# TVC Prompt Engineering Knowledge Base

> **Responsibility**: Reference for Phase 3 Art Style Confirmation + Phase 4/5 Prompt Writing. Covers Nano Banana Pro image prompt syntactic structure, art style choices, scene templates, and composition paradigms.
> **Out of Scope**: Creative strategies (refer to [treatment_en.md](treatment_en.md)), asset planning and generation sequence (refer to [pre-production_en.md](pre-production_en.md)), video prompts and multi-grids (refer to [storyboard_en.md](storyboard_en.md)), output formats and iterations (refer to [delivery_en.md](delivery_en.md)).

---

## Part 1: Prompt Structure

---

## I. Core Prompt Structure

Nano Banana Pro's optimal prompt structure is divided into six layers, ordered from left to right:

```
[Quality Anchor] + [Subject Description] + [Environment/Space] + [Lighting] + [Composition/Camera] + [Art Style Anchor]
```

### Layer Details

#### Layer 1: Quality Anchor (highest priority at front)

Quality anchors determine the overall generation quality and are placed at the very beginning of the prompt. The choice depends on the confirmed art style direction.

| Quality Anchor Word | Applicable Art Style Direction | Applicable Scenario |
|-----------|------------|---------|
| Real-life shoot | A. Real-life shoot | Real-life characters / scenes |
| Cinematic photography | A. Real-life shoot | Real-life movie frames |
| Real-life movie still texture | B. Real-life movie still | Cinematic movie level like Marvel/GoT |
| Hyper-realistic movie quality | B/C. Movie stills or CG | Hyper-realistic CG scenes (⚠️ leans toward CG when used alone) |
| Ultra-realistic movie quality | C. 3A game CG | High-realism CG scenes |
| 8K ultra-clear resolution | General | All scenes requiring fine textures |
| Cinematic lens | General | Cinematic frames |
| Master-class CG rendering | C/D. CG or engine grade | 3A games, animated CG |
| Unreal Engine 5 render | D. High-precision CG engine grade | Top-tier CG pursuing close-to-reality |
| Hyper-realistic CG | D. High-precision CG engine grade | Hollywood visual effects grade CG |
| Cinematic CG visual effects | D. High-precision CG engine grade | Ready Player One / Avatar level visual effects |

**Combination Examples by Art Style Direction**:
- **Real-life Shoot**: `Real-life shoot, cinematic photography, real skin pore texture, natural lighting`
- **Real-life Movie Stills**: `Real-life movie still texture, 8K ultra-clear resolution, cinematic color grading`
- **3A Game CG**: `Hyper-realistic movie quality, 8K ultra-clear resolution, cinematic color grading`
- **High-precision CG Engine Grade**: `Unreal Engine 5 render, 8K ultra-clear resolution, subsurface scattering skin, global illumination` or `Hyper-realistic CG, cinematic CG visual effects, 8K ultra-clear resolution, cinematic color grading`
- **Camera-leaning**: `8K ultra-clear resolution, cinematic lens`

#### Layer 2: Subject Description

**Character Description Hierarchy**:
```
[Identity/Name] + [Body Type/Physique] + [Facial Features] + [Clothing/Gear] + [Posture/Action] + [Expression/Emotion]
```

**Object/Weapon Description Hierarchy**:
```
[Type] + [Material] + [Size] + [Special Effects] + [State]
```

#### Layer 3: Environment / Space

```
[Space Type] + [Space Scale] + [Material/Surface] + [Atmospheric Effect] + [Environmental Details]
```

#### Layer 4: Lighting

```
[Overall Light/Dark] + [Key Light Source Position and Type] + [Lighting Effects] + [Color Temperature / Color]
```

#### Layer 5: Composition / Camera

Specify composition intentions and camera parameters using natural language in the prompt.

#### Layer 6: Art Style Anchor (wrapping up as backup)

Art style anchors are placed at the end to guarantee the overall style. **Must align with the confirmed art style direction.**

| Art Style Anchor Word | Applicable Art Style Direction |
|-----------|------------|
| Real-life shoot, cinematic photography, real skin pore texture, natural lighting | A. Real-life shoot |
| Real-life movie still texture, real skin texture and hair details | B. Real-life movie still |
| Cinematic film color, film grain | A/B. Real-life direction |
| 3A masterpiece 3D game style | C. 3A game CG |
| Cinematic color grading | General |
| Unreal Engine 5 render, subsurface scattering skin, PBR materials | D. High-precision CG engine grade |
| Hyper-realistic CG, cinematic CG visual effects, cinematic color grading | D. High-precision CG engine grade |
| Expressive lighting | E. Specific aesthetic |
| Minimalist composition | General |

---

## II. Quality × Art Style Combination Quick Reference

| Visual Goal | Art Style Direction | Quality Anchor (Pre-posed) | Art Style Anchor (Wrap-up) |
|---------|---------|----------------|----------------|
| Real-life shoot | A | Real-life shoot, cinematic photography, 8K ultra-clear resolution | Real skin pore texture, natural lighting |
| Real-life movie still | B | Real-life movie still texture, 8K ultra-clear resolution | Real skin texture and hair details, cinematic color grading |
| Hyper-realistic movie (CG-leaning) | B/C | Hyper-realistic movie quality, 8K ultra-clear resolution, cinematic color grading | — |
| 3A game CG | C | Master-class CG rendering, 8K ultra-clear resolution | 3A masterpiece 3D game style |
| High-precision CG engine grade (Character-leaning) | D | Unreal Engine 5 render, 8K ultra-clear resolution | Subsurface scattering skin, real skin texture, PBR materials, global illumination |
| High-precision CG engine grade (Scene-leaning) | D | Hyper-realistic CG, cinematic CG visual effects, 8K ultra-clear resolution | PBR materials, global illumination, cinematic color grading |
| Dark realism | A/B/C | Ultra-realistic movie quality, 8K material texture | Low-key lighting, high contrast, film grain |
| Grand scene | Follows global | Hyper-realistic movie quality, 8K ultra-clear resolution | Wide-angle lens, very low angle to highlight spatial scale |
| Oriental classical style | E | Cinematic quality, 8K | Chinese ink wash aesthetics, expressive lighting |
| Warm/healing style | E | 8K ultra-clear resolution | Golden Hour warm light, dreamy bokeh |

---

## III. Description Specifications for Multi-Image References

```
Composition Core:
Foreground: [Character/Object] (Image 1) [Posture/Position Description]. [Appearance Details].
Midground/Background: [Character/Object] (Image 2) [Posture/Position Description]. [Appearance Details].
Lighting:
[Light Source 1 Description].
[Light Source 2 Description].
Key Details: [Material reflections / reflections / special effects].
Camera Language: [Lens Type], [Angle], [Depth of Field].
```

---

## IV. Prompt Length Control

| Scene Complexity | Recommended Length | Description |
|-----------|---------|------|
| Simple (single subject + simple background) | 30-80 words | E.g., character three-view, object close-up |
| Medium (subject + environment + lighting) | 80-150 words | E.g., environment concept, single character scene |
| Complex (multi-layer composition + narrative) | 150-300 words | E.g., confrontation frame, multi-character scene |

**Principle**: Description precision > description length.

---

## Part 2: Art Style Anchor Vocabulary

---

## I. Art Style Direction Options

| Option | Description | Visual Effect |
|------|------|---------|
| **A. Real-life Shoot / Photography Grade** | Looks like real photographic pictures | Similar to movie stills, fashion photography |
| **B. Real-life Movie Stills** | Somewhere between real-life and CG | Similar to Marvel characters, Game of Thrones |
| **C. 3A Game CG** | High-quality game CG rendering | Similar to Final Fantasy CG, Genshin Impact cutscenes |
| **D. High-precision CG Engine Grade** | Full CG but pursuing top-tier "close-to-reality" texture | Similar to Ready Player One, Unreal Engine 5 MetaHuman |
| **E. Specific Aesthetic Style** | Ink wash painting, cyberpunk, anime, etc. | Depending on the specific style |

---

## II. Anchor Words & Combinations for Each Direction

### A. Real-life Shoot / Photography Grade

| Anchor Word | Applicable Scenario | Matching Recommendation |
|--------|---------|---------|
| Real-life shoot | Directly anchors toward real-life photo direction | + Cinematic photography + natural lighting |
| Cinematic photography | Emphasizes photographic feel rather than render feel | + Real-life shoot |
| Real skin pore texture | Forces microscopic details of real skin | Used for character setting drawings / close-ups |
| RAW photo texture | Raw, unprocessed photographic feel | + Natural lighting |
| Cinematic film color | Film-like color tone | + Film grain |

**Combination Examples**:
- `Real-life shoot, cinematic photography, real skin pore texture, natural lighting` — pure real-life photographic grade
- `Real-life shoot, 8K ultra-clear resolution, cinematic film color` — high-definition real-life film feel

### B. Real-life Movie Stills

**Combination Examples**:
- `Real-life movie still texture, 8K ultra-clear resolution, real skin texture and hair details, cinematic color grading` — cinematic grade
- `Hyper-realistic movie quality, real-life movie still texture, cinematic color grading` — hyper-realistic real-life leaning

### C. 3A Game / CG

Key anchor words: `3A masterpiece 3D game style`, `master-class CG rendering`, `hyper-realistic movie quality`, `8K ultra-clear resolution`, `cinematic color grading`

### D. High-precision CG Engine Grade

**Core Positioning**: Entirely CG rendered, but infinitely approaching reality in materials, lighting, skin, etc. Difference from C direction: C retains obvious "game CG aesthetics", while D pursues "indistinguishably realistic CG".

| Anchor Word | Applicable Scenario | Matching Recommendation |
|--------|---------|---------|
| Unreal Engine 5 render | Ultimate ray-tracing texture | + Global illumination + PBR materials |
| Subsurface scattering skin | Translucent skin light effect | + Unreal Engine 5 render + real skin texture |
| PBR materials | Physically correct material rendering | + Global illumination |
| Hyper-realistic CG | Directly anchors "CG pursuing realism" | + Cinematic color grading |
| Cinematic CG visual effects | Hollywood visual effects blockbuster level | + 8K + cinematic color grading |

**Combination Examples**:
- `Unreal Engine 5 render, subsurface scattering skin, real skin texture, PBR materials, global illumination` — top-tier engine grade CG (character-leaning)
- `Hyper-realistic CG, cinematic CG visual effects, 8K ultra-clear resolution, cinematic color grading` — Hollywood visual effects grade CG (scene-leaning)
- `Ray-traced render, PBR materials, global illumination, cinematic color grading` — engine grade CG environment

### E. Specific Aesthetic

| Anchor Word | Applicable Scenario |
|--------|---------|
| Chinese ink wash aesthetics | Classical / martial arts / Oriental themes |
| Cyberpunk aesthetics | Sci-Fi / futuristic cities |
| Japanese anime style | ACG / anime series texture |
| Studio Ghibli style | Warm/healing / Miyazaki style texture |
| Low-key lighting | Dark / suspense / horror |
| Golden Hour warm light | Healing / nostalgic / emotional films |

---

## III. C vs D Comparison

| Dimension | C. 3A Game CG | D. High-precision CG Engine Grade |
|------|------------|----------------|
| Skin | Exquisite but smooth, has idealized aesthetics | Has pores, fine lines, uneven skin tone, close to reality |
| Lighting | Game-level lighting, artistic adjustments acceptable | Global illumination + ray tracing, physically correct |
| Materials | Exquisite but allows styling/stylization | PBR physically correct, every surface has realistic reflections/roughness |
| Overall Impression | "Exquisite game character" | "CG or real?" |

---

## Part 3: TVC Scene Types

> TVC commercial-dedicated scene classifications and prompt templates. Designed around the three core demands: product display, brand narrative, and visual transitions.

---

## Scene Type Overview

| Category | Scene Type | Core Function |
|------|---------|---------|
| Product World Shots | Product Hero Shot | Keynote setting for main visual |
| Product World Shots | Cinematic Product Breakdown Frame | Technology capability visualization |
| Product World Shots | Feature Visualization Frame | UI/data/sensor presentation |
| Product World Shots | Material Macro Frame | Craftsmanship details magnification |
| Product World Shots | Pack Shot | Packaging display |
| Product World Shots | End Frame | Ending freeze-frame |
| Brand World Shots | Extreme Sports Scene | Extreme environment persuasiveness |
| Brand World Shots | Lifestyle Scene | Daily usage resonance |
| Brand World Shots | Emotional Scene | Emotional connection between character and product |
| Brand World Shots | Atmospheric Empty Shot | Brand world view establishment |
| Crossover Transition Frames | Match Cut Transition Frame | Visual bridge between Product World ↔ Brand World |
| Crossover Transition Frames | Product Reveal Transition | Transition revealing from usage scene → product close-up |

---

## Category 1: Product World Shots

---

### 1. Product Hero Shot

#### Prompt Template
```
[Quality Anchor], [Product Description] resting at the center of [Background]. [Lighting Design—side light / rim light / top light]. [Material Details—metal / glass / matte]. [Composition—product proportion / blank space]. [Art Style Anchor].
```

#### Key Points
- **Restrained Background**: Solid color or minimalist studio texture
- **Lighting with at least dual light sources**: Key light (side light for shaping) + fill/accent light (rim light to separate from background)
- **Materials must be described in detail**: Brushed metal, AG matte glass, ceramic sheen, etc.
- **Product Proportion**: 40%-60% is optimal

#### Example
```
8K ultra-clear resolution, cinematic product photography. A space gray titanium smart watch rests at the center of a pure black background, the dial turned slightly 15 degrees to the right. A soft side light on the left outlines the brushed texture of the titanium case and subtle chamfered highlights. A rim light on the right separates the product from the pure black background, forming a very fine white light border on the edge of the case. The dial displays a dark blue surface, with scales and hands reflecting faint cold white light. The watch strap is made of black fluororubber, showing fine diamond embossed patterns on the surface. The product occupies 50% of the center of the frame, leaving 30% blank space at the top. Extremely shallow depth of field, focus is on the dial. Product photography texture, cinematic color grading.
```

---

### 2. Cinematic Product Breakdown Frame

#### Prompt Template
```
[Quality Anchor], cinematic exploded state of [Product Name]'s [Component Description]. [Spatial relation of components]. [Glowing effects of core sensors/chips]. [Studio side light]. [Art Style Anchor].
```

#### Key Points
- **Hovering Spacing**: Need to describe specific spatial layer relationships between components
- **Glowing Elements**: Add faint self-glowing effects to chips, sensors, etc.
- **Component Count Control**: 3-5 component layers are optimal

#### Example
```
8K ultra-clear resolution, cinematic CG visual effects. A cinematic exploded view of a smart watch, with components suspended and expanded along the vertical axis. Top layer: sapphire crystal face, edges refracting iridescent halos. Second layer: AMOLED display panel, screen emitting faint blue self-glow. Third layer: titanium alloy middle frame, precise CNC machining marks visible. Fourth layer: motherboard and sensor modules, core chip emitting faint green glow, circuit traces as precise as strands of hair. Bottom layer: ceramic back cover, optical heart rate sensor emitting red pulse lights. Spacing between layers is uniform, with the overall view at a slightly high 3/4 angle. Pure black gradient background, studio side lighting from the left illuminating the edges of each component. Hyper-realistic CG, cinematic color grading.
```

---

### 3. Feature Visualization Frame

#### Prompt Template
```
[Quality Anchor], display screen/interface of [Product]. [Detailed description of screen content—UI elements/data/charts]. [Impact of screen light spill on surroundings]. [Position and state of the product body in the frame]. [Lighting—with screen self-glow as key light source]. [Art Style Anchor].
```

#### Key Points
- **Screen Content Must Be Specific**: Describe UI layout using geometric shapes, avoiding requests for precise text
- **Screen Light Spillover Effect**: Light from the screen illuminates surrounding surfaces
- **Dark Environment Reinforcement**: Make the screen the primary light source of the frame

#### Example
```
8K ultra-clear resolution, cinematic product photography. In a dark environment, a smart watch is worn on a wrist, the face turned toward the camera. The screen displays a workout monitoring interface: a large green heart rate number at the center, surrounded by three colored circle progress bars (red/green/blue), and a real-time heart rate waveform curve at the bottom emitting faint green pulse lights at the peaks. The cold blue glow of the screen spills onto the skin of the wrist, forming a soft blue halo on the skin surface. The background is completely black, with only the screen light as the sole light source. Close-up shot, slightly high angle, extremely shallow depth of field, focus on the screen with wrist edges softly blurred. Product photography texture, cinematic color grading.
```

---

### 4. Material Macro Frame

#### Prompt Template
```
[Quality Anchor], macro close-up of [Material Type] surface on [Product Part]. [Microscopic physical details—texture/particles/reflections]. [Macro lighting—side lighting to sculpt texture / backlighting to penetrate material]. [Extremely shallow depth of field, focus position]. [Art Style Anchor].
```

#### Key Points
- **Side Lighting is the King of Macros**: Low-angle side lighting maximizes the description of surface texture undulations
- **Physical Microscopic Details**: Metal machining toolmarks, glass micro-bubbles, fiber weave intersections
- **Scale Implication**: Add microscopic reference objects like dust particles to imply magnification scale

#### Example
```
8K material texture, macro close-up. The side chamfered area of a titanium watch case. Extremely low-angle side light sweeps from the left, illuminating every precise parallel groove of the brushed texture; the high points between grooves reflect sharp white highlight lines, while the low points sink into shadow. Extremely fine concentric toolmarks left by CNC machining are visible at the junction of the chamfer and the flat surface. A few dust particles are scattered on the surface, implying an extremely magnified scale. The right edge transitions to an AG matte glass area, the matte particles twinkling like fine starlight under the side light. Extremely shallow depth of field, focus on the midsection of the brushed texture, with the foreground and far end blurring rapidly. Product photography texture, high contrast.
```

---

### 5. Pack Shot

#### Prompt Template
```
[Quality Anchor], [Product Box Description—shape/color/material] facing the camera, [placement state]. [Product body next to the box]. [Lighting—soft studio lighting]. [Composition—position relationship between box and product]. [Art Style Anchor].
```

#### Key Points
- **Box + product in the same frame**
- **Box Angle**: Tilted 15-30 degrees provides more three-dimensionality than a flat front view
- **Soft lighting as primary**

#### Example
```
8K ultra-clear resolution, product photography texture. On a light gray gradient studio background, a matte black square packaging box is placed on the left side of the frame, tilted 20 degrees, with a silver hot-stamped brand logo on the box face. To the right of the packaging box, the smart watch body is shown at a 3/4 angle, the dial facing the camera, with the screen displaying the time interface. The box lid is slightly open, revealing the dark gray velvet lining material inside. Soft top light evenly illuminates the product and packaging, casting a soft oval shadow on the background. The product and box occupy 60% of the screen, leaving blank spaces at the top and right. Product photography texture, natural lighting.
```

---

### 6. End Frame

#### Prompt Template
```
[Quality Anchor], [Product Description] resting in [Background] in [angle/posture]. [Lighting—clean, premium]. [Composition—product offset, blank space reserved for text overlay]. [Art Style Anchor].
```

#### Key Points
- **Reserving Space for Text is Core**: At least 30%-40% clean area for Logo and Slogan
- **Stable Product Posture**: No motion implications
- **Post-production Space**: Logo/Slogan/legal info overlaid in post-production

#### Example
```
8K ultra-clear resolution, cinematic product photography. Dark gray gradient background; at the lower-left rule of thirds, a smart watch is stably set facing the camera, the dial displaying a dark blue interface. Soft side light from the left illuminates the product, creating a naturally transitioning shadow on the right. A clean space occupying 40% of the screen is left at the top-right, background gradient uniform with no clutter. The overall tone is steady, premium, and restrained. Product photography texture, cinematic color grading.
```

---

## Category 2: Brand World Shots

---

### 7. Extreme Sports Scene

#### Prompt Template
```
[Quality Anchor], [sport scene environment description]. [Athlete description—action/posture/gear]. [Position and state of the product on the athlete]. [Physical effects produced by motion—splashes/airflow/snowflakes]. [Lighting—natural lighting]. [Composition—dynamic]. [Art Style Anchor].
```

#### Key Points
- **Freeze the most tense moment**
- **Physical effects enhance motion**: Water splashes, swirling snow mist, flying dust
- **Product must be visible but not steal the scene**

#### Example
```
Real-life shoot, cinematic photography, 8K ultra-clear resolution. Alpine ski resort, strong midday sunlight. A skier at the frozen moment of a high-speed turn on a steep slope, body extremely low and tilted, outer hand almost touching the snow surface. The snow mist kicked up by the carving turn forms an arc-shaped white wave wall, snow particles twinkling like crushed diamonds in the backlight. The smart watch on the athlete's left wrist is clearly visible, the green glow of the GPS track interface contrasting with the white snow. Low-angle tracking shot from the side; the athlete cuts in diagonally from top-left to bottom-right, the snow mist behind occupying the top 1/3 of the frame. Real skin pore texture, natural lighting, cinematic color grading.
```

---

### 8. Lifestyle Scene

#### Prompt Template
```
[Quality Anchor], [daily scene environment description—time/location/atmosphere]. [Character description—clothing/state/emotion]. [Character's interaction action with the product]. [Environmental details—props enhancing lifestyle feel]. [Lighting—natural light / window light / warm tone]. [Composition]. [Art Style Anchor].
```

#### Key Points
- **"Casual" Feel is Key**: Product appears naturally in life
- **Realistic environmental props**: Coffee cup with usage traces, desk with natural clutter
- **Natural light + warm tones**

#### Example
```
Real-life shoot, cinematic photography, 8K ultra-clear resolution. 7 AM, beside a dining table in a Scandinavian style apartment. Warm morning window light spills from a large window on the left, casting window pane shadows on the wooden dining table. A woman in her 30s in a beige linen shirt sips from a white ceramic coffee cup with her left hand; the smart watch on her right wrist displays today's workout goal completion. An open magazine, a croissant, and a small dish of butter are scattered on the table. The background shows slightly blurred green plants and a kitchen island. Medium shot at eye level, character located at the right rule of thirds, window light on the left creating a large warm-colored light area. Real skin pore texture, natural lighting, cinematic film color.
```

---

### 9. Emotional Scene

#### Prompt Template
```
[Quality Anchor], [emotional scene environment]. [Character description—key emotional expressions and body language]. [Role of product in emotional interaction]. [Lighting—color temperature and contrast matching the emotion]. [Composition—close-up or medium close-up to highlight expressions]. [Art Style Anchor].
```

#### Key Points
- **Emotion conveyed through multiple channels**: Micro-expressions + body + lighting + color tone
- **Product as emotional carrier**: "Props" that trigger or carry emotion
- **Avoid excessive sentimentality**

#### Example
```
Real-life shoot, cinematic photography, 8K ultra-clear resolution. Evening living room; a young father sits on the sofa, his 3-year-old daughter asleep resting on his shoulder. He gently pats his daughter's back with his right hand; the smart watch screen on his left wrist lights up, displaying a message notification from his wife, the soft blue-white light of the screen illuminating his face. He lowers his head to look at the watch, the corners of his mouth rising slightly, eyes warm. A warm yellow lamp shines from the left side of the frame, wrapping the father and daughter in a warm light bubble, the background completely blurred into warm-colored Bokeh light spots. Medium close-up, characters located center-right, extremely shallow depth of field, focus on the father's facial expression. Real skin texture and hair details, cinematic color grading.
```

---

### 10. Atmospheric Empty Shot

#### Prompt Template
```
[Quality Anchor], [space type and scale]. [Environmental physical details—materials/textures/objects]. [Atmospheric effects—mist/light rays/particles]. [Lighting design]. [Composition/lens—wide-angle/high-angle/leading lines]. [Art Style Anchor].
```

#### Key Points
- **No characters**
- **Lighting is Emotion**: Delivered entirely through light, shadow, and color tones
- **Can be used as transitions**: Tone and composition must consider preceding and succeeding shots

#### Example
```
8K ultra-clear resolution, cinematic photography. A plateau lake at dawn, the lake surface calm as a mirror, perfectly reflecting the distant rolling snow mountains and gradient sky. The skyline shifts from deep blue to rose gold, the brightest point about to raise the sun over the ridge. A thin layer of morning mist floats on the lake, the mist flowing slowly about one meter above the water surface. Foreground shows gravel on the shore and a patch of yellowed alpine meadow, blurred by shallow depth of field into foreground color blocks. Wide-angle lens, rule of thirds composition: sky occupies the top 1/3, lake surface and reflection occupy the middle 1/3, shore foreground occupies the bottom 1/3. Cinematic film color, film grain.
```

---

## Category 3: Crossover Transition Frames

---

### 11. Match Cut Transition Frame

Design the "bridge frame" in a Match Cut: establish a perceivable visual continuity between A's end frame and B's first frame. For the complete Match Cut technique library, see [storyboard_en.md](storyboard_en.md) Part 4.

---

### 12. Product Reveal Transition

Smoothly transition from the usage scene of the brand world to close-up displays of the product world.

Transition Path: Usage scene wide view → Product partially visible → Product occupying screen → Product Hero Shot

#### Prompt Template (Three Stages)

**Stage A (Brand World → Product initial appearance)**:
```
[Quality Anchor], [usage scene medium shot]. [Character action naturally brings product into view]. [Product is clear but not focused in the frame]. [Environmental lighting]. [Art Style Anchor].
```

**Stage B (Transition frame — product magnified)**:
```
[Quality Anchor], [close-up/extreme close-up], [product occupying screen body]. [Environmental elements of usage scene blurred into background]. [Lighting transitions from environmental light to product photography light]. [Extremely shallow depth of field, focus locked on product]. [Art Style Anchor].
```

**Stage C (Product World — Hero Shot)**: Use the "Product Hero Shot" template.

#### Example (Outdoor Sports → Watch Close-up Reveal)

**Stage A**:
```
Real-life shoot, cinematic photography, 8K ultra-clear resolution. Sunny mountaintop; a cross-country runner bends over with hands on knees to catch breath after sprinting, lifting left wrist to check workout data. The smart watch is visible but small in the frame, the green glow of the screen still clearly distinguishable under sunlight. Background shows open valleys and blue sky. Medium shot, character located center, natural lighting. Real skin pore texture, cinematic color grading.
```

**Stage B (Transition frame)**:
```
Real-life shoot, cinematic photography, 8K ultra-clear resolution. Close-up of the smart watch on the athlete's left wrist, the dial facing the camera, screen displaying the stats interface after completing a 10km trail run. Watch occupies 60% of the screen, with sunlight highlights on the titanium surface and tiny sweat droplets visible on the case. Wrist skin and distant mountain scenery completely blurred into a warm-toned background Bokeh. Extremely shallow depth of field, focus on the dial. Mixed natural sunlight and faint rim lighting. Product photography texture, cinematic color grading.
```

---

## Part 4: TVC Composition Paradigms

TVC composition not only serves "aesthetics" but must also serve "delivery/conveyance".

### 4.1 Reveal Composition

**Classical Reveal Sequence**:

```
Step 1: Extreme macro—audience sees abstract texture/lines, without knowing what it is
Step 2: Slow zoom out—partial outlines begin to appear, audience begins to guess
Step 3: Continued zoom out—product full view revealed, cognitive pleasure of "so it's this"
Step 4: Product fully presented—shown in its entirety in perfect composition
```

**Variant Methods**: Obscuration reveal, lighting reveal, focusing reveal, rotation reveal.

### 4.2 End Frame Composition Standards

| Element | Composition Position | Size Requirement |
|------|---------|---------|
| **Product** | Center-left or dead-center of screen | Occupies 20%–40% of the frame |
| **Brand Logo** | Bottom-right corner or bottom-center | Clearly distinguishable but does not overpower the product |
| **Tagline/Slogan** | Above Logo or below product | Font size smaller than product name |
| **Background** | Brand color or brand signature visuals | Clean, non-distracting |

**End Frame Three Rules**:
1. **3-Second Read**: All information must be read by the audience within 3 seconds.
2. **Within 3 Elements**: Product + Logo + Slogan, maximum of three information hierarchies.
3. **3-Tier Visual Hierarchy**: Clear primary-secondary-supplementary visual priorities.

### 4.3 Text / Logo Safe Area

| Area | Definition | Usage |
|------|------|------|
| **Action Safe Area** | 5% inner border margin | All important visual elements |
| **Title Safe Area** | 10% inner border margin | All text information |
| **Top 1/5** | Top 20% | Tagline, title |
| **Bottom 1/5** | Bottom 20% | Product information, legal disclaimer |
| **Center 60%** | Center region | Core visual content, avoiding obscuration by text |

---

## Appendix: TVC Visual Design Checklist

- [ ] Is there an explicit placement strategy for brand colors?
- [ ] Do brand colors blend naturally with the film's color arc?
- [ ] Is the beauty of product materials unlocked through correct lighting strategies?
- [ ] Are product shots treated "sculpturally"?
- [ ] Does the proportion of product and negative space serve the narrative intent?
- [ ] Does composition reserve safe areas for text/Logo?
- [ ] Does the End Frame satisfy "3-second read, 3 elements, 3 hierarchies"?
- [ ] Is the brand's visual world determined and carried throughout the entire film?
- [ ] Does the choice of visual world match the brand tone and target audience?
