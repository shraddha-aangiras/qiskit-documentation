<span id="qiskit-providers-ibmq-managed-managedjob" />

# qiskit.providers.ibmq.managed.ManagedJob

<span id="undefined" />

`ManagedJob(start_index, experiments_count, job=None)`

Job managed by the Job Manager.

ManagedJob constructor.

**Parameters**

*   **start\_index** (`int`) – Starting index of the experiment set.
*   **experiments\_count** (`int`) – Number of experiments.
*   **job** (`Optional`\[`IBMQJob`]) – Job to be managed, or `None` if not already known.

<span id="undefined" />

`__init__(start_index, experiments_count, job=None)`

ManagedJob constructor.

**Parameters**

*   **start\_index** (`int`) – Starting index of the experiment set.
*   **experiments\_count** (`int`) – Number of experiments.
*   **job** (`Optional`\[`IBMQJob`]) – Job to be managed, or `None` if not already known.

## Methods

|                                                                                                                                                                |                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| [`__init__`](#qiskit.providers.ibmq.managed.ManagedJob.__init__ "qiskit.providers.ibmq.managed.ManagedJob.__init__")(start\_index, experiments\_count\[, job]) | ManagedJob constructor.                      |
| [`cancel`](#qiskit.providers.ibmq.managed.ManagedJob.cancel "qiskit.providers.ibmq.managed.ManagedJob.cancel")()                                               | Attempt to cancel the job.                   |
| [`error_message`](#qiskit.providers.ibmq.managed.ManagedJob.error_message "qiskit.providers.ibmq.managed.ManagedJob.error_message")()                          | Provide details about the reason of failure. |
| [`qobj`](#qiskit.providers.ibmq.managed.ManagedJob.qobj "qiskit.providers.ibmq.managed.ManagedJob.qobj")()                                                     | Return the Qobj for this job.                |
| [`result`](#qiskit.providers.ibmq.managed.ManagedJob.result "qiskit.providers.ibmq.managed.ManagedJob.result")(\[timeout, partial, refresh])                   | Return the result of the job.                |
| [`status`](#qiskit.providers.ibmq.managed.ManagedJob.status "qiskit.providers.ibmq.managed.ManagedJob.status")()                                               | Query the server for job status.             |
| [`submit`](#qiskit.providers.ibmq.managed.ManagedJob.submit "qiskit.providers.ibmq.managed.ManagedJob.submit")(qobj, job\_name, backend, executor, …)          | Submit the job.                              |

<span id="undefined" />

`cancel()`

Attempt to cancel the job.

**Return type**

`None`

<span id="undefined" />

`error_message()`

Provide details about the reason of failure.

**Return type**

`Optional`\[`str`]

**Returns**

An error report if the job failed or `None` otherwise.

<span id="undefined" />

`qobj()`

Return the Qobj for this job.

**Return type**

`Union`\[`QasmQobj`, `PulseQobj`, `None`]

**Returns**

The Qobj for this job or `None` if the Qobj could not be retrieved.

<span id="undefined" />

`result(timeout=None, partial=False, refresh=False)`

Return the result of the job.

**Parameters**

*   **timeout** (`Optional`\[`float`]) – Number of seconds to wait for job.
*   **partial** (`bool`) – If `True`, attempt to retrieve partial job results.
*   **refresh** (`bool`) – If `True`, re-query the server for the result. Otherwise return the cached value.

**Return type**

`Optional`\[`Result`]

**Returns**

Job result or `None` if result could not be retrieved.

**Raises**

[**IBMQJobTimeoutError**](qiskit.providers.ibmq.job.IBMQJobTimeoutError#qiskit.providers.ibmq.job.IBMQJobTimeoutError "qiskit.providers.ibmq.job.IBMQJobTimeoutError") – If the job does not return results before a specified timeout.

<span id="undefined" />

`status()`

Query the server for job status.

**Return type**

`Optional`\[`JobStatus`]

**Returns**

Current job status, or `None` if an error occurred.

<span id="undefined" />

`submit(qobj, job_name, backend, executor, submit_lock, job_share_level, job_tags=None)`

Submit the job.

**Parameters**

*   **qobj** (`Union`\[`QasmQobj`, `PulseQobj`]) – Qobj to run.
*   **job\_name** (`str`) – Name of the job.
*   **backend** (`IBMQBackend`) – Backend to execute the experiments on.
*   **executor** (`ThreadPoolExecutor`) – The thread pool used to submit the job.
*   **submit\_lock** (`allocate_lock`) – Lock used to synchronize job submission.
*   **job\_share\_level** (`ApiJobShareLevel`) – Job share level.
*   **job\_tags** (`Optional`\[`List`\[`str`]]) – Tags to be assigned to the job.

**Return type**

`None`