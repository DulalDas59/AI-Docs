Epic	Feature	Type	Story / Task	Acceptance / Output	Dependency	Owner	Size	Build Weeks	Buffer	Total
Foundation	Layer C boundary	HLD	Freeze Planner / Supervisor / Orchestrator boundaries and lifecycle	Approved architecture note and sequence flow	None	Architecture	S	0.5	0	0.5
Foundation	Contracts	LLD	Define RequestEnvelope, ExecutionPlan, TaskNode, StateCheckpoint, SupervisorDecision, ReplanRequest	Versioned Pydantic models and JSON schema exports	Layer C boundary	Engineering	M	1	0.5	1.5
Planner	Prompt & I/O design	LLD	Design planner input/output rules, plan versioning, prompt templates, and plan metadata	Planner LLD package and prompt files	Contracts	Architecture	S	0.5	0	0.5
Planner	Deterministic planner	Build	Implement deterministic planner for benchmark flows and template-driven intents	Working deterministic planner module	Planner prompt & I/O design	Engineering	M	1	0	1
Planner	LLM planner	Build	Implement structured-output planner backend through provider adapter	Planner emits schema-constrained ExecutionPlan objects	Deterministic planner	Engineering	L	2	0.5	2.5
Planner	Plan validator	Build	Implement DAG validation, normalization, and plan version manager	Validator catches cycles, missing fields, and dependency issues	LLM planner	Engineering	M	1	0.5	1.5
Planner	Replan entry point	Build	Implement replan flow using partial state and failure reason	Replan API returns versioned replacement plan	Plan validator	Engineering	M	1	0	1
Supervisor	Decision policy	LLD	Design thresholds, decision enums, escalation payloads, and config model	Supervisor LLD and config package	Contracts	Architecture	S	0.5	0	0.5
Supervisor	State reader	Build	Implement state reader over real execution checkpoints	Supervisor consumes StateCheckpoint and execution events	Decision policy	Engineering	M	1	0	1
Supervisor	Decision engine	Build	Implement continue / re-plan / escalate / stop logic	Supervisor emits governed decisions from execution state	State reader	Engineering	L	2	0.5	2.5
Supervisor	Conflict / failure detector	Build	Add low-confidence, repeated-failure, and conflict detection	Conflict/failure triggers connected to decision engine	Decision engine	Engineering	M	1	0	1
Integration	Orchestrator handshake	Build	Implement minimal runtime adapter for task transitions and supervisor checkpoints	Planner and Supervisor integrated into execution loop	Planner + Supervisor core	Engineering	L	2	0.5	2.5
Observability	Trace model	Build	Instrument plan events, state transitions, validation failures, and decisions	OpenTelemetry spans and structured logs available	Orchestrator handshake	Platform	M	1	0	1
Quality	Release tests	QA	Create golden workflows, negative-path tests, and integration suite	Release 1 test pack passes	Trace model	Engineering	M	1	0.5	1.5
Deployment	Dev/test baseline	DevOps	Containerize services and deploy to dev/test runtime	Docker image and Azure Container Apps baseline	Release tests	Platform	M	1	0.5	1.5