# Saving Candidates

## What's a Candidate? 

When you execute a method using ```Direct Invoke``` or through an http endpoint, you will see the method input values that can be replayed. 

Each unique combination of input and return value is called a Candidate.

!!! tip 
    By default, when you replay a candidate, Unlogged compares the return value object down to the key level. 

But return value may contain ever changing or irrelevant fields such as timestamp. That's where Assertions come in picture.

## Creating Assertions

When you click on **Save Replay** - you will see a window that presents the recorded value of the object for the candidate we just replayed.  

![](assets/images/assertion.gif)

## Defining Assertions

You can define any assertion on this return value, down to any key/value pair. You can define nested assertions with ```AND``` ```OR``` ```NOT``` on different key-value pairs and **group them together**. 

### List of Operators

You can see the following operators available in the dropdown.

- [x] is
- [x] size is
- [x] length is
- [x] equals ignore case
- [x] is not
- [x] size is not
- [x] length is not
- [x] is false
- [x] matches regex
- [x] not matches regex
- [x] is true
- [x] <
- [x] <=
- [x] >
- [x] >=
- [x] is not null
- [x] is null
- [x] is empty
- [x] is not empty
- [x] contains key in object
- [x] contains item in array
- [x] not contains item in array
- [x] contains substring
- [x] not contains key in object
- [x] not contains substring

![](assets/images/defineassertion.gif)

!!! tip
    Green background color means passing assertion and red means failing assertion. 



## Saving the Replays

Replays with assertions are saved at the below location

```/YOUR MODULE DIRECTORY/src/test/resources/unlogged```

![](assets/images/savelocation.png)

!!! nodifference "Replaying with Assertions"
    For your code change, when you replay the candidate, Unlogged will execute the assertion you just saved and inform if the candidate passes or fails the assertions.

## Collaborate

You can now push these replays to your git repository, so that your team members can pull and replay locally for their code changes.