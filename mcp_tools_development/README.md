# Developing MCP Tools

The **`mcp_tools_development`** folder documents the process of designing and prototyping **MCP tools** based on structured content data (events, articles, and blog posts).
The goal is to enable a language model to answer analytics-style questions reliably by routing them to the correct tool.

---

## Table of Contents

[1. Data Preparation](#1-data-preparation)

- [1.1. Download Data](#11-download-data)
- [1.2. Clean Data](#12-clean-data)

[2. Preparing MCP Tools](#2-preparing-mcp-tools)

- [2.1. What Kind of Questions Are Possible?](#21-what-kind-of-questions-are-possible)
- [2.2. Raw Question Set](#22-raw-question-set)

[3. Polishing the Questions](#3-polishing-the-questions)

[4. How to Organize MCP Tools?](#4-how-to-organize-mcp-tools)

- [4.1. Aggregator Tools](#41-aggregator-tools)
- [4.2. Analyst Tools](#42-analyst-tools)
- [4.3. Thematic Finder Tools](#43-thematic-finder-tools)

[5. Mapping Questions to MCP Tool Groups](#5-mapping-questions-to-mcp-tool-groups)

[6. Making Hands Dirty](#6-making-hands-dirty)

---

## 1. Data Preparation

### 1.1. Download Data

The following datasets were downloaded as a **JSON** files:

- Events
- Articles
- Blog posts

### 1.2. Clean Data

After downloading, the data was cleaned and normalized to ensure:

- Consistent date formats
- Structured categories and tags
- Reliable numeric fields (attendance, views, likes, waitlist counts)

---

---

## 2. Preparing MCP Tools

### 2.1. What Kind of Questions Are Possible?

As a next step, a set of analytics questions was formulated based on the available data.

### 2.2. Raw Question Set

#### Events

- How many events all time?
- Which year has the most events organized?
- How many events in a given year?
- Total attendance across all time?
- How many online or venue events in all time?
- How many online or venue events in a given year?
- Most visited events all time?
- Most visited events in a given year?
- How many events for a given category in all time?
- How many events for a given category in a given year?
- Most visited events for a given category in all time?
- Most visited events for a given category in a given year?
- Which events had the highest "Waitlist" count?
- High-demand events (highest waitlist) in a given year

---

#### Articles

- How many articles all time?
- Which year has the most articles published?
- How many articles in a given year?
- Which is the most active month in a specific year?
- How many articles for a given category?
- How many articles for a given tag?
- Which months have the most publications?
- What is the total list of unique tags used across the whole site?
- Which tags are used most often?

---

#### Blog Posts

- How many blog posts all time?
- Which year has the most blog posts published?
- How many blog posts in a given year?
- Which is the most active month in a specific year?
- How many blog posts for a given category?
- How many blog posts for a given tag?
- Which months have the most publications?
- What is the total list of unique tags used across the whole site?
- Highest views & likes (all time)
- Highest views & likes (in a specific year)
- Category with highest average views
- Who are the authors?
- How many blog posts do the authors have? (Count per author)
- Posts by a specific author

---

---

## 3. Polishing the Questions

Using an LLM, the raw questions were:

- rewritten with **uniform phrasing**
- clarified for **clear intent**
- grouped into a structure resembling an **analytics specification or dashboard query list**

### 📅 Events Analytics – Properly Formulated Questions

#### General

- What is the total number of events organized to date?
- Which year had the highest number of events?
- How many events were organized in a given year?
- What is the total attendance across all events to date?

#### Event Format

- How many online events have been organized to date?
- How many venue-based (in-person) events have been organized to date?
- How many online vs. venue-based events were organized in a given year?

#### Popularity / Attendance

- Which events have the highest attendance of all time?
- Which events had the highest attendance in a given year?

#### Categories

- How many events were organized for a given category across all time?
- How many events were organized for a given category in a specific year?
- Which events are the most attended within a given category of all time?
- Which events are the most attended within a given category in a specific year?

#### Demand / Waitlist

- Which events have the highest waitlist counts of all time?
- Which events had the highest waitlist counts in a given year?

---

### 📰 Articles Analytics – Properly Formulated Questions

#### General

- What is the total number of articles published to date?
- Which year had the highest number of published articles?
- How many articles were published in a given year?

#### Time-Based Activity

- Which month was the most active in a specific year?
- Which months have the highest number of article publications overall?

#### Categories & Tags

- How many articles were published for a given category?
- How many articles were published for a given tag?
- What is the complete list of unique tags used across the site?
- Which tags are used most frequently?

---

### ✍️ Blog Posts Analytics – Properly Formulated Questions

#### General

- What is the total number of blog posts published to date?
- Which year had the highest number of blog posts published?
- How many blog posts were published in a given year?

#### Time-Based Activity

- Which month was the most active in a specific year?
- Which months have the highest number of blog post publications overall?

#### Categories & Tags

- How many blog posts were published for a given category?
- How many blog posts were published for a given tag?

#### Engagement

- Which blog posts have the highest number of views and likes of all time?
- Which blog posts have the highest number of views and likes in a specific year?
- Which category has the highest average number of views per post?

#### Authors

- Who are the blog post authors?
- How many blog posts has each author published?
- Which blog posts were written by a specific author?

---

---

## 4. How to Organize MCP Tools?

After brainstorming, three main MCP tool categories were identified.

### 4.1. Aggregator Tools

**Goal:**
Answer questions like:

- “How many events were organized in 2024?”
- “How many articles were published in December 2023?”

**Pandas logic**

- Filter by date
- Return simple counts

---

### 4.2. Analyst Tools

**Goal:**
Answer questions like:

- “What was the total attendance in 2025?”
- “Which event was the most popular?”

**Pandas logic**

- Perform sums, averages, and rankings

---

### 4.3. Thematic Finder Tools

**Goal:**
Answer questions like:

- “What articles do we have about nutrition (Táplálkozás)?”
- “Show me posts with the #ManóDuma tag.”

**Pandas logic**

- Filter content and return **lists of relevant items**, not metrics.

---

---

## 5. Mapping Questions to MCP Tool Groups

Using the polished questions, each one was mapped to the most appropriate MCP tool group.

### 🧮 Aggregator Tools

**Goal:**
Simple counts after filtering

#### 📅 Events — Aggregators

- What is the total number of events organized to date?
- Which year had the highest number of events?
- How many events were organized in a given year?
- How many online events have been organized to date?
- How many venue-based (in-person) events have been organized to date?
- How many online vs. venue-based events were organized in a given year?
- How many events were organized for a given category across all time?
- How many events were organized for a given category in a specific year?

#### 📰 Articles — Aggregators

- What is the total number of articles published to date?
- Which year had the highest number of published articles?
- How many articles were published in a given year?
- Which month was the most active in a specific year?
- Which months have the highest number of article publications overall?
- How many articles were published for a given category?
- How many articles were published for a given tag?

#### ✍️ Blog Posts — Aggregators

- What is the total number of blog posts published to date?
- Which year had the highest number of blog posts published?
- How many blog posts were published in a given year?
- Which month was the most active in a specific year?
- Which months have the highest number of blog post publications overall?
- How many blog posts were published for a given category?
- How many blog posts were published for a given tag?
- Who are the blog post authors?
- How many blog posts has each author published?

---

### 📊 Analyst Tools

**Goal:**
Sums, rankings, averages, popularity

#### 📅 Events — Analysts

- What is the total attendance across all events to date?
- Which events have the highest attendance of all time?
- Which events had the highest attendance in a given year?
- Which events are the most attended within a given category of all time?
- Which events are the most attended within a given category in a specific year?
- Which events have the highest waitlist counts of all time?
- Which events had the highest waitlist counts in a given year?

#### ✍️ Blog Posts — Analysts

- Which blog posts have the highest number of views and likes of all time?
- Which blog posts have the highest number of views and likes in a specific year?
- Which category has the highest average number of views per post?

---

### 🧭 Thematic Finder Tools

**Goal:**
Filter by tags, categories, and authors

#### 📅 Events — Thematic Finders (Optional)

- What events are available for a given category?
- What events were organized in a given year?
- What online events are available?
- What venue-based events are available?

#### 📰 Articles — Thematic Finders

- What articles are available for a given category?
- What articles are available for a given tag?
- What is the complete list of unique tags used across the site?
- Which tags are used most frequently?

#### ✍️ Blog Posts — Thematic Finders

- What blog posts are available for a given category?
- What blog posts are available for a given tag?
- Which blog posts were written by a specific author?

---

**Note**: Mental Shortcut for Future Tools
When adding a new MCP tool, ask:

- **Is the answer a number?** → Aggregator
- **Is the answer a ranked or summed metric?** → Analyst
- **Is the answer a list of content?** → Thematic Finder

---

---

## 6. Making Hands Dirty

After the design phase, a **Jupyter Notebook** was used to prototype the MCP tools.
A simple implementation was chosen first, then gradually refactored into code suitable for use inside the `server.py` file.

This approach allowed fast iteration while keeping the final MCP tools clean and production-ready.
