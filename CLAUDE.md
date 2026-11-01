# Reel-editing — entry point for Claude Code

This repository hosts **Reel Studio** (RC1.10, EL COACH edition): Abdulrahman's production system for 9:16 Arabic fitness/coaching Reels
(HyperFrames renderer + Remotion/Three.js/Lottie inserts + FFmpeg/Python audio and QA).

## Start of every session
1. If `reel-studio/CLAUDE.md` exists → read it, then `reel-studio/MASTER_WORKFLOW.md`. Those are the rules; this file only points to them.
   Make sure the canonical path exists: `[ -e /home/user/reel-studio ] || ln -s /home/user/Reel-editing/reel-studio /home/user/reel-studio`
   and that the runtimes exist (`reel-studio/.venv`, `reel-studio/.hf`, `reel-studio/engine/remotion/node_modules`); if not, run the install in step 2 from "sh engine/setup.sh" on.
2. If `reel-studio/` is missing (fresh cloud container — this repo is public, so the studio is NOT committed): ask the creator to upload the
   Reel Studio zip (or point to a private artifact), verify its SHA-256 (RC1.10 EL COACH: `7af32025339da43acafc9c9b80042b8bf52ee45a70863ad179beabb433299d59`), then:
   ```sh
   cd /home/user/Reel-editing && unzip -q <zip> && ln -sfn /home/user/Reel-editing/reel-studio /home/user/reel-studio
   cd reel-studio && sh engine/setup.sh && (cd engine/remotion && npm ci) && .hf/node_modules/.bin/hyperframes browser ensure && sh bin/selftest
   ```
   Expect 67 passed / 0 failed / 4 skipped. Never upgrade pinned versions.
3. New footage uploaded → `MASTER_WORKFLOW.md` stage 0 onward. Do not edit anything unless the creator asked for production.

## ⛔ Permanent creator rule — NEVER modify the footage (2026-11-01)
Never change the original footage's colour, white balance, lighting, exposure, brightness, contrast, saturation, highlights/shadows,
sharpness, noise/grain, and never apply a LUT, grade, filter or "look" — not subtly, not to "fix" it, not on finished reels brought back for changes.
Edit only what surrounds the footage: cuts/timing, text, captions, graphics, transitions, framing (punch-ins/reframes), sound and music.
Only technical exception: a high-quality re-encode (no sharpening/denoise). HDR (iPhone HLG) sources stay HDR and untouched: graphics are
rendered alone (`GEN.overlay`, alpha MOV) and composited onto the original footage in 10-bit, delivered as HEVC Main10 HLG
(reference: `reel-studio/reels/reel-1102/build/composite.sh`). Verify on the delivered file that graphic-free footage is unchanged.
If the footage looks wrong, tell the creator; never correct it unasked. This rule overrides any older note that mentions grading.

## ✅ Approved editing standard (creator approval, 2026-11-01)
Reference: **reel-1102 v2** — Adam transformation, HDR (`deliveries/v2/final_reel.mp4`, MD5 `4abed917d73a76f2bdaaabf718556942`). Never modify it.
1. **RAW footage preserved** — footage, lighting, exposure, contrast, colour, skin texture and image quality untouched (rule above).
2. **Creative editing at that level** — hand-designed typography, word-by-word captions with the spoken word in lime, cards with a lime edge,
   pills, checklists that grow with the words, counters, purposeful graphic transitions, framed end card — all as layers over the footage
   (reference build: `reel-studio/reels/reel-1102/build/gfx.mjs`).
3. **No creative simplification** — footage preservation is never a reason for basic captions or simple editing.
4. **Video-specific direction** — every new video gets its own creative concept from its own content, at the same quality. Never copy reel-1102's devices blindly.
5. **Workflow** — the creator sends footage + instructions; analyse → plan → build → verify (footage unchanged, captions, audio gates) → deliver.

## Hard rules (summary — full list in reel-studio/CLAUDE.md)
- This GitHub repo is **PUBLIC**: never commit or push footage, renders, voice files, brand assets, transcripts or the studio itself unless the creator explicitly decides so.
- Music: a low, licensed bed under the voice on every reel (voice ≥ 18 dB above it; credit in the caption). Never invent or rewrite the creator's Arabic. Never overwrite `deliveries/`, `releases/` or approved masters.
- Report only measured results; unverified = UNKNOWN. Audio is never "approved" until the creator has listened.
- No paid services, global config changes or new packages without approval.
