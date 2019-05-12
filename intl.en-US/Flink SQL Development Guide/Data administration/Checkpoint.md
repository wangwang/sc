# Checkpoint {#concept_62485_zh .concept}

Realtime Compute provides a fault tolerance mechanism that allows you to restore data streams. This mechanism ensures that the data streams are consistent with the application. The core of this fault tolerance mechanism is to continuously create consistent snapshots for distributed data streams and their statuses. These snapshots act as consistency checkpoints for rollback in case of system failure.

## Completed Checkpoints {#section_tbc_dwr_bgb .section}

On this tab, you can view checkpoints that have been completed. The following table describes the parameters on this tab.

|Name|Description|
|----|-----------|
|ID|The ID of the checkpoint.|
|StartTime|The time when the checkpoint is created.|
|Durations\(ms\)|The time that is spent on creating the checkpoint.|

## Task Latest Completed Checkpoint {#section_lrm_fwr_bgb .section}

On this tab, you can view the detailed information about the latest checkpoint. The following table describes the parameters on this tab.

|Name|Description|
|----|-----------|
|SubTask ID|The ID of the subtask.|
|State Size|The size of the checkpoint.|
|Durations\(ms\)|The time that is spent on creating the checkpoint.|

