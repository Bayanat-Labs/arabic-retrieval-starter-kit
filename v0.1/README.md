# Arabic Retrieval Starter Kit v0.1 (synthetic)

Bayanat Labs, 2026-10-05. License: CC BY 4.0 (see LICENSE.txt).

A small, fully synthetic Arabic/English retrieval and RAG evaluation fixture. It shows the
format and the failure cases that matter in Arabic enterprise search: Gulf colloquial and MSA
questions, Arabic questions with English terms, Arabic questions over English documents (and the
reverse), superseded policy versions, rules for a different customer group, partly answerable
questions and unanswerable questions.

Everything here was written by Bayanat Labs for this kit. The company, policies and numbers are
fictional. It is not a sample of a Bayanat commercial dataset, not customer data and not a
benchmark: 12 passages and 12 queries are enough to test a pipeline and a scoring setup, not to
rank systems.

## Files

- corpus.jsonl: 12 passages. doc_id, lang, title, version, effective_date, status
  (current or superseded), customer_group, text, provenance; superseded_by / translation_of where relevant.
- queries.jsonl: 12 queries. query_id, lang, variety, script, text, note.
- qrels.txt: TREC qrels (query_id 0 doc_id grade). Unjudged passages count as not relevant.
- judgments.jsonl: the same judgments with a reason code for each.
- answers.jsonl: expected grounded answer, evidence quotes (exact substrings of the passage text),
  answerable (true, "partial", false), expected_behavior for unanswerable queries, and
  must_not_use (passages a faithful answer must not rely on).

## Relevance grades

3 direct evidence that answers the query; 2 answers part of it; 1 on topic but does not answer;
0 not relevant, including hard negatives (superseded version, other customer group).

## Using it

1. Index corpus.jsonl with your retriever; run the 12 queries; write a TREC run file.
2. Score the run against qrels.txt with a standard tool such as trec_eval, pytrec_eval or
   ir_measures (for example nDCG@10, and Recall@5 counting only grades 2 and 3:
   `trec_eval -l 2`). Report the unanswerable queries separately.
3. Generate answers for the top passages and score them separately against answers.jsonl:
   does the answer match the evidence, does it avoid must_not_use passages, and does it decline
   or ask for detail on Q08 and Q09?

Report retrieval and answer results separately: a system can find the right passage and still
answer from the old version.

## Citation

Bayanat Labs (2026). Arabic Retrieval Starter Kit v0.1. https://www.bayanatlabs.com/research/arabic-retrieval-starter-kit

## Contact

hello@bayanatlabs.com. For retrieval data built on your own documents: https://www.bayanatlabs.com/products/search
