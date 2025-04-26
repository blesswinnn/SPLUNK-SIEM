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


# 📘 Sample SPL Queries
## 🔍 Basic Search Queries
    index=main error
→ Finds all events with the keyword "error" in the main index.
    
    index=web_logs status=404
→ Shows events where HTTP status is 404 (Not Found).

## 📊 Aggregation & Statistics
    index=web_logs | stats count by status
→ Counts number of events grouped by HTTP status code.


    index=syslog | stats avg(cpu_usage) by host
→ Shows average CPU usage per host.

## 📈 Time-based Analysis
    index=app_logs | timechart span=1h count
→ Number of events per hour.

    index=web_logs | timechart avg(response_time) by host
→ Average response time by host over time.

## 🧠 Top & Rare Values

    index=web_logs | top limit=5 url
→ Top 5 most accessed URLs.

    index=web_logs | rare user_agent
→ Rarely used user agents.

## 🛠️ Using Eval for Calculations

    index=sales | eval total_price=quantity*price | stats sum(total_price) by region
→ Calculates total sales amount by region.

    index=logins | eval login_time=strptime(_time, "%Y-%m-%d %H:%M:%S") | table user login_time
→ Converts time format and displays login times.

## 🧹 Field Extraction & Filtering
    index=access_logs | rex "user=(?<username>\w+)" | table _time, username
→ Extracts username using regex.

    index=transactions | where amount > 1000
→ Filters events where amount is greater than 1000.

## 🧾 Working with Tables
    index=web_logs | table _time, host, status, url
→ Displays selected fields in a table format.

    index=error_logs | fields - _raw, source
→ Removes unnecessary fields from results.

## 🔁 Joins and Subsearches
    index=orders order_status="failed" [ search index=users region="US" | fields user_id ]
→ Finds failed orders by users in the US.

## 🔄 Deduplication and Sorting
    index=logins | dedup user_id | sort -_time
→ Shows only the latest login event per user.

##  🧮 Running Totals
    index=transactions | streamstats sum(amount) as running_total by account_id
→ Running total of transaction amounts per account.



