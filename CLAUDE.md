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

## Hard rules (summary — full list in reel-studio/CLAUDE.md)
- This GitHub repo is **PUBLIC**: never commit or push footage, renders, voice files, brand assets, transcripts or the studio itself unless the creator explicitly decides so.
- No music unless asked. Never invent or rewrite the creator's Arabic. Never overwrite `deliveries/`, `releases/` or approved masters.
- Report only measured results; unverified = UNKNOWN. Audio is never "approved" until the creator has listened.
- No paid services, global config changes or new packages without approval.
