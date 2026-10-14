# Arabic Retrieval Starter Kit

A small, fully synthetic Arabic and English retrieval and RAG evaluation fixture from [Bayanat Labs](https://www.bayanatlabs.com). Use it to test an Arabic search or RAG pipeline and its scoring setup before you build an evaluation set on your own documents.

[Project page](https://www.bayanatlabs.com/research/arabic-retrieval-starter-kit) · License CC BY 4.0 · Version v0.1 (2026-10-05)

## What is in it

The kit covers the cases that trip up Arabic enterprise search:

- Gulf colloquial and MSA questions
- Arabic questions with English terms
- Arabic questions over English documents, and the reverse
- Superseded policy versions and rules for a different customer group, as hard negatives
- Partly answerable and unanswerable questions

Twelve passages and twelve queries are enough to test a pipeline and a scoring setup, not to rank systems. It is not a benchmark, not customer data and not a sample of a Bayanat Labs commercial dataset. Everything was written by Bayanat Labs for this kit, and the company, policies and numbers are fictional.

## Limitations

The grades are single-author judgments written with the fixture, so no reviewer agreement is reported. A real project measures and reports disagreement between reviewers.

## Files

The release files are in [`v0.1/`](v0.1/) and match the copies on bayanatlabs.com byte for byte.

| File | Contents |
| --- | --- |
| `corpus.jsonl` | 12 passages with language, version, effective date, status (current or superseded), customer group and provenance |
| `queries.jsonl` | 12 queries with language, variety, script and a note |
| `qrels.txt` | TREC qrels (`query_id 0 doc_id grade`); unjudged passages count as not relevant |
| `judgments.jsonl` | The same judgments with a reason code for each |
| `answers.jsonl` | Expected grounded answers, evidence quotes, answerability, and passages a faithful answer must not use |
| `README.md` | Field-level documentation |
| `SHA256SUMS.txt` | Checksums for every file above |

Relevance grades: 3 answers the query directly, 2 answers part of it, 1 is on topic but does not answer, 0 is not relevant (including the hard negatives).

## Quickstart

```bash
git clone https://github.com/Bayanat-Labs/arabic-retrieval-starter-kit.git
cd arabic-retrieval-starter-kit/v0.1
shasum -a 256 -c SHA256SUMS.txt
```

1. Index `corpus.jsonl` with your retriever, run the 12 queries and write a TREC run file.
2. Score the run against `qrels.txt` with trec_eval, pytrec_eval or ir_measures. For example nDCG@10, and Recall@5 counting only grades 2 and 3 (`trec_eval -l 2`). Report the unanswerable queries separately.
3. Generate answers from the top passages and check them against `answers.jsonl`. A good answer matches the evidence, avoids the `must_not_use` passages, and declines or asks for detail on Q08 and Q09.

Report retrieval and answer results separately. A system can find the right passage and still answer from the old version.

## Retrieval data for your own documents

Bayanat Labs builds [Arabic retrieval and RAG data](https://www.bayanatlabs.com/products/search) on your own documents. The usual first step is a [pilot](https://www.bayanatlabs.com/pilot).

## Cite

Bayanat Labs (2026). Arabic Retrieval Starter Kit v0.1. https://www.bayanatlabs.com/research/arabic-retrieval-starter-kit

GitHub's "Cite this repository" button gives APA and BibTeX from [CITATION.cff](CITATION.cff).

## License

[CC BY 4.0](LICENSE). Copyright 2026 Bayanat Labs. The Bayanat Labs name and logo are not licensed.

## Contact

Open an issue, or email [hello@bayanatlabs.com](mailto:hello@bayanatlabs.com).

---

### About Bayanat Labs

[Bayanat Labs](https://www.bayanatlabs.com) is a Riyadh-based Arabic data company for AI. We work only on data, from sourcing and annotation to alignment and evaluation, across 25+ Arabic varieties, with vetted native speakers, linguists and licensed domain professionals.

[Run a pilot](https://www.bayanatlabs.com/pilot) · [Datasets](https://www.bayanatlabs.com/products) · [LinkedIn](https://www.linkedin.com/company/bayanat-labs/) · [hello@bayanatlabs.com](mailto:hello@bayanatlabs.com)
