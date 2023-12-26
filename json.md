
`example1.json`

```json
{
    "name": "Sai arun yadav",
    "DOB": "17-11-1999",
    "City": "HYD",
    "Country": "India"
}    
```
{
    "name": "Sai arun yadav",
    "DOB": "17-11-1999",
    //this is address map,Inside map is everything is keyvalue pair
    "address": {
        "City": "HYD",
        "Country": "India"
    }
}
//How to make the list :- 
- Map is {}
- list is []

``````
{
    "name": "Sai arun yadav",
    "DOB": "17-11-1999",
    //this is address map,Inside map is everything is keyvalue pair
    "address": [
        {
            "City": "HYD",
            "Country": "India",
            "Type": "current"
        },
        {
            "City": "HYD",
            "Country": "India",
            "Type": "Perm"
        }
    ]
}