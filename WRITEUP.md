## AI vs rules:

Q. Which steps in my flow use AI ?

A. AI does one step only, it reads each proposal and fills the form built from the admin’s criteria, with a quote and page for every answer.
Reason: using plain search or exact rules would'nt be a good fit for this step, as proposals can mention the criteria in different forms

Q. Which are plain code or rules?

A. Plain code does everything else: file checks, reading the PDF (parser, then OCR for scans), building the form, checking that quotes really exist, mandatory pass/fail, scoring, ranking and logging.

Q. Why did I draw the line here?

A. Rule: If something scores people or removes them, it must be consistent and explainable, so it should be code, not AI.

## Consistency and explainability

Q. How do I make scores repeatable and explainable?

A. Scores are calculated based on facts which are taken from each bid,then turned into a number by a fixed rule.

Q. If the same proposals were ranked twice, would the result be the same?

A. Yes. Extraction is run at temperature 0, and results are stored by file and criteria version. So a re-rank reuses the same facts, and the formulas give the same numbers.

## Human in the loop

Q. Where does a person review, confirm or override the result? What gets
logged for audit?

A. Person is involved at three points:

- Flag queue: Anything the tool can't settle, like D's missing timeline, C's unclear experience window, scanned pages read by OCR, or text that tries to give the system orders.

- Results screen: The reviewer can fix any extracted value (the quote is shown next to it), clear flags, or exclude or include a bidder with a reason. scores recalculate.

- Final decision: A person makes the award. The tool only suggests an order.

Q. What gets logged ?

A. File fingerprint, who uploaded it and when, text method, criteria version, model and prompt version, what the AI extracted, validation results, every override with who, when and why, the ranking shown, and the final decision.

## Changing criteria

Q. What happens if an admin edits the criteria or weights after some proposals have already been scored?

A. criteria are versioned, so an edit creates a new version and old results keep the version they were scored under, labelled as such.

## Risks

Q. What could go wrong with this tool (for example wrong extraction, made-up facts, bias, manipulation, cost), and how does my design guard against each one?

A. Wrong extraction : quotes are checked, answers are validated, and failures go to a person.

Made-up facts: "not found" is allowed, guessing is banned, and no quote means no answer.

Manipulation: the document is just data, the AI can't score, and sneaky notes are flagged but ignored.

Bias: names are hidden, rules are the same for all, and reasons are shown.

Gaps and over-trust: missing data is flagged, not guessed, and a person makes the final call.

Cost: parse first, one call per proposal, small model, caching and batching.

Bad files: scans are marked less certain, and unreadable files stop with a clear message.
