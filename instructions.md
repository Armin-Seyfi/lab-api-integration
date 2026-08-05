# Two brains, zero single point of failure

> **How you'll submit this lab**
>
> This repo is your lab. Fork it, do the work described below in your fork, then open a pull
> request back into this repository. An AI reviewer will check your PR against `rubric.md` and
> leave feedback directly on the PR. See `README.md` for the full workflow.

## Learning Goal

You will build one Multi-Provider News Summarizer workflow path and prove data moves from input to output correctly.

## Working Context

This lab turns a manual handoff into a small automated workflow.
You define one input, one transformation, and one output a reviewer can inspect.
Avoid broad automation. Prove the critical path first.

## Proof of Learning

Submit one `lab_proof.md` with the workflow export or configuration, one execution trace, one input payload, and one output record.

## Pseudocode

```text
INPUT: source event, message, ticket, or payload
DECIDE: required fields, routing rule, and destination
BUILD: trigger -> transform -> action
VERIFY: inspect one successful run and output artifact
EXPLAIN: justify the mapping and operational risk
```

## Prompt Discipline

Use AI for review, debugging, or critique. Do not ask it to produce the final artifact or final answer.

```text
Role: Workflow reviewer
Task: Challenge my event-flow plan before I build or submit.
Inputs: trigger, sample payload, destination schema, and proof plan.
Constraints: Do not build the workflow for me. Find brittle mappings and missing checks.
Output format: three workflow risks, two trace checks, and one simplification.
Verification: Name the execution evidence that proves the workflow ran.
```

## Build

## Part 1: Setup and Environment Configuration

### Step 1: Create Project Structure

Create the following folder structure:

```
news-summarizer/
├── .env
├── .gitignore
├── requirements.txt
├── config.py
├── news_api.py
├── llm_providers.py
├── summarizer.py
├── test_summarizer.py
└── main.py
```

### Step 2: Install Dependencies

Create `requirements.txt`:

```txt
openai>=1.12.0
anthropic>=0.18.0
requests>=2.31.0
python-dotenv>=1.0.0
aiohttp>=3.9.0
tiktoken>=0.5.0
pytest>=7.4.0
```

Install dependencies:

```bash
pip install -r requirements.txt
```

### Step 3: Configure Environment Variables

Create `.env` file (DO NOT commit this!):

```bash
# .env: replace each value with your actual key (do NOT commit this file)
OPENAI_API_KEY=<your key from platform.openai.com>
ANTHROPIC_API_KEY=<your key from console.anthropic.com>
NEWS_API_KEY=<your key from newsapi.org>

ENVIRONMENT=development
MAX_RETRIES=3
REQUEST_TIMEOUT=30
DAILY_BUDGET=5.00
```

Create `.gitignore`:

```
.env
.env.*
__pycache__/
*.pyc
*.pyo
*.log
.pytest_cache/
```

### Step 4: Create Configuration Module

Create `config.py`:

**Checkpoint 1:** Run `python config.py`. It should validate successfully or tell you which keys are missing.

---

## Part 2: News API Integration

### Step 5: Create News API Module

Create `news_api.py`:

**Checkpoint 2:** Run `python news_api.py`. It should fetch and display 3 tech news articles.

---

## Part 3: LLM Provider Integration

### Step 6: Create LLM Providers Module

Create `llm_providers.py`:

Tip: if you are not using the `os` library in this module, this code will need to be adapted.

**Checkpoint 3:** Run `python llm_providers.py`. It should test both providers and show cost tracking.

---

## Part 4: News Summarizer Core Logic

### Step 7: Create Summarizer Module

Create `summarizer.py`:

**Checkpoint 4:** Run `python summarizer.py`. It should fetch 2 articles, summarize them with OpenAI, analyze sentiment with Anthropic, and show a cost summary.

---

## Part 5: Async Processing (Optional Advanced Feature)

### Step 8: Add Async Support for Concurrent Processing (Optional - Advanced)

Add this to `summarizer.py` (below the `NewsSummarizer` class):

Tip: if you are not using `aiohttp` in this version of the summarizer, this code will need to be adapted.

---

## Part 6: Testing

### Step 9: Write Unit Tests

Create `test_summarizer.py`:

**Checkpoint 5:** Run `pytest test_summarizer.py -v`. All tests should pass.

---

## Part 7: Main Application

### Step 10: Create Main Application

Create `main.py`:

**Checkpoint 6:** Run `python main.py`. The interactive application should fetch and process news articles.

---

## Part 8: Deliverables and Submission


### What to Submit

Create a GitHub repository with the following:

1. **All source code files**:
   - `config.py`
   - `news_api.py`
   - `llm_providers.py`
   - `summarizer.py`
   - `test_summarizer.py`
   - `main.py`

2. **Configuration files**:
   - `requirements.txt`
   - `.gitignore`
   - `.env.example` (template without real keys)

3. **Documentation**:
   - `README.md` explaining:
     - What the project does
     - How to set it up
     - How to run it
     - Example output
     - Cost analysis
   - `lab_summary.md` containing **one short paragraph** summarizing challenges, how you solved them, what you learned, and ideas for improvement (**not** a long essay)

4. **Test results**:
   - Screenshot or output of `pytest` passing all tests
   - Screenshot of main app processing 3-5 articles

### Submission Guidelines

1. **Code Quality Checklist**:
   - [ ] All code is well-commented
   - [ ] Functions have docstrings
   - [ ] No API keys committed to git
   - [ ] `.env` is in `.gitignore`
   - [ ] All tests pass
   - [ ] Code follows PEP 8 style guide

2. **Functionality Checklist**:
   - [ ] Fetches news from external API
   - [ ] Uses OpenAI for summarization
   - [ ] Uses Anthropic for sentiment analysis
   - [ ] Implements fallback logic
   - [ ] Tracks API costs
   - [ ] Respects rate limits
   - [ ] Has working unit tests

3. **Submit**:
   - GitHub repository URL (everything above must be in that repo)

---

## Troubleshooting

**Problem**: "Missing required configuration" error
**Solution**: Check that all API keys are set in `.env` file

**Problem**: Rate limit errors
**Solution**: Reduce number of articles or increase wait times in rate limiters

**Problem**: Tests failing
**Solution**: Make sure all dependencies are installed: `pip install -r requirements.txt`

**Problem**: News API returns no articles
**Solution**: Check your News API key, try different category or country

**Problem**: "Budget exceeded" error
**Solution**: Increase `DAILY_BUDGET` in `.env` or process fewer articles

---

## Learning Reflection

*Optional self-check: not part of the graded submission beyond the single paragraph above.*

After completing this lab, reflect on:

1. **Multi-Provider Integration**: How did passing outputs between OpenAI and Anthropic work? What are the benefits?

2. **Fallback Logic**: When did your fallback logic activate? How did it improve reliability?

3. **Cost Tracking**: How much did processing cost? How could you optimize it?

4. **Rate Limiting**: Did you hit any rate limits? How did the rate limiters help?

5. **Code Quality**: How did writing tests help you find bugs? What would you improve?

## Conclusion

You completed! You've built a production-ready multi-provider news summarizer that:

- Integrates with external data sources (News API)
- Uses multiple LLM providers (OpenAI + Anthropic)
- Passes outputs between providers
- Implements fallback logic
- Tracks costs and respects rate limits
- Processes articles efficiently
- Has comprehensive unit tests
- Uses production-ready configuration

You now have the skills to build real-world AI applications that are reliable, efficient, and cost-effective!

## Verify

The reviewer can inspect one run trace and see the observable output in the destination.

## Explain

What is the first failure mode you would monitor if this workflow ran daily?

## Submission Sanity Check

Before you submit:
- Keep only files for this lab.
- Name files clearly.
- Remove secrets, API keys, tokens, and unrelated data.
- Make `lab_proof.md` the entry point for the reviewer.

## Optional Stretch
Want to go further? Try these:

1. **Caching**: Add response caching to avoid re-processing identical articles
2. **Database**: Store processed articles in SQLite database
3. **Web UI**: Create a simple Flask/FastAPI web interface
4. **Scheduling**: Add ability to run automatically on a schedule
5. **Email Reports**: Send daily email summaries
6. **More Providers**: Add Google AI (Gemini) as a third provider
7. **Advanced Analytics**: Calculate trending topics across multiple articles
