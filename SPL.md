# 📚 Splunk SPL (Search Processing Language) - Notes
# 1. What is SPL?
SPL stands for Search Processing Language.

It's the language you use in Splunk to search, filter, analyze, visualize, and transform your data.

Think of it like SQL for Splunk — but for machine data!

# 2. SPL Structure
A basic SPL query structure:

php-template
Copy
Edit
<search> | <pipeline of commands> | <visualization>
Example:

ini
Copy
Edit
index=web_logs status=404 | stats count by host | sort -count
# 3. Types of SPL Commands

Command Type	Purpose	Example
Search	Find specific events	index=main error
Transforming	Transform event data into tables	stats count by host
Filtering	Narrow down events	where status=500
Formatting	Rename, reformat fields	rename userID as User_ID
Data Enrichment	Add new fields or data	eval duration=end-start
Sorting	Sort results	sort -count
Grouping	Group results based on fields	dedup user_id

# 4. Commonly Used SPL Commands
# 🔎 Search & Filter
search → Search for keywords

where → Conditional filtering (like SQL WHERE)

# 📊 Transforming
stats → Aggregate statistics (sum, count, avg)

timechart → Time-series chart

top → Find top values

rare → Find rare values

# ✍️ Eval (Calculations)
eval → Create new fields or do calculations

Example: eval total=price*quantity

# 🔀 Event Manipulation
dedup → Remove duplicate events

sort → Sort results

fields → Include/exclude fields

table → Display fields in a table

# 🧹 Clean Data
rex → Extract fields using regex

spath → Extract fields from JSON/XML

replace → Replace field values

# 📈 Reporting & Visualization
chart → Create multi-series charts

eventstats → Adds stats to events without transforming the result

streamstats → Rolling calculations

# 5. Important Concepts
Pipelines (|) → Connect multiple commands together.

Fields → Data keys extracted from events (e.g., host, source, status).

Time Range → Splunk searches are time-bound by default (last 24 hours, etc.)

# 🎯 SPL Example Queries

Purpose	SPL Query Example
Count errors	`index=main error
Top 5 URLs	`index=web_logs
Events over time	`index=app_logs
Find slow transactions	`index=txn_logs duration>5
Calculate success rate	`index=api_logs
# 🔥 Bonus: SPL Tips
Always start with a broad search, then filter down.

Use index and sourcetype early in the query for better speed.

Try to transform and reduce data as early as possible (to minimize resource usage).

