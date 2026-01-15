🎬 Distributed AI Movie Poster Generator
An automated pipeline that leverages Parallel Distributed Computing principles to synthesize cinematic marketing assets from a Neo4j Graph Database.

🧠 System Architecture
The system utilizes an asynchronous, parallel-worker architecture orchestrated via n8n. This design minimizes total execution time by running independent tasks simultaneously.

Data Layer: Neo4j (Cypher) provides structured movie metadata (Title, Plot, Cast) as the single source of truth.

Orchestration Layer: n8n manages the data flow, task distribution, and logic gates.

Compute Layer (Parallel):

Worker A (NLP): Processes the movie plot to generate a snappy, 2-sentence Discord summary.

Worker B (Visual): Synthesizes a high-fidelity theatrical poster with dynamic typography and movie-specific aesthetics.

Synchronization Barrier: An n8n Merge Node (Combine by Position) handles the latency gap between the fast text worker and the slower image generation worker, ensuring the final payload is unified.

Sink: The synchronized results are dispatched to a Discord Webhook.

🚀 Key Technical Features
Prompt Engineering: Optimized "Master Prompts" that ensure high-fidelity typography and prevent AI-generated gibberish on the poster.

Data Marshaling: Dynamically transforming raw Graph nodes (Arrays and Strings) into natural language instructions for LLMs using n8n expressions.

Latency Management: Implementing a join-synchronization pattern to handle the 10x latency difference between text and image APIs.

🛠️ Repository Structure
README.md: Project overview and architecture.

workflows/movie_posters.json: The full n8n workflow export (ready to import).

database/init.cypher: The Neo4j initialization script to build the schema.

assets/Capture.JPG: Visual map of the n8n logic.

🏁 Setup Instructions
Database: Run the init.cypher script in your Neo4j browser to create constraints and sample movies.

Workflow: Import movie_posters.json into n8n.

Credentials: Connect your Neo4j, OpenAI, and Discord Webhook credentials.

Execute: Trigger the workflow to generate a new poster and review in Discord.
