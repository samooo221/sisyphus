---
type: moc
code: LOG101
course: Introduction to Logic Circuits (invented course)
tags: [university, moc]
created: 2026-03-01
exam:
  final_total: 40
  time_min: 60
  time_status: verified
  corpus: ../sample-corpus/LOG101   # sample only: in real use the corpus lives outside the vault and every repo
  topics:
    - {name: number-systems, weight: skim}
    - {name: boolean-algebra, weight: invest}
    - {name: karnaugh-maps, weight: invest}
    - {name: flip-flops}
  sections:
    - {id: final, total: 40, questions: 4, question_points: [8, 10, 12, 10]}
  gates:
    - {scope: exam, min_points: 16, on_fail: zero_exam}
---
# LOG101: Introduction to Logic Circuits

An invented course for the sample vault. It does not match any real university course.

## Topics
- number-systems: binary, decimal, conversion
- boolean-algebra: laws, simplification
- karnaugh-maps: minimal sum of products
- flip-flops: D and T behaviour, toggling

## Flashcards
- [[LOG101 — flashcards]]
