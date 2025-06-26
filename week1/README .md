# README: Week 1 - LLM Zoomcamp (Summary)

This README summarizes the `week1_intro.ipynb` notebook from Week 1 of the **LLM Zoomcamp**, focusing on using **Elasticsearch** to index and search course FAQs, building LLM prompts, and counting tokens. It includes instructions for running Elasticsearch with Docker.

---

## Summary
The notebook covers:
- **Elasticsearch**: Set up and query a local instance.
- **Indexing**: Store FAQs from `documents.json` in an Elasticsearch index.
- **Searching**: Query with boosting and filtering.
- **Prompt Building**: Create LLM prompts from search results.
- **Tokenization**: Count tokens using `tiktoken`.

### Questions
1. **Q1: Run Elasticsearch**
   - Task: Run Elasticsearch 8.4.3 and get `version.build_hash`.
   - Answer: `42f05b9372a9a4a470db3b52817899b99a76ee73`.
2. **Q2: Indexing Data**
   - Task: Index FAQs with `course` as `keyword`, others as `text`. Identify the function.
   - Answer: `index`.
3. **Q3: Searching**
   - Task: Search "How do execute a command on a Kubernetes pod?" with `question` boosted by 4. Get top `_score`.
   - Answer: `44.50556` (~44.50).
4. **Q4: Filtering**
   - Task: Search "How do copy a file to a Docker container?" for `machine-learning-zoomcamp`. Get third question.
   - Answer: "How do I copy files from a different folder into docker container’s working directory?"
   - Note: Fix bug in Q4: Use `search_query_filtered` in `es_client.search`.
5. **Q5: Building a Prompt**
   - Task: Build prompt with Q4 results. Calculate length.
   - Answer: `1917` (~1946).
6. **Q6: Tokens**
   - Task: Count tokens in Q5 prompt for `gpt-4o`.
   - Answer: `448` (~420).

---

## Running Elasticsearch
Run Elasticsearch 8.4.3 using Docker:

```bash
docker run -it \
    --rm \
    --name elasticsearch \
    -p 9200:9200 \
    -p 9300:9300 \
    -e "discovery.type=single-node" \
    -e "xpack.security.enabled=false" \
    elasticsearch:8.4.3
```

### Docker Command Details
- Maps ports `9200` (HTTP) and `9300` (transport).
- Runs as a single node with security disabled.
- Auto-removes container on exit.

### Prerequisites
- **Docker**: Install and ensure it’s running.
- **Python Libraries**: Install `requests`, `elasticsearch`, `tqdm`, `tiktoken` (`pip install requests elasticsearch tqdm tiktoken`).
- **Python**: Use 3.8+ (notebook uses 3.12.7).
- **Dataset**: Fetched from GitHub (`documents.json`).

### Steps
1. Run the Docker command to start Elasticsearch.
2. Verify with `curl localhost:9200` or `es_client.info()`.
3. Execute notebook cells in order.
4. Fix Q4 bug: Use `search_query_filtered` for filtering.
5. Check outputs against provided answers.

---

## Recommendations
- Ensure port `9200` is free.
- Run cells sequentially to avoid errors.
- Validate search results and prompt format.
- Use `tiktoken` to explore tokenization.
- Debug issues with `docker logs elasticsearch`.

This concise summary covers the Week 1 homework and Docker setup for Elasticsearch. Refer to course materials for more details.