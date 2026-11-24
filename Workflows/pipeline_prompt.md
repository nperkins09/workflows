# Claude Prompt for creating pipelines

## Requirements

- Target Data Source Documentation
- Claude.md
- Pipeline_claude.md

## Outcomes

- A python script that ELT's the target data source into a snowflake database
  - collects metrics and uploads the data set to a metrics focuses data table in snowflake
  - collects the data from the target source into a bronze layer data table in snowflake
  - uses github actions to run on a scheduled basis.

## Prompt

Create a python repo (pipeline) that connects to <data-source-url> and ELT's the data from the source into a pandas dataframe.
I want the repo to upload the dataframe into a snowflake bronze layer data table. I also want the pipeline repo to follow the pipeline_claude.md, 
collect the metrics through pipeline runtime and upload the metrics to the snowflake MONITORING.HISTORY.PIPELINE_RUN_HISTORY regardless if the
pipeline was run successfully or not. This pipeline is to be run via github actions.