# Technical Decisions

This case study highlights architecture and engineering judgment without exposing the private implementation.

| Decision area | Choice | Why it mattered |
| --- | --- | --- |
| Product architecture | Role-separated candidate and recruiter surfaces. | Keeps ownership, permissions, and user intent clear. |
| Application layer | Next.js and Node.js for web and workflow orchestration. | Supports fast iteration across UI and server-side product logic. |
| Data platform | Supabase and PostgreSQL for auth-aware relational workflows. | Fits structured profiles, recruiter workflows, and permission-sensitive data. |
| Profile model | Convert student work into structured candidate records. | Makes search and matching more evidence-based than resume text alone. |
| Matching architecture | Combine hard constraints, metadata, evidence signals, and embeddings. | Balances deterministic filtering with semantic role fit. |
| AI boundary | Use AI to assist structuring and matching, not to own the entire decision. | Keeps recruiter judgment central and reduces black-box behavior. |
| Public export | Document architecture with sanitized diagrams and exclusions. | Demonstrates technical depth while protecting production details. |

## Design Posture

- Make the system understandable at the layer level.
- Keep privileged operations and sensitive data out of the public narrative.
- Show enough architecture to demonstrate engineering maturity.
- Omit exact mechanics that would expose private business logic or security-sensitive implementation.
