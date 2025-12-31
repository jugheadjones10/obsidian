---
generated-by: life-tag-aggregator
source: "[[Life]]"
tag: teebloc
do-not-edit: true
---

# Teebloc

## 2025-12-29 [[Life#2025-12-29#Teebloc|↩]]

### Answer key cropping
We know that there are many different types of answer keys. Here are the categories encountered so far:
- Grid view, with one column.
	- For this, what if we train a YOLO model to identify all rows, and then we use a light Gemini model to label the question number of rows as well as decide whether each row is a continuation of an existing question or now.
	- Is training a custom YOLO model the only way though? Surely there are good table detector models out there? We just need one that can extract table rows reliably.
		- Paddle has a table cell detector, but upon testing on one of our answer keys we got this output:
		- ![[Pasted image 20251230144242.png|300]]
		- The tricky thing about answer key tables is that they may contain nested tables, which seems to confuse the more "classic" table recognisers.
- Grid view, with two columns.
	- Similar approach to one column, except we might need to train a different YOLO model?
- Similar to questions, except with the answers filled in.
