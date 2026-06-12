# Contributing to Kerrigan's TeX-Marp Necklace / 鍙備笌璐＄尞

> This Skill is part of the AC Paradigm v6 ecosystem. Contributions should follow the AC paradigm rules and three-state closure protocol.

## Ways to Contribute / 璐＄尞鏂瑰紡

### 1. Extend the Problem Registry / 鎵╁睍闂娉ㄥ唽琛?
The `references/problem-capability-registry.md` tracks 28+ registered problem types. To add a new one:

1. Identify whether it's a **LaTeX** (LTX-xxx) or **Marp** (MP-xxx) problem
2. Add an entry following the existing template:
   - Symptoms / 鐥囩姸
   - Root cause / 鏍瑰洜
   - First reference (past practice) / 绗竴鍙傝€?   - Skill document / Skill 鏂囨。
   - Examples/Scripts / 鑼冧緥/鑴氭湰
   - Severity / 涓ラ噸搴?   - User alignment required? / 鐢ㄦ埛瀵归綈
3. Add corresponding error codes to `scripts/format_guard.py` if the problem is mechanically detectable
4. Add a smoke test in `evals/smoke/`

### 2. Add Smoke Tests / 娣诲姞鐑熼浘娴嬭瘯

Place test fixtures in `evals/smoke/`. Each smoke test should:

- Be a minimal, self-contained `.tex` or `.md` file
- Trigger exactly one route path (A鈥揌) from the SKILL.md route index
- Include a comment header describing which route it tests and what the expected behavior is

### 3. Improve Format Guard / 鏀硅繘鏍煎紡鏍￠獙

The `scripts/format_guard.py` script is the hard gate. When adding new checks:

- Follow the existing error code naming convention (TEX### for LaTeX, MARP### for Marp)
- Maintain the three severity levels: `error` (hard-block), `warning` (review-required), `info`
- Output structured JSON that includes `severity`, `code`, `message`, and `line` fields
- Update the error code quick-reference tables in both `problem-capability-registry.md` and `README.md`

### 4. Improve Reference Materials / 鏀硅繘鍙傝€冩潗鏂?
- **Guides** (`latex-guide.md`, `marp-guide.md`): For from-scratch authoring instructions
- **FAQs** (`latex-faq.md`, `marp-faq.md`): For common problem diagnosis and repair
- **Capability Maps** (`latex-capability-map.md`, `marp-capability-map.md`): For capability disclosure chains
- **Install Preflight** (`install-preflight.md`): For environment setup instructions

When adding content, maintain bilingual (Chinese/English) parity.

## Guidelines / 瑙勮寖

- Follow the **three-state closure protocol**: every PR must be marked as 宸查棴鍚?鏈棴鍚?褰撳墠涓嶅彲鍒ゅ畾
- Content decisions that affect output quality **must** go through AskUserQuestion, not auto-resolved
- Format guard changes must be accompanied by updated smoke tests
- The Skill's boundary philosophy ("maximal restraint, lower bound of typesetting") must be respected 鈥?no decorative features

## Development Setup / 寮€鍙戠幆澧?
```bash
# Clone and navigate
cd .trae/skills/acp-traetune-kerrigan-s-tex-marp-necklace

# Verify format_guard.py runs
python scripts/format_guard.py --help

# Run existing smoke tests
python scripts/format_guard.py evals/smoke/latex_overflow_case.tex
python scripts/format_guard.py evals/smoke/marp_overflow_case.md
```
