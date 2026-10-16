---
name: dreamtune-compute
description: Discover, launch, connect to and stop Dreamtune GPUs with automatic local SSH access through CLI or local MCP. Use when a user asks to rent a GPU, execute a workload, access a notebook, or manage a Dreamtune machine.
---

Requires the installed Dreamtune package, Node.js 22.20 or later, OpenSSH and a
platform key with compute:read and compute:run scopes and workspace credit.
Configure DREAMTUNE_API_KEY, DREAMTUNE_API_ORIGIN and
DREAMTUNE_REQUEST_TIMEOUT_MS in protected process/client settings. Automatic
local access requires an absolute DREAMTUNE_COMPUTE_STATE_DIRECTORY.
CLI connections require DREAMTUNE_SSH_USER matching the GPU image's account.
Never print the API key or pass it as a command argument.

Choose one launch interface. CLI and local MCP share local key storage when
configured with the same origin, key and state directory. Hosted MCP accepts
public launch inputs and cannot generate keys on the user's computer.

1. Discover with `dreamtune compute catalog` or compute_catalog. Use the returned
   available type/region and explain the hourly rate and continuous billing.
2. With authorization to rent compute, choose a stable launch name for this
   intended rental. Run `dreamtune compute start --name <name> --type <type>
   --region <region>` or advertised start_local_compute with name, instanceType
   and region. These save an SSH key and launch reference locally automatically.
   Do not manually generate keys or create a launch JSON for this path.
3. Repeating identical named input resumes the existing launch. Never choose a
   new name, origin, key, type or region to retry an uncertain attempt. A new
   rental requires an explicitly new name. Never launch the same work through
   another interface. A timeout leaves local access and accepted work intact.
4. Read the returned job ID using `dreamtune compute get <id>` or get_compute_job.
   Check until running/active with an IP within the user's time/rate limits.
   Reading may reconcile incurred usage. Failures remain failures; no busy loops.
5. Connect with `dreamtune compute ssh <id>`. For an explicitly requested remote
   command, use --command. Honor OpenSSH's host-key verification; do not disable
   it or send private-key contents. SSH output is workload output. With local
   MCP, local_compute_connection returns an argv array and key path; execute
   through the local terminal only when requested. It does not open an SSH
   session. Quote paths correctly when constructing terminal commands.
6. For hosted MCP, run `dreamtune compute prepare --name <name> --type <type>
   --region <region>` on the user's computer, or use prepare_local_compute from
   local MCP. This rents nothing. Send only instanceType, region, publicKey and
   idempotencyKey to the hosted create_compute_job tool. Connect with
   `dreamtune compute ssh <id> --name <name>` to link its prepared local access.
7. Retrieve a private notebook link only when requested using `dreamtune compute
   notebook <id>` or compute_notebook. Share only with the requesting user.
8. Stop the authorized machine with `dreamtune compute stop <id>` or
   stop_compute_job. Verify terminated state; a stop request is not confirmation.
   Closing SSH, canceling a CLI request or finishing a script does not stop a GPU.

Keys remain on the original computer. A website key cannot be recovered through
CLI. Missing, damaged, linked or overly accessible local files are errors; never
replace a saved private key to conceal a failure. Preserve state for recovery.
Keep local state private and outside committed projects.

Compute bills recorded runtime at the published rate plus the configured fee.
Do not claim a final provider invoice. Launch failures charge zero; credit or key
budget exhaustion blocks work and requests termination. Do not bypass admission.
