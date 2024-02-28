# AZSynapseNotebookInstallWheel
how to install a Python wheel file within AZ Synapse notebooks
## Instructions
1. Build wheel file for distribution
2. Upload wheel file to ADLS location that your notebook has access to.
3. Create a linked service to your ADLS storage (if you don't already have one)
4. Using `mssparkutils.fs.mount`, mount the linked service to your notebook session:
  `mssparkutils.fs.mount( 
      "abfss://yourdatalake@datalakeid.dfs.core.windows.net", 
      "/my_linked_svc", 
      {"LinkedService":"my_linked_svc"} # linked service name must match the service name you created (e.g. "my_linked_svc")
  )`
5. Get the job_id of the mounted linked services via `job_id = mssparkutils.env.getJobId()`
6. Use the `%pip` magic command to install the wheel file into your environment:
   `%pip install /synfs/{job_id}/my_linked_svc/path_to_wheel.whl`
7. import the module like any other python module using `import <module_name>`
