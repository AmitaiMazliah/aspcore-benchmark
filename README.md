# ASP core controllers vs. minimal api

This is a small benchmark of asp core controllers api vs. minimal api

## Projects

There are 2 projects in the solution

1. WebApplicationNormal which is the template asp core web api project using controllers api
2. WebApplicationMinimal which is the template asp core web api project using minimal api

## Usage

The load testing is using a tool called [Locust]("https://locust.io/")
Follow the [Guide]("https://docs.locust.io/en/stable/installation.html") to install it

After installation run each of the webs using dotnet cli or any IDE
And call locust to start the load test using the following command
```python
locust --headless -u 100 -r 20 -t 5m --only-summary -H http://localhost:5131
```

The host should be changed to the port you chose for your application
After 5 minutes locust will print the results to the console

## My results
Using Contrllers api
```
Type     Name                                                                          # reqs      # fails |    Avg     Min     Max    Med |   req/s  failures/s
--------|----------------------------------------------------------------------------|-------|-------------|-------|-------|-------|-------|--------|-----------
GET      /WeatherForecast                                                               13062     0(0.00%) |   1115      49   15932   1100 |   87.81        0.00
--------|----------------------------------------------------------------------------|-------|-------------|-------|-------|-------|-------|--------|-----------
         Aggregated                                                                     13062     0(0.00%) |   1115      49   15932   1100 |   87.81        0.00

Response time percentiles (approximated)
Type     Name                                                                                  50%    66%    75%    80%    90%    95%    98%    99%  99.9% 99.99%   100% # reqs
--------|--------------------------------------------------------------------------------|--------|------|------|------|------|------|------|------|------|------|------|------
GET      /WeatherForecast                                                                     1100   1200   1200   1300   1500   1700   1900   2100  14000  16000  16000  13062
--------|--------------------------------------------------------------------------------|--------|------|------|------|------|------|------|------|------|------|------|------
         Aggregated                                                                           1100   1200   1200   1300   1500   1700   1900   2100  14000  16000  16000  13062
```

Using minimal api
```
Type     Name                                                                          # reqs      # fails |    Avg     Min     Max    Med |   req/s  failures/s
--------|----------------------------------------------------------------------------|-------|-------------|-------|-------|-------|-------|--------|-----------
GET      /WeatherForecast                                                              375928     0(0.00%) |     62       7     332     60 | 1255.92        0.00
--------|----------------------------------------------------------------------------|-------|-------------|-------|-------|-------|-------|--------|-----------
         Aggregated                                                                    375928     0(0.00%) |     62       7     332     60 | 1255.92        0.00

Response time percentiles (approximated)
Type     Name                                                                                  50%    66%    75%    80%    90%    95%    98%    99%  99.9% 99.99%   100% # reqs
--------|--------------------------------------------------------------------------------|--------|------|------|------|------|------|------|------|------|------|------|------
GET      /WeatherForecast                                                                       60     65     69     71     79     87    100    110    190    240    330 375928
--------|--------------------------------------------------------------------------------|--------|------|------|------|------|------|------|------|------|------|------|------
         Aggregated                                                                             60     65     69     71     79     87    100    110    190    240    330 375928
```
