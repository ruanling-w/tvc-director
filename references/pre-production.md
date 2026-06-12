# TVC Asset Image Generation Framework

> **Core Mission**: After the storyboard script is finalized and before outputting storyboard keyframes, generate a set of **visual asset images** first—locking in the visual baseline of "people, objects, and scenes" for all subsequent frames.
> **Essence**: Asset images = TVC "casting + set design + product look". Just like when shooting a live-action commercial where you must first finalize actors, set up scenes, and arrange products—the same logic applies to AI generation.
> **Only Three Asset Types**: Character three-view, product image, scene image. Do not invent a fourth.

---

## Part 1: Asset Planning—From Storyboard Script to Asset List

> Once you receive the storyboard script, do not rush to generate images frame by frame. Scan the script and answer two questions:

### Question 1: Who is on camera?

- **Product** → Must generate product images, no exceptions
- **Characters/Models** → Determine if character asset images are needed:

| Decision Dimension | Create Character Asset Image | Only Standard Presenter Description Needed |
|----|----|----|
| **Category Path** | Identity-based (fashion/wearables/jewelry/luxury) → The styling itself is the brand world, must create | Functional (tech/tools) and the character is just a "user background board" |
| **Placement Strategy** | Lifestyle Film → Product worn on the body and stays in scene, character spans over 5 panels | Brand World Crosscut → Character only appears in a few brand world panels |
| **Appearance Method** | Lower body/hand/partial but **appearing repeatedly across multiple panels** → High risk of accumulated styling inconsistencies | Only 1-2 panels of wide shot silhouettes / back views / group shots |

**Core Logic**: The trigger for character assets is not "whether the face is visible", but rather "**whether the character styling is the core visual element of this TVC**". In identity-based brand worlds, even if no faces are shown in the entire film, the clothing/accessories/posture are the brand expressions—they must be locked with asset images.

### Question 2: Where to shoot?

- Scan all scenes appearing in the storyboard, categorizing them into a few **visually distinct spaces**.
- Create one scene image for each independent space (locking in atmosphere, color tone, lighting keynote).
- If the entire film is set in a studio (pure cinematic product breakdown) → Scene images can be omitted; the studio atmosphere is already locked in the product images.

### Generation Sequence

```
① Product Image (Highest priority—the product is the soul of the TVC)
② Character Three-view (If someone is on camera—characters interact with the product, so you need to know what the product looks like first)
③ Scene Image (Relatively independent, but color tone must harmonize with the product image)
```

---

## Part 2: Definitions of the Three Asset Types

> **Default Assumption: Product reference image exists.** Real TVCs are always advertising existing products—product official images / physical photos / e-commerce images almost certainly exist. "No product reference image" is an exception path (conceptual product / virtual product / early design stages), only enabled when the user explicitly states that the product has not been physicalized yet.
>
> Reference images determine the **writing path** of prompts—the prompt structures of the two paths are completely different:
> - **Default Path (with reference images)** → Prompt directly references the "product in the image / character in the image", **without describing appearance details** (appearance is locked by the reference images; extra description only interferes with reconstruction).
> - **Exception Path (no reference images)** → Prompt must describe the appearance precisely in text (materials, colors, shapes, etc.), pure text-to-image.
>
> **Do not block the workflow because the user lacks reference images.** Both paths can produce usable asset images—however, the product reference image should be proactively asked for during the Creative Brief stage, rather than waiting for Pre-production to ask as a quick fix.

### 2.1 Product Image

**Purpose**: Lock in the product's appearance, materials, color scheme, and proportions. All subsequent product shots reference it.

**Reference Image Interaction**:
- The product reference image should have already been confirmed in the Creative Brief stage (Phase 1); do not repeat questions regarding the product level in the Pre-production stage.
- If Phase 1 was omitted (Mode B/C skipped the Creative Brief), ask as a follow-up: "Do you have official images / physical photos / e-commerce images for this product?"—assuming by default that it "exists" rather than asking "if it is needed".
- Once the user replies, directly generate the prompt according to the corresponding path, **do not request images, and do not wait for images**.

**Two Prompt Paths**:

| Path | Applicable Scenario | Prompt Writing | Example |
|------|---------|-----------|------|
| **Default Path (with reference image)** | Launched products, finalized designs, products with any official visual assets | `Based on the reference image, generate xxx for this product` — without describing product appearance | "Based on the reference image, generate multi-view for this product, white background studio, unified side lighting + rim lighting..." |
| **Exception Path (no reference image)** | Conceptual products, virtual products, early design stages, user explicitly requests text definition | Must precisely describe product appearance in text (materials, colors, shapes, design features) | "White background studio, a square amber glass perfume bottle, walnut cap, vertical stripes carved on the body..." |

**Core Requirements** (shared by both paths):
- **White background / solid color studio**, without introducing any environmental elements—purely locking in the product itself.
- **Lighting with at least dual light sources**: Key light (side light for shaping) + fill/accent light (rim light to separate from background).
- **Extra requirement for Exception Path—Materials must be described in detail**: Instead of "metal shell", use "brushed texture titanium shell, concentric CNC machining marks visible on the chamfered edges".

**How many to make? How to choose?**

| Scheme | When to Use |
|------|-----------|
| **Product Multi-view (TVC Default)** | One image containing multi-angle full body + key detail close-ups. The product will inevitably appear from multiple angles in TVC ads, making multi-view the standard primary asset. |
| Single Hero Shot | Only when the product appears from a single angle (rare in TVCs) |
| Extra Material Macro | When there is an extreme macro shot in the storyboard, append an independent macro image on top of the multi-view. |

TVC ads **generate product multi-views by default**. Do not output Hero Shots, profile views, and macros individually one by one—one multi-view locks all angles and key details, maximizing efficiency and consistency.

**Product Multi-view Prompt Templates**:

Default Path (with reference image):
```
Based on the reference image, generate multi-view for this product. White background studio, unified side lighting + rim lighting.
Includes the following angles: 3/4 classic angle full body, front full body, side full body, back full body,
and 2-3 key detail macro close-ups (such as the bottle cap / button / material texture / interface, which are the most recognizable parts of the product).
Maintain consistent lighting direction and color temperature across all angles.
```

Exception Path (no reference image):
```
White background studio, multi-view of [complete product appearance description]. Unified side lighting + rim lighting.
Includes the following angles: 3/4 classic angle full body, front full body, side full body, back full body,
and macro close-ups of [specific detail part 1] and [specific detail part 2].
Maintain consistent lighting direction and color temperature across all angles.
```

### 2.2 Character Asset Image

**Purpose**: Lock in the character's body shape, clothing, accessories, and temperament (and face, if applicable). All subsequent frames featuring this character reference it.

**Three Prompt Paths**:

| Path | Trigger Condition | Prompt Writing |
|------|---------|-----------|
| **Face Ref + Product/Clothing Ref** | User provided model photo and product image | `(Image 1) model reference, (Image 2) product/clothing reference`, referencing both images in the prompt without describing character appearance and product look |
| **Face Ref, No Product Ref** | User only provided model photo | `Based on the reference image, generate xxx for the character in the image`, without describing appearance but requiring text description of clothing/styling |
| **No Reference Image** | User has no character reference | Must precisely describe appearance + body type + clothing + accessories in text, pure text-to-image |

**Core Requirements** (shared by all paths):
- **White background, unified lighting**: Soft studio lighting, consistent lighting direction and color temperature across all angles.
- **Clothing aligned with brand tone**: Minimalist urban style for tech products, natural cotton/linen style for tea drinks, dark techwear style for avant-garde brands.
- **Expression kept neutral and natural**: Specific emotions are left for the storyboard frames.
- **Extra requirement for No Reference Image path—Lock 2-3 key facial features**: E.g., "oval face, almond eyes, black shoulder-length straight hair"—too many details make it harder for AI to maintain consistency.
- **Hierarchy of character description for No Reference Image path**: `[Identity] + [Body Type] + [Facial Features] + [Complete Clothing Description] + [Accessories] + [Temperament]`

**Asset Images Are Always Full-Body**:

Character asset image = casting lookbook. Real TVC directors always look at the whole person during casting—shooting only legs/hands/back view is a filming decision, not a casting decision. Clothing is a holistic styling system (tops + bottoms + shoes + accessories echoing each other); shooting only half-body loses the complete context of the styling.

| Facial Visibility | Asset Image Format | Description |
|------------|----------|------|
| **Face Visible** | **Complete Three-view**: Facial close-up + front full body + back full body | Standard format |
| **Face Hidden / Obscured** | **Styling Lookbook**: Front full body + side full body + back full body + key accessories close-up | Face can be obscured / lower half / profile, focusing on locking in the complete clothing and accessories styling |
| Only 1-2 panels of silhouette/back view | **No asset image created**, replaced by standard presenter description | See Part 3 Character Consistency |

> **Generating half-body / partial character asset images is prohibited.** Even if only the lower body or hands appear in the storyboard, the asset image must be full-body—the holism of styling determines the visual logic of each detail.

**Character Assets Wearing Products Must Reference Product Images**:

When the product is worn on the body / wrist / held in hand (running shoes, watches, jewelry, jackets, glasses, handbags, etc.), the character asset prompt **must reference the pre-generated product multi-view** to let the character wear/carry the product on camera. Writing method: Upload the product multi-view in the edit mode of Nano Banana Pro, and reference it with `(Image N)` in the prompt—e.g., `wearing the running shoes of Image 1` / `wearing the watch of Image 1 on wrist` / `wearing the jacket of Image 1`. Not referencing the product image = uncontrollable product appearance on the character's feet/hands/body = collapse of subsequent storyboard consistency.

#### Character Asset Image Prompt Examples

**Example 1: Pure text generation (no reference image, face visible) — Classical Hanfu Model**

```
A high-quality studio photography three-view, including facial close-up, front full body, back full body.
A beautiful young woman standing in an exquisite Tang-style Hanfu in light champagne gold and red bean paste tones, full-body portrait.
The Hanfu fabric is of fine silk texture, dotted with soft light blue and pink floral embroidery and classical dark patterns.
A cyan-green belt with an exquisite blue jade buckle is tied around her waist. She wears an elegant cloud bun,
adorned with minimalist yet gorgeous floral hair accessories, pearl earrings, and tasselled hairpins.
Her hands are formally folded in front of her waist, wide sleeves hanging down naturally, showing a graceful and dignified posture.
The character looks straight at the camera with clear eyes and a calm expression.
Pure white background, soft studio lighting, 8k resolution, ultra-realistic realism, extremely fine fabric texture.
```

**Example 2: Face Ref + Clothing Ref — Fashion Styling Multi-panel Display**

```
Masterpiece, 8K ultra HD, realistic photo, 16:9 landscape composition, 4-panel fashion display layout,
Panel 1: Close-up portrait of the woman in Image 1, wearing the leopard print dress in Image 2, clean white background, soft studio lighting,
Panel 2: Front full-body photo of the same woman, wearing the slim-fit long-sleeved V-neck leopard print mini dress in Image 2, holding the black small handbag in Image 2, nude pointed high heels, standing naturally, white studio background,
Panel 3: Side full-body photo of the same woman, same styling, handbag, and shoes, standing naturally, white background,
Panel 4: Back full-body photo of the same woman, same styling, handbag, and shoes, standing naturally, white background,
Facial features are completely identical, hairstyle is identical (long wavy dark brown hair), accessories are identical (thin silver necklace, small ear studs, silver bracelet, ring),
skin tone is identical, professional fashion lookbook style, unified lighting, sharp focus, no distortion, no blur
```

> Example 2's key writing method: Use `(Image 1)` to lock in the face/body type, and `(Image 2)` to lock in the clothing/accessories appearance. The prompt only describes the styling combination method and the display angles—appearance details are handed over to the reference images. Each panel uses "same woman" and "same styling" to reinforce consistency.

**Example 3: Face Hidden + Referencing Product Image — Running Shoes TVC Model Styling Lookbook**

```
Masterpiece, 8K ultra HD, realistic photo, 16:9 landscape composition, 4-panel athletic styling layout,
Panel 1: Front full-body photo of a beautiful, slender young Asian woman, black high ponytail, wearing black high-waisted slim-fit ankle-length running tights (matte compression fabric, snug above ankles), light gray short-sleeved slim-fit quick-drying top, wearing the white running shoes of Image 1 on feet, extremely short no-show socks exposing slender ankles, standing naturally with hands relaxed at sides, head slightly lowered showing only jawline, clean white background, soft studio lighting,
Panel 2: Side full-body photo of the same woman, same styling, wearing the white running shoes of Image 1 on feet, standing naturally, showing the running tights side cut and the complete side profile of the running shoes of Image 1, white background,
Panel 3: Back full-body photo of the same woman, same styling, wearing the white running shoes of Image 1 on feet, standing naturally, showing the back design of the top and the hip line cut of the tights, white background,
Panel 4: Close-up of the ankle and running shoes, showing the scale relation between the white running shoes of Image 1 and the slender ankle, the woven texture of the shoe upper is clearly visible, a section of skin exposed between the tight cuffs and shoe collar,
Body shape completely identical, clothing completely identical, hairstyle identical (black high ponytail), skin tone identical, professional sports lookbook style, unified lighting, sharp focus, no distortion, no blur
```

> Example 3's key writing method: **repeat `wearing the white running shoes of Image 1 on feet` or `the white running shoes of Image 1` in every single panel**—referencing the product only once is easily ignored by the AI; repeating it in every panel ensures that the character wears the product in every view. The format references Example 2's "same woman" and "same styling" methods to reinforce consistency. Facial visibility is bypassed by lowering the head while retaining hairstyle information.

**Iron Rule of Product Referencing**: When the character wears the product, the product reference **must be repeated in the prompt for every single panel** (`wearing the xxx of Image 1 on feet` / `wearing the xxx of Image 1 on wrist`), rather than mentioning it only once at the beginning. The weight of a single mention is not enough for the AI to render the product correctly in all angles.

### 2.3 Scene Image

**Purpose**: Lock in the visual atmosphere of the brand world—space, lighting, color tone, and time. All subsequent frames in this scene continue this visual keynote.

**Two Prompt Paths**:

| Path | Prompt Writing | Example |
|------|---------|-----------|
| **With Reference Image** | `Based on reference image, generate xxx with same scene atmosphere` — without describing scene details | "Based on the reference image, generate a 16:9 wide empty shot with same scene atmosphere, no characters, no products, maintaining the same color tone and lighting keynote" |
| **Without Reference Image** | Must precisely describe space, color tone, lighting, and time in text | "16:9 wide shot, Scandinavian minimalist apartment living room in early morning, golden morning sun pouring through floor-to-ceiling windows, white walls, gray floor..." |

**Core Requirements** (shared by both paths):
- **No characters, no products**: The scene image only locks in the "space itself"; people and products are added later in the storyboard frames.
- **Time and weather must be explicit**: For the same tea plantation, early morning mist and midday scorching sun yield two completely different images.
- **Color tone is the core deliverable**: The most important output of the scene image is the "color tone baseline".
- **Foreground/midground/background layering**: The scene must have spatial depth.
- **Wide aspect ratio 16:9**

**How many to make?**
- Create one for each **visually distinct space** in the storyboard.
- Different corners of the same space do not need to be generated separately.

---

## Part 3: Consistency—The Core Value of Asset Images

> The value of asset images is not "aesthetics", but "referentiability". Subsequent storyboard frames ensure visual consistency across the entire film by referencing asset images.

### Product Consistency

Establish a **standard product description** based on the product image, to be uniformly reused in prompts of all subsequent frames:

```
[Product Name], [Core Material] + [Color Scheme], [Key Design Feature 1], [Key Design Feature 2].
```

### Character Consistency

- **With Asset Images**: Subsequent frames reference the asset image (`[Character Name] in the image` or `(Image N)`), without repeating appearance descriptions.
- **Without Asset Images (silhouettes/wide shots where no asset is created)**: Establish a **standard character description**, to be uniformly reused in all subsequent frames:
  `[Skin Tone / Ethnicity] + [Body Type] + [Clothing Style + Color] + [Key Accessories]`
  Example: "Asian male, lean runner physique, black tight ankle-length running tights, dark gray quick-drying tank top, no accessories"
- Clothing/hairstyle/body type descriptions remain unchanged; only expressions and postures can change.

### Scene Consistency

- Different shots of the same scene maintain consistent color tones, lighting directions, and atmospheric effects.
- The color tone of the scene image is the "baseline color"; subsequent frames can be fine-tuned but must not jump abruptly.

### Cross-Asset Coordination

- Product color tones and scene color tones must harmonize—warm scenes pair with warm product lighting.
- Character clothing colors echo brand colors / scene colors.
- All assets consistently use the same art style direction.
