# Tool-Call Reliability Bench

An agent that books the right appointment four times out of five is not safe to leave unattended. This repository measures **pass^k**, the chance that all k attempts at the same task are correct, for small open-weight models run locally on eight physiotherapy-clinic tool calls requested in **English** and in **Roman Urdu**.

**Paper:** *Right Once, Wrong Next Time: Repeated-Trial Reliability of Small Local Models on Roman Urdu Clinic Tool Calls*, November 2026 ([`tool-call-reliability-paper/`](tool-call-reliability-paper/)).

## Main results (320 calls)

| Model | Language | pass^5, five wordings | pass^5, five samples |
|---|---|---|---|
| llama3.1:8b | English | 87.5 | 87.5 |
| llama3.1:8b | Roman Urdu | 37.5 | 37.5 |
| qwen2.5:3b | English | 75.0 | 75.0 |
| qwen2.5:3b | Roman Urdu | 12.5 | 25.0 |

67 of the 73 failed calls (91.8%) were valid against the tool schema: the format was right and a value was wrong, mostly times, amounts and numbers written as words in Roman Urdu.

## Layout

| Folder | What it is |
|---|---|
| [`tool-call-self-correction/`](tool-call-self-correction/) | The 8 clinic tools, their schemas and ground truth, and a pilot of a validator-feedback loop |
| [`tool-call-consistency/`](tool-call-consistency/) | Four extra wordings per request, the 320-call run and the pass^k analysis |
| [`tool-call-reliability-paper/`](tool-call-reliability-paper/) | LaTeX source and PDF of the paper |

Each folder has its own README with the exact commands. Runs use [Ollama](https://ollama.com) locally; tests run without a model:

```bash
cd tool-call-consistency && python3 -m pytest -q
```

## Data

All requests are invented. No patient data were used.

## Citation

See [`CITATION.cff`](CITATION.cff). Code is released under the MIT licence.
