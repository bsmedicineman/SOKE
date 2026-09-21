SOKE 2.0.0 — Self-Optimizing Knowledge Engine
A Windows program that writes a new type of AI model: the SFF (.sff) container — paged, gauge-tagged,
append-only, self-describing — and trains, converts, heals, expands and streams models in it. Since 1.2.0 it also
forges new `.gguf` models from a template you lay out, harvesting weights from the models Ollama already holds,
and improves the layout by trial and error on your own text.
BS Medicineman / Knight Industries · jurisdiction over the model

What's new in 2.0 (SOKE)
Renamed SOKE → SOKE (Self-Optimizing Knowledge Engine; soke = the Anglo-Saxon right to hold court
and give judgment). The Python package, `%SOKE_HOME%` data root and SFF magic keep their spelling for
backward compatibility, so existing installs and models keep working.
Home is a chat console. Load a second gguf as an advisor; it runs beside the model you are building
(two models live at once, the advisor in low-RAM streaming mode) and can Diagnose the build, Generate
probes, run the Behavior questionnaire, Suggest template edits, and Test the target — real SOKE
routines, narrated by the model. `soke/diagnose.py` powers the diagnosis (e.g. "only one donor — nothing to
blend", "min_gain is eating small real gains", "these operators never win").
Import sits next to Home; every imported file (text, PDF, ebook, model) is shared with every tab
(`ImportStore`).
Reskin: an early-Windows-95 chrome (beveled controls, sunken fields, tabbed folders) in the cream / olive
/ acid-green palette of the cover art (`soke/theme.py`).
Books: `soke/pdf_ingest.py` reads PDF / ePub / HTML with the standard library only (zlib), so the
Knowledge tab and the probes can learn from ebooks. No OCR — scanned/image-only pages yield little, reported
honestly. Editable sample corpus ships in `samples/corpus/`.
~17 template presets modeled on known model families and 10 probe presets on the Forge tab; expanded
topic-expert sets.
Real-time testing in Build & Train with an intensity you can change mid-run.
Tandem knowledge-tree scaffold (`soke/tandem.py`, optional): a math driver over a tree of per-branch
gguf models. SOKE routes a prompt to a branch and can run that one branch; the driver-orchestrated
multi-model runtime is declared, not built — the scaffold is present as requested.
CLI additions: `ingest-books <folder>`, `tandem [--route "…"] [--out tandem.json]`.
Self-test: 390 checks (`--quick` 332), including the new diagnose / pdf_ingest / tandem suites.
---
Install (one click)
Unzip `SOKE-2.0.0.zip` anywhere (e.g. `C:\Knight\SOKE`).
Double-click `INSTALL.bat`. It installs Python 3.12 for your user if no Python 3.10+ is found
(winget, or the official python.org installer), installs `numpy`, puts a SOKE icon on the desktop
and in the Start Menu, and runs the quick self-test. Nothing else is downloaded.
Double-click the SOKE icon (or `SOKE.bat`). `SOKE-CLI.bat` opens a command line where `soke <command>` works.
Four steps (Home tab): Add a folder → Name it → START LEARNING → Try it. `QUICK START.txt` says the same in one page;
the Help tab explains the words and numbers in plain language.
Requirements: Windows 10/11, ~200 MB disk for the program + Python, internet once for the install.
Runtime dependency: `numpy` only (everything else is the Python standard library). SOKE never imports
`numpy.random` / `numpy.fft` (their compiled files can be blocked by Windows Application Control / Smart App Control
even when numpy's core loads — seen on a Python 3.14 install); it ships its own vectorized generator (`soke/rng.py`).
The desktop icon is made by Python + COM, which works even where PowerShell is locked to Constrained Language Mode.
What it does
Tab	Purpose
Home	The simple front page: (1) Add a folder / Add files — folders are walked recursively, only text-like files count, pictures/programs/empty files are skipped and counted; (2) name + how long (Quick ≈ 2 min, Normal ≈ 15 min, Long = until Stop) + brain size; (3) START LEARNING with a progress bar and one plain sentence of status (every lock class, floor, trial, growth, heal and checkpoint is translated); (4) Try it. Right side: import a `.gguf` exactly, with a plain-language account of what happened.
Forge	Build a new `.gguf` from a template while harvesting weights from other `.gguf` files (1.2.0). 1 Donors: scan the model folder — Ollama's blob store `%USERPROFILE%\.ollama\models\blobs` by default (every `.gguf` and every blob that starts with the GGUF magic, blobs labelled from Ollama's manifests; change it with Browse or `soke settings --model-dir`); models are grouped into families (`arch:n_embd×n_layer:ff:heads/kv:vocab`) — donors of one family fill the same slots byte-for-byte. 2 Template: presets (math always-on = qwen2moe with a shared expert that works on every token + one routed expert per topic; all routed; dense; interleave; stack = every layer twice; random soup), then edit any cell: attention / expert / always-on per layer ← one donor (exact copy), a blend, an extrapolation `A + t·(B−A)` with t > 1 (weights no donor has), or zeros; duplicate/delete layers; re-source a layer from another donor layer; save/load the template (JSON). 3 Probes: your text, routed to the topics by the knowledge tower; train and hold-out chunks. 4 Learn: trial and error — 15 operators (swap/blend/task-arithmetic per slot, gate rescale/re-seed, always-on gain, expert topic swap, layer re-source, GROW add expert / duplicate layer, HEAL drop expert / drop layer, extrapolate); a change is kept only if the training loss drops by ≥ min-gain and the priority topic does not worsen by more than the tolerance; hold-out is scored, never optimised, and three worsenings in a row step back to the best hold-out template. Weights have no rank at the start — rank is what the trials discover. 4 Behavior (1.3.0): the fine-tuning layer — the emotion + logic pillars from the behavior map. A climate (or the 13 machine-chemical sliders + the 4-D emotion string) MODULATES the trial loop: CORT high → heal before grow, DA → bolder moves, NE → aim the worst topic, HT → patience, GABA/regulation → a STRICTER accept bar (never looser). The logic pillar adds a proof-state veto (⊥⊥ freeze+rollback, ? no-grow). Four auxiliary regularizers are logged and clamped, never the objective; task loss stays the only judge. The clone battery (Digital Psychoanalyst, consent-gated) captures your own word→feeling map, priors and veto style into `soke.clone.*` + the psychology helix. All of it rides the export as GGUF metadata + streamed ACTG helix teeth in the `.sff`, never as weights. 5 Export & Chat: `name.gguf` (loads in llama.cpp / Ollama / LM Studio; verified) + `name.sff` sidecar (template, per-tensor lineage, behavior helices, trial ledger) + `name.Modelfile`; forged MoE files are chat-only, not harvested; talk to any llama / qwen2 / qwen2moe `.gguf` with SOKE's own engine.
Help	What the numbers mean, what happens while it learns, what the files are, the Forge, the Behavior fine-tuning layer, the honesty rules — no jargon.
Build & Train	Every dial: corpus files/folders, model shape, learning rate, cycles, target loss, scoped corpus. Live loss curve with the corpus' bigram-entropy floor, ratchet milestones, plateau classes, control-arm trials. Buttons: Stop, Grow, Heal sweep, Finalize.
Import GGUF	Streams any `.gguf` into `.sff` without ever loading the file: tensor by tensor, block-aligned chunks, resident memory kept under the guard. Exact (default): F32/F16 native, Q8_0 → LIN8 and Q4_0 → LIN4 by byte transcoding, every other type (Q4_1/Q5_/Q8_1, K-quants, BF16, F64, ints, IQ/TQ*) as RAW pages of verbatim block bytes decoded on read — 0 error, output ≈ source + 1.7 % (page table 44 B / 4096 values + sections). Re-band (opt-in, lossy, error recorded per tensor): the Third-Law contest into f32/f16/8bit/4bit. Measured: a 700 MB / 1.07 B-parameter file, exact, in 60 s at a peak of 222 MB.
Inspect SFF	Summary, tensors (source type, pages, storage verdict, errors), patch log, lineage graph, the Third-Law storage table, the embedded ledger, deep verification (every section + every page checksum), compaction.
Knowledge	The helical memory: ingest files into domain strands (27 knowledge-tower domains), O(log N) seek, face-gear rides (one page window at a time), ACTG strands (`A[math:peano]{...} ~ T[math:induction]{...}`), MFP math boot with proof status per statement.
Generate	Byte-level generation from an `.sff` model with streaming experts: only the domain experts the router selects are loaded from the file.
Ledger & Self-test	Hash-chained, HMAC-signed ledger of every proof, route, descent, fork, heal and null; the research database (control-arm trials, milestones); the falsifier suite (375 executed checks); the frame calculus' own 47 checks and certified Third-Law rows.
Command line equivalents: `soke selftest | train | convert | inspect | generate | ingest | seek | boot-math | heal | grow | finalize | rollback | compact | status | settings | forge-inventory | forge-build | forge-run | forge-export | chat | score | behavior | clone`.
```
soke train --corpus C:\\my\\notes book.docx --model-id v001 --cycles 20 --steps 100 --finalize   (folders are walked recursively)
soke convert C:\models\phi-3.5-mini-q4_k_m.gguf            (exact; --mode reband --budget 8bit for the lossy contest)
soke inspect C:\models\phi-3.5-mini-q4_k_m.sff --opt --verify
soke generate soke_data\models\v001-final.sff --prompt "The theorem states"
soke settings --model-dir C:\Users\me\.ollama\models\blobs   (where to look for models and save forged ones; this is the default)
soke forge-inventory                                        (every GGUF in the model folder, grouped into families)
soke forge-build --donors qwen2.5/0.5b deepseek-r1-draft --preset math-always-on --topics math,language,science,code --out tpl.json
soke forge-run tpl.json --corpus C:\my\notes --trials 40 --minutes 60 --priority math --export mine.gguf   (a bare name saves into the model folder)
soke chat mine.gguf --prompt "What is a prime number?"        (then: ollama create mine -f mine.Modelfile)
soke behavior --climate scarcity --out climate.json          (the fine-tuning climate: CORT high -> heal-first)
soke clone --user me --session STANDARD                      (the consent-gated personality battery -> clone_profile.json)
soke forge-run tpl.json --corpus C:\my\notes --behavior climate.json --export mine.gguf   (modulated trial loop)
soke forge-export tpl.json --out mine.gguf --behavior clone_profile.json --clone-consent    (writes soke.clone.*)
```
Why SFF instead of GGUF (measured, not asserted)
Property	GGUF	SFF
Loading	whole file mapped; tensors are monolithic blobs	paged (4096 values per page); a 0.7 GB / 261,641-page file opens in ~60 ms with +31 MB RSS; a 4-row window of a 4096×11008 tensor (11 pages) reads in 0.4 ms with +0.1 MB
Modification	overwrite	append-only: new pages, page map re-pointed, patch log kept; rollback is a pointer change (byte-identical, tested)
Checkpoints	full copies	DELTA8 pages against key-frames (video-style: seek to any checkpoint)
Storage encoding	one quant type per tensor	imports are exact by default (source blocks kept verbatim or transcoded bit-for-bit); SOKE's own models use a per-page storage gauge chosen by the Third Law of storage among a bit band (linear = the GGUF layout family, log = L-register); the baseline error, the chosen error and the verdict (VERIFIED ≥ 33 % cut / TIE / EXACT) are recorded per tensor — ties are declared as ties
Provenance	KV metadata	lineage graph (every tensor, checkpoint, growth, import), patch log, experiments, Third-Law table, hash-chained signed ledger, knowledge index — all inside the file, every section and page checksummed
Knowledge	none	domain helices (ACTG teeth), face-gear streaming, O(log N) seek keys
Experts	n/a	each expert is a helix in its knowledge-tower domain; inference loads only routed experts
Standing honesty clauses carried from the protocol texts: cross-entropy 0.001 is only claimable against a declared
scoped corpus (LAW C); on general text the engine descends toward the corpus' own entropy floor and says so;
the log storage gauge is kept only where it wins ≥ 33 % (the tie table is in every file); orthometric frame weights
inside the net and pillar routing are standing nulls (SEPHIRA tests epsilon/delta) and are not re-entered.
Files
```
SOKE/
  INSTALL.bat  SOKE.bat  SOKE-CLI.bat  UNINSTALL.bat      Windows one-click tooling (+ QUICK START.txt, soke.ico)
  soke_main.py                                             entry (GUI when run without arguments)
  soke/                                                    the program (numpy + stdlib)
    sff.py teeth.py            the SFF container and its page/tooth codecs
    gguf_rewrites.py           streaming GGUF reader, dequantizers, GGUF->SFF, GGUF writer
    frame_engine.py            Orthometric frame calculus (47 executed checks, Third Law table)
    tower.py actg_parser.py memory_engine.py    knowledge tower, ACTG strands, helical memory
    proof_engine.py math_engine.py              Math Truth Engine + derivation graph (MFP boot 0-7)
    model_engine.py kernels.py                  SOKE-LM (numpy, explicit backward, gradient-checked), routes
    loss_engine.py expansion_engine.py heal_engine.py meta_optimizer.py orchestrator.py   ALM / EFP / SOP / ORB
    ledger.py memguard.py util.py selftest.py cli.py rng.py winshortcut.py
    tokenizer.py               GGUF tokenizers (byte-level BPE with the qwen2 / llama-bpe / gpt2 pre-tokenizers, SPM) — 138 llama.cpp vectors
    llm_engine.py              streaming inference for llama / qwen2 / qwen2moe GGUF (row-chunked dequant matmuls, GQA, RoPE, MoE, packed NLL, KV cache)
    forge.py forge_loop.py     donor inventory, family signatures, ForgeSpec template, live template store, assembly to GGUF + SFF sidecar; trial loop
    behavior.py                the fine-tuning layer: emotion (C, S_e) + logic (P, S_l) pillars -> loop knobs, proof-state veto, regularizers, GGUF metadata + helix teeth
    clone_battery.py           the Digital Psychoanalyst clone battery (A-H), consent-gated -> a personality profile + soke.clone.* + psychology helix
    gui.py gui_home.py gui_forge.py gui_help.py   the window: Home (simple), Forge (with the Behavior page), Help, and the advanced tabs
  docs/SFF_SPEC.md  docs/ARCHITECTURE.md                    byte-level format spec, module<->protocol map, decisions
  tests/                                                     cross-checks against the official gguf package and llama.cpp, 1 B streaming test
  soke_data/  (created on first run)                       models/, knowledge.sff, math_graph.json, ledger/, research.db, state.json, settings.json (model folder), forge/
```
Data root: `%SOKE_HOME%` if set, else `soke_data` next to the program.
Self-test
`SOKE.bat selftest` (full, a few seconds; 4.2 s on the build machine) runs 375 executed checks (each counted once — 1.0.0's runner double-counted 35 frame checks; corrected): SOKE's own RNG (moments, chi-square, a scalar
second route), the 35-row frame-calculus transcript re-executed (+12 more), codecs, container append/rollback/compaction/corruption, GGUF dequantizers against a scalar transcription
of the ggml loops, the tower, ACTG, helical memory, the proof engine (decision procedures never promote PATH 3
results), the model's backward pass against finite differences on every tensor, expansion equivalence proofs,
the heal gate, ALM laws, a full orchestrator run, and (1.2.0) the tokenizer, the inference engine against a plain-numpy
reference (chunked matmuls, streamed vocabulary, KV cache, packed batches, boundary snapshots), the forge (template
ops, live template == assembled file, byte-exact copies, sidecar) and the trial loop (ratchet, partial recompute == full
pass, grow/heal operators, export). `--quick` skips the training runs (317 checks).
`tests/crosscheck_llama_cpp.py` (needs `pip install gguf llama-cpp-python`) builds synthetic qwen2 / llama / qwen2moe /
llama-MoE models, runs them in llama.cpp and in SOKE's engine, and compares logits and NLL (F32: max |Δlogit| ≈ 1e-3,
argmax agreement 100 %; Q8_0: ≈ 3e-2 because llama.cpp quantizes activations to Q8 for that path); it then forges two
files and confirms llama.cpp loads and agrees with the live template. All pass on the build machine.
The behavioral fine-tuning layer (1.3.0)
Once the rough language configuration is forged, the behavior map ties the behavioral component to the
language component. It is a conditioning layer, taken from the operator's SOKE behavior mapping, and it
obeys that document's own laws, enforced in `behavior.py` and the self-test:
Modulate, not govern. A profile (a 4-D emotion string `S_e` × a 13-gain machine-chemical vector `C`,
plus the logic string `S_l` and proof-state `P`) tilts the trial loop's PROPOSAL — which operator is tried,
which topic gets attention — and may only make the accept bar STRICTER. It can never lower `min_gain` or relax
the priority tolerance. "Chemistry may bid; L0, Z and W close." The task NLL stays the only objective.
The C → forge-knob map (from section 02 of the map): DA → explore/extrapolate bias; OP → credit when a
topic lands; HT → patience / delay-gamma; NE → aim the worst topic; CORT → heal before grow (grow ops are
zeroed while load is high) + a tunnelled search window; GABA + regulation → veto strength; GLU → blend step
size; OXT → topic affinity; eCB → a decay pass after a burst.
The logic pillar adds a proof-state veto (`veto_and_shape_not_erase`): a non-finite candidate is `⊥⊥`
(frozen + rolled back + audited), an uncertain grow move is `?` (not promoted to a macro act), a worse
candidate is `⊥`. It can only veto or shape, never force an accept and never rewrite L0.
Four auxiliary regularizers — `L_want_like` (DA without OP), `L_cort_decay`, `L_veto_bypass` (must be
0 — an accept that skipped the priority veto), `L_oxt_weapon` — are logged and clamped every accepted trial.
Constraints, not goals to overfit.
The clone battery (`clone_battery.py`, the Digital Psychoanalyst) captures the operator's own word→feeling
and feeling→word lexicons, `S_e`/`S_l` priors, a `C` baseline, inversion pairs and a veto style — consent-gated
(SKIP/PASS/LATER/EDIT/STOP/RAW; three skips offer STOP; hard-red topics are never asked; WIPE tombstones, not
hides). Nothing reaches a model unless the operator consents.
On export, the profile is written as `soke.emotion.* / soke.logic.* /` (with consent) `soke.clone.*`
GGUF metadata (policies `modulate_not_govern` and `veto_and_shape_not_erase`) plus streamed ACTG helix teeth
(emotion `level_8`, logic `level_0`, behavior `level_14`, and the clone's psychology teeth) in the `.sff`
sidecar. Never a weight. `tests/crosscheck_llama_cpp.py` confirms llama.cpp still loads a
behavior+clone-conditioned `.gguf`, agrees with the live template to argmax 1.000, exposes the `soke.*`
keys, and the weights are byte-identical — the metadata is inert to inference.
Declared limit: this is conditioning + a behavior-tilted layout search, not gradient LoRA. The forge changes
what fills a slot and the layout, and writes the profile beside the weights; it does not back-propagate a trained
adapter into them (the map itself says: do not dump C into weights; stream the helix). Gradient LoRA with the same
ratchet/hold-out discipline is roadmap.
Forge numbers (measured on the build machine, 2 cores, no GPU)
Two 0.5 B-shaped Q8_0 donors (qwen2, 24 layers × 896, ff 4864, vocabulary 151,936; 506 MB each), template
math always-on with 3 topics, probes 18 train + 6 hold-out chunks × 192 tokens: baseline scoring 74 s, one trial
31–34 s (only the layers after the change are recomputed from cached boundary states), peak RSS 614 MB
(the 1.1.0 engine peaked at 1,644 MB on the same run; 1.2.0 streams the SwiGLU block over the ff axis and the
vocabulary in 32 MB logit blocks). Chat with the engine on the same model: 0.5–0.7 tokens/s. Bigger donors scale in
proportion; the forge is meant to run for minutes to hours, not seconds.
`tests/crosscheck_gguf_py.py` additionally checks the reader and every dequantizer against the official `gguf`
Python package bit-for-bit (needs `pip install gguf`; not required at runtime).
