---
name: arc-usage-demo
description: Inspect resources, prepare Slurm jobs, and monitor or recover authorized CPU/GPU research workloads on Virginia Tech ARC.
---
# ARC Usage — Demonstration Skill

## Scope and authorization

- Identify the cluster, workload, project allocation, relevant files, and job IDs. This demonstration uses one cluster per workflow.
- Use an allocation authorized for the actual project; FairShare alone does not justify account selection.
- Keep status requests read-only. Before submitting, releasing, cancelling, requeuing, or changing jobs, present the concrete action and obtain explicit approval. Existing approval for that unchanged action remains valid. File changes must stay within the authorized task. [ARC agent guidance](https://docs.arc.vt.edu/ai/040_coding_agents.html)
- Use login nodes for lightweight preparation and management. Run substantial processing and model workloads within Slurm allocations. Release resources when work ends; do not leave interactive allocations idle. [ARC acceptable-use policy](https://docs.arc.vt.edu/usage/01-acceptable-use-policy.html)

## Inspect and diagnose

Run only necessary queries on the selected cluster. Avoid polling loops and per-worker scheduler queries; reuse recent snapshots. Prefer ARC dashboards or requested notifications for ongoing monitoring. [Slurm query guidance](https://slurm.schedmd.com/squeue.html#SECTION_PERFORMANCE)

Choose relevant commands below; replace `JOB_ID` with a verified job belonging to the user:

```bash
sinfo -s
squeue --user="$(id -un)"
scontrol show job --detail JOB_ID
sprio --jobs=JOB_ID
squeue --start --jobs=JOB_ID
sacct --jobs=JOB_ID --format=JobID,State,Elapsed,ExitCode
showqos
```

ARC hides other users' jobs from ordinary job views. Visible queue counts cannot establish cluster-wide demand or queue rank. Respect withheld information. [ARC inspection guidance](https://docs.arc.vt.edu/usage/00faq.html#why-isn-t-my-job-starting)

Distinguish holds, failed dependencies, configuration errors, and allocation limits from ordinary resource waiting. `Priority` or `Resources` alone provides no waiting-time estimate. Label scheduler start estimates as provisional.

An unallocated GPU may be unavailable because of reservations, CPU or memory requirements, or access restrictions. Report missing information as unknown. Priority scores and resource snapshots do not guarantee a start time. [Slurm scheduling](https://slurm.schedmd.com/sched_config.html)

## Prepare and execute

- Benchmark useful work in an approved allocation. Request measured CPU, memory, GPU, and runtime needs within current limits. Do not use dummy jobs, duplicate races, inflated requests, or repeated submission/cancellation to manipulate scheduling.
- Check current partition, QoS, time limits, and billing. Select short-duration QoS only when the application can finish or safely checkpoint within its limit. [ARC job options](https://docs.arc.vt.edu/usage/job_scheduling/02_slurm_options.html)
- Review the complete script, resource request, environment, working directory, workload command, and log paths before submission. Record the cluster and returned job ID. After an ambiguous submission timeout, check whether the job exists before retrying.
- Bundle small tasks or use arrays with bounded concurrency. Assign each task one output owner; reuse model loading and validated batching. Preserve approved model, input, and evaluation settings. [ARC parallel workloads](https://docs.arc.vt.edu/usage/job_scheduling/03_parallel.html)

## Monitor, recover, and report

Check application logs and completed records alongside Slurm status. Use `showjobusage JOB_ID` for running jobs or `seff JOB_ID` for completed jobs where supported.

Retry only unfinished work under an approved retry count and resource budget. Preserve checkpoints and failure history; stop unexplained recurring failures. Use `--time-min` or preemptable execution only with tested recovery. `--requeue` does not implement application checkpointing. [Slurm job options](https://slurm.schedmd.com/sbatch.html)

Operate on exact approved job IDs; protect unrelated jobs and live interactive sessions. Validate output coverage, format, and duplicates before declaring completion.

Report observation time, cluster, job IDs, blockers, application progress, and actions taken. Base compute estimates on measured throughput; report unknown queue delay explicitly.

## Data and storage

Access only task-authorized files. Keep credentials out of commands, scripts, scheduler exports, and logs. Use shared model caches when suitable. Keep durable results in approved persistent storage; treat scratch as temporary and respect cleanup rules. Delete only approved task-owned files. [ARC storage guidance](https://docs.arc.vt.edu/usage/01-acceptable-use-policy.html#best-practices-for-storage-management)
