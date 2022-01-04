# WorkManager
Work manager
Work Manager is basically a task scheduler, it makes it easy to specify the asynchronous task and when they should run. The Work Manager API helps create the task and hand it to the Work Manager to run immediately or at an appropriate time as mentioned
 Let’s understand what are various base classes that are used for Job Scheduling
	Worker
It specifies what task to perform, The Work Manager API include an abstract worker class and You need to extend this class and perform the work
	WorkRequest
WorkRequest represents an individual task that is to be performed. Now this WorkRequest, you can add values details for the work. Such as constraint or you can also add data while creating the request
WorkRequest can be of to type
•	OneTimeWorkRequest– That means you requesting for non-repetitive work.
•	PeriodicWorkRequest– This class is used for creating a request for repetitive work


	WorkInfo
WorkInfo contains the information about a particular task, The work manager provide live data for each of the work request objects, We can observe this and get the current status of the task.
1.	Add dependency
implementation "android.arch.work:work-runtime:1.0.0”
2.	Create WorkRequest
Create a WorkRequest to execute the work that we just created. Now first we will create Work Manager. This work manager will enqueue and manage our work reques
WorkManager mWorkManager = WorkManager.getInstance();
Now we will create OneTimeWorkRequest, because I want to create a task that will be executed just once.
OneTimeWorkRequest mRequest = new OneTimeWorkRequest.Builder(NotificationWorker.class).build();

3.	Enqueue the request with WorkManager
   mWorkManager.enqueue(mRequest);

4.	Fetch the particular task status
mWorkManager.getWorkInfoByIdLiveData(mRequest.getId()).observe(this,new Observer<WorkInfo>() {
            @Override
            public void onChanged(@Nullable WorkInfo workInfo) {
                if (workInfo != null) {
                    WorkInfo.State state = workInfo.getState();
                    tvStatus.append(state.toString() + "\n");
                }
            }
    });









