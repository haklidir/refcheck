# refcheck

A small Colab notebook that checks the reference list of a manuscript. It extracts the references from a PDF with [GROBID](https://github.com/kermitt2/grobid), then looks each one up in OpenAlex, Crossref, PubMed and Europe PMC. For every reference the best candidate from each source is scored on title similarity (token sort ratio), first-author surname and year; the highest score decides the verdict.

The output is `reference_check_results.csv` with one row per reference: the extracted title, first author and year, the best source and its score, the verdict, the matched title, year, DOI and identifier, and the per-source scores.

| Score | Verdict |
|---|---|
| 80 and above | high confidence, most likely correct |
| 60 to 79 | medium confidence, minor mismatches possible |
| 1 to 59 | low confidence, doubtful |
| 0 | no match, very doubtful |

A low score does not prove that a reference is wrong; it marks the references worth checking by hand, which is the point of the tool.

## Running

Open `refcheck.ipynb` in Google Colab and run the cells in order. The first cell installs Java 21, builds the GROBID service from source and starts it in the background; allow several minutes before the health check passes. Then upload the PDF when asked. Replace `youremail@example.com` in the `mailto` and `email` arguments with your own address, which the APIs use to identify polite clients.

## License

MIT, see `LICENSE`.
