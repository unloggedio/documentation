# What do we track?

Unlogged tracks a few things from the plugin. This is important for us to improve the developer experience and release better products.

Here are a few things we track.

### Your computer hostname

We track the hostname to get an approximate count of users and where each of those users may be stuck.

### SDK connected

When you start the application with ```unlogged-sdk``` we track an event, so that we know the user has progressed to the next step from installation.

### DIRECT Invoke

We track the name of the method invoked. 

!!! tip "Important" 
    We DO NOT track the variables fed to this method or the response returned by the method.

#### SDK Response Normal

We track this event in case the method successfully returned the necessary object, without any error.

#### SDK Response Exception

We track this event to know in case the method didn't return the necessary object or returned an exception.

### Unit Test Generated

We track this event, when a user generates unit test using the recorded data.

### Candidate Replayed

When a user replays a candidate, we track the button click.

### Replay Saved

When a user saves the replay in the form of a json, we track the event. 

!!! tip "Important" 
    We DO NOT track assertion rules, or variable names within the assertion rules or the assertion ```json``` itself.

### Mocks Injected

When a user injects mocks, enables or disables them, we track the event. 

!!! tip "Important" 
    We DO NOT track the mock maps or the lines for which mocks have been enabled/disabled.

### Replay Status

We track if the replay candidate is passing or failing. 

!!! tip "Important"
    In any case, we DON'T track your variable names, code blocks, or config files. None of these are uploaded over the internet. 

The plugin can work fully offline and none of these event tracking block the user.