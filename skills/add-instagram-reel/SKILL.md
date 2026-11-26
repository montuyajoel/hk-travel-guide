---
name: add-instagram-reel
description: Add a user-provided Instagram Reel URL to the Hong Kong & Macau Trip Navigator's Reel Inspiration gallery, preserving its original full-size embed layout and saving the change to GitHub without deploying unless explicitly requested.
---

# Add an Instagram Reel to the Trip Navigator

## When to use

Use this workflow when the user sends an Instagram Reel URL and asks to add it to the Reel Inspiration gallery, or sends a Reel URL in the established gallery-maintenance conversation where that intent is clear.

Repository: `montuyajoel/hk-travel-guide`  
Branch: `main`  
Target file: `reel-inspo.html`  
Live gallery: `https://hk-macau-trip-navigator.vercel.app/reel-inspo.html`

## User preferences and safety rails

- **Never deploy automatically.** Commit the change to GitHub `main`, then wait. Deploy only after an explicit user instruction such as “deploy” or “deploy now”.
- Keep the existing original gallery presentation: full-size Instagram embeds in a vertical stack. Do not convert it to a compact grid, thumbnails, or a custom player.
- Preserve every existing Reel and its numbering.
- Add new Reels at the very top of the gallery so the newest item appears first.
- Do not claim Instagram playback is guaranteed; Instagram controls embed availability and playback.
- Be concise in the completion message and clearly say whether the update was committed or deployed.

## Procedure

1. **Normalize the submitted URL.**
   - Accept standard Reel URLs such as `https://www.instagram.com/reel/ABC123/`.
   - Extract the Reel shortcode from the `/reel/<shortcode>/` path.
   - Remove tracking/query parameters (for example `?hvrq=...`) and use the canonical URL `https://www.instagram.com/reel/<shortcode>/`.
   - If the URL is not a recognizable Instagram Reel URL, ask for clarification instead of editing the page.

2. **Fetch the latest target file from GitHub.**
   - Use the GitHub fetch-file action for `reel-inspo.html` on `main`.
   - Always edit the freshly fetched content and use its current blob SHA for the update. Never base the edit on a stale local copy or a previous conversation snapshot.

3. **Determine the next Reel number.**
   - Inspect the current gallery's embed anchors/labels (for example, “View Reel 23 on Instagram”) and find the highest existing Reel number.
   - Assign the next sequential number. Do not use the number of cards or assume a fixed starting point.
   - If the exact same shortcode is already present, do not add a duplicate. Report that it is already in the gallery.

4. **Insert one official Instagram embed at the top.**
   - Insert immediately inside the gallery's existing `<section class="panel">`, before the current first Reel card.
   - Use the established markup and styling, changing only the canonical URL and Reel number:

   ```html
   <div class="reel-card"><div class="reel-preview"><blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/reel/SHORTCODE/" data-instgrm-version="14" style="background:#fff;border:0;max-width:540px;width:100%"><a href="https://www.instagram.com/reel/SHORTCODE/" target="_blank" rel="noopener">View Reel NN on Instagram</a></blockquote></div></div>
   <div style="height:14px"></div>
   ```

   - Replace `SHORTCODE` with the extracted shortcode and `NN` with the next number (use two digits for numbers below 10, otherwise the natural number).
   - Do not remove or reorder existing cards, alter the theme controls, change the gallery layout, or change the Instagram embed script.

5. **Commit to GitHub.**
   - Update `reel-inspo.html` on `main` using the fetched blob SHA.
   - Use a clear commit message, e.g. `Add Instagram Reel 24 to inspiration gallery`.
   - Confirm the returned commit SHA.

6. **Verify the edit.**
   - If practical, fetch the file again and confirm:
     - the new canonical Reel URL appears exactly once;
     - the new Reel label uses the next sequential number;
     - the new card is the first card in the gallery;
     - the previous first Reel remains directly after it;
     - the full-size vertical embed structure and Instagram embed script remain intact.

7. **Respond to the user.**
   - State the assigned Reel number.
   - Link to the gallery and the GitHub commit.
   - Explicitly say: “Saved to GitHub, not deployed.”
   - Do not say the live gallery has changed until a deployment has actually been requested, completed, and verified READY.

## Deployment (only on explicit request)

If the user explicitly asks to deploy after the commit:

1. Deploy the latest `main` commit to the Vercel production project `hk-macau-trip-navigator`.
2. Wait for the deployment to reach `READY`.
3. Confirm the production alias `https://hk-macau-trip-navigator.vercel.app`.
4. Report the deployment as live only after READY is confirmed.

Never deploy simply because a Reel was added.
