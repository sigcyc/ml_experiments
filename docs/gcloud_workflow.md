# Gcloud Workflow
This includes some knowledges on the google cloud

## GPU Background
The zone I'm currently on us-east1-d has NVIDIA L4, T4 gpus. NVIDIA T4 GPU is a descent GPU debutted in 2018. NVIDIA L4 is a very good gpu which I probably don't need at the moment.  

## Switching GPU
In order to save some money, I like to switch from my low cost machine to T4. Here are the steps
1. Shutdown the instance first.
2. Click on the instance, then clip `edit` at the top
3. Go to `Machine configuarion -> General purpose`, and switch the machine type to `N1`
4. Go to `Management -> On host maintenance`, swith the option to Terminate
5. Go to `Machine configuration -> GPUs`, add the GPU you like

## Login 
Run `gcloud compute ssh --zone "us-east1-d" "yichenc@instance-1" --project "arctic-kiln-391812" -- -X`

## Errors
1. Instances with guest accelerators do not support live migration.
We need to change the `On host maintenance` option in the `Management` session. The cheap E2 option only has the live migration option. So we need first switch it to  
