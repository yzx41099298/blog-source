title: "Activity being created twice, when back from camera Intent"
date: 2015-03-11 17:53:17
tags:
---

-  Android may choose to destroy an Activity that is waiting for the call to onActivityResult; especially when free memory is running low. Some devices appear more aggressive about destroying Activitys that are on the task stack. I can reliably recreate the issue on a Samsung device set to a debugging mode called "strict mode".

- You can verify whether this is your issue by logging calls to onCreate & onDestroy.

- In the case of a destroyed activity, when the activity result needs to be processed, Android will recreate the Activity, passing a savedInstanceState to onCreate. So, the remedy is to check the value of savedInstanceState in your GetImageActivity.onCreate. If it is not null then don't make any calls to startActivity because your Activity is being recreated to call onActivityResult.