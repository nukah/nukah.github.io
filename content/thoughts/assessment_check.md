---
title: "Assessment check example"
date: 2023-02-19T14:53:34+06:00
tldr: Example of assessment story
---

## Brief

Example of backend software developer assessement test that can be completed within few hours.

It consists of few crucial points:
- API Generation
- Algorithmical work with geospatial data
- Caching strategy

<!--more-->

## Description

We have a database storing information about ATMs and their locations.
Data structure is defined in the following format:

| Name | ID | Latitude | Longitude |
|:--|:--|:--|:--|
| VTB Mayakovskaya | VTB_M | 55.770935 | 37.596461 |
| Otkritie Yuzhnaya | OPEN_SOUTH | 55.621701 | 37.610418 |
| Sberbank Tverskaya | SBER_TVER | 55.763507 | 37.605967 |
| Pochta Marksistskaya | POCHTA_MARKS | 55.738556 | 37.661429 |

## Goal
The task is to create an application with API of the following format

```
method: GET
path: /atms
params:
	lat (float)
	long (float)
	rad (int)
```


response:
```json
{
  data:[
    { "code": "VTB_M", name: "VTB Mayakovskaya", lat: 55.770935, long: 37.596461 },
      ...
  ]
}
```

Input:
- current coordinates of the client (lat, long)
- search radius (in meters)

The output shows the nearest ATMs in this radius.

## Supplementary goal

Assume that access to ATM data source is an external call, with limit on number of requests.

Since ATMs are static and only the user's position changes, a situation may arise when two users, not far from each, other make a request.

For each customer request, a cached response is required so that if another nearby customer makes a request, the response from the cache will follow instead of a new external request.
