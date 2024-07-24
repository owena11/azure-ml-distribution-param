
## Introduction

This is the minimal example we can produce of AzureML not following the full
parameters set within the Pipeline when utilising a PipelineComponent to
parameterise the distribution of jobs using the built in distribution features.

- `small-train.yaml` - A pipeline parameterised to run on a single GPU.
- `bigger-train.yaml` -  A pipeline parameterised to run on 4 GPUs with a
   process per gpu.
- `bigger-train.yaml` -  A pipeline parameterised to run on 4 GPUs with a
   process per gpu.
- `train_val_pipeline_component.yaml` - A pipelineComponent that is
  parameterised to allow us to call it with different compute clusters and
  distributions.
- `component/azure-ml-component.yaml` - A dummy component that just prints
  something  to stdout.

## Prerequisites

Azure Infrastructure:
- Azure ML workspace in relevant resource group
- A compute cluster within AzureML called `A100x4`
- A compute cluster within AzureML called `A100x1`


## Commands submitted

For the small pipeline...

Command:
```
az ml job create -f small-train.yaml  -g <resource_group>  -w <workspace>
```

Expected Result:

Job running on compute cluster A100x1, spawning 1 process.

Actual Result:

Job running on compute cluster A100x1, spawning 4 process.


For the bigger pipeline...

Command:
```
az ml job create -f bigger-train.yaml  -g <resource_group>  -w <workspace>
```

Expected Result:

Job running on compute cluster A100x4, spawning 6 process.

Actual Result:

Job running on compute cluster A100x4, spawning 4 process.
