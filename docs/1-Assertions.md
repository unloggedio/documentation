# Defining Assertions & Saving

You can save the replays in the form of Atomic Tests. 

The Atomic Tests are in the form of a json artifact. Here is how one Atomic Test looks like.

```json
{
  "classname" : "org.zerhusen.service.GCDService",
  "storedCandidateMap" : {
    "gcdOfTwoNumbers#(II)Lorg/zerhusen/service/MessageDto;" : [ {
      "testAssertions" : {
        "subAssertions" : [ {
          "subAssertions" : null,
          "expression" : "SELF",
          "expectedValue" : "",
          "id" : "b7e6cf63-ea67-4498-b88f-3a2215e37ae4",
          "assertionType" : "EQUAL",
          "key" : "root"
        } ],
        "expression" : "SELF",
        "expectedValue" : null,
        "id" : "27b52945-2b11-4d20-bad7-6ce52b1a9e3e",
        "assertionType" : "ALLOF",
        "key" : null
      },
      "candidateId" : "7adad67c-8c99-4786-b400-f09bfc1f66ba",
      "name" : "case number 25",
      "description" : "description for case # 25",
      "methodArguments" : [ "25", "30" ],
      "returnValue" : "{\"gcd\":5,\"weather\":{\"location\":{\"name\":\"Mumbai\",\"region\":\"Maharashtra\",\"country\":\"India\",\"lat\":18.98,\"lon\":72.83,\"tz_id\":\"Asia/Kolkata\",\"localtime_epoch\":1690291007,\"localtime\":\"2023-07-25 18:46\"},\"current\":{\"temp_c\":27.0,\"temp_f\":80.6,\"is_day\":1,\"condition\":{\"text\":\"Light rain\",\"icon\":\"//cdn.weatherapi.com/weather/64x64/day/296.png\",\"code\":1183},\"wind_mph\":12.5,\"wind_kph\":20.2,\"wind_degree\":280,\"wind_dir\":\"W\",\"pressure_mb\":1005.0,\"pressure_in\":29.68,\"precip_mm\":3.5,\"precip_in\":0.14,\"humidity\":100,\"cloud\":100,\"feelslike_c\":31.8,\"feelslike_f\":89.3,\"vis_km\":2.1,\"vis_miles\":1.0,\"uv\":6.0,\"gust_mph\":22.4,\"gust_kph\":36.0}}}",
      "returnValueClassname" : "org.zerhusen.service.MessageDto",
      "metadata" : {
        "recordedBy" : "shardul",
        "hostMachineName" : "shardul",
        "timestamp" : 1690291012869,
        "candidateStatus" : "PASSING"
      },
      "entryProbeIndex" : 84757955,
      "probSerializedValue" : "eyJnY2QiOjUsIndlYXRoZXIiOnsibG9jYXRpb24iOnsibmFtZSI6Ik11bWJhaSIsInJlZ2lvbiI6Ik1haGFyYXNodHJhIiwiY291bnRyeSI6IkluZGlhIiwibGF0IjoxOC45OCwibG9uIjo3Mi44MywidHpfaWQiOiJBc2lhL0tvbGthdGEiLCJsb2NhbHRpbWVfZXBvY2giOjE2OTAyOTEwMDcsImxvY2FsdGltZSI6IjIwMjMtMDctMjUgMTg6NDYifSwiY3VycmVudCI6eyJ0ZW1wX2MiOjI3LjAsInRlbXBfZiI6ODAuNiwiaXNfZGF5IjoxLCJjb25kaXRpb24iOnsidGV4dCI6IkxpZ2h0IHJhaW4iLCJpY29uIjoiLy9jZG4ud2VhdGhlcmFwaS5jb20vd2VhdGhlci82NHg2NC9kYXkvMjk2LnBuZyIsImNvZGUiOjExODN9LCJ3aW5kX21waCI6MTIuNSwid2luZF9rcGgiOjIwLjIsIndpbmRfZGVncmVlIjoyODAsIndpbmRfZGlyIjoiVyIsInByZXNzdXJlX21iIjoxMDA1LjAsInByZXNzdXJlX2luIjoyOS42OCwicHJlY2lwX21tIjozLjUsInByZWNpcF9pbiI6MC4xNCwiaHVtaWRpdHkiOjEwMCwiY2xvdWQiOjEwMCwiZmVlbHNsaWtlX2MiOjMxLjgsImZlZWxzbGlrZV9mIjo4OS4zLCJ2aXNfa20iOjIuMSwidmlzX21pbGVzIjoxLjAsInV2Ijo2LjAsImd1c3RfbXBoIjoyMi40LCJndXN0X2twaCI6MzYuMH19fQ==",
      "exception" : false,
      "method" : {
        "name" : "gcdOfTwoNumbers",
        "signature" : "(II)Lorg/zerhusen/service/MessageDto;",
        "className" : "org.zerhusen.service.GCDService",
        "methodHash" : -1398852981
      }
    } ]
  }
}

```

These tests will be saved inside your project directory in the below location.

```/YOUR PROJECT DIRECTORY/src/test/resources/unlogged```

You can commit these cases in git and your team mates can pull them and run locally.

#### Default

By default, Unlogged compares the 2 return values before and after the code change.

#### Custom

From the release 1.16.22 onwards, you will have the option to define custom assertions all the way down to key level, combining multiple assertions with ```AND``` ```OR``` & ```NOT``` operators, and saving them to git. 

Here is how custom assertions will look like.

![](assets/images/assertion.png)
