# CST8916 Final Project: Real-time Monitoring System for Rideau Canal Skateway

## Name: Kylath Mamman George

## Student Number: 041198835

## Overview

### Dashboard Features

This dashboard gives us visual representation of real-time data and past data (1-hour) from monitoring devices along the Rideau Canal. The system ingests data from the simulated devices into Azure IoT hub and processes it using Azure Stream Analytics which passes this data to be stored using Azure blob storage and also exposes them to this front-end dashboard using Azure Cosmos DB.

### Technologies used

- Node.js
- Javascript
- HTML
  
## Prerequisites

- Must have the whole data system set up before hand with live data in Azure Cosmos DB with correct matching fields for the query in Azure Stream Analytics.
  
## Installation

- Install Node.js and npm.
- In the main directory run:

    ```command
        npm install
        node server.js
    ```

## API Endpoints

**Note: I will be using localhost to show the examples below. To use the same endpoints with the Azure App Service you can add the end points to the end of the domain for your Azure App Service.**

1. `/api/latest` gets the latest readings for all locations

   Example request: `http://localhost:3000/api/latest`

   Example response:

   ```json
        {
            "success": true,
            "timestamp": "2025-12-09T23:09:13.960Z",
            "data": [
                {
                "windowEndTime": "2025-12-09T20:05:00.0000000Z",
                "location": "Dow's Lake",
                "avgIceThickness": 23.3306896551724,
                "minIceThickness": 10.06,
                "maxIceThickness": 43.37,
                "avgSurfaceTemperature": -10.5327586206897,
                "minSurfaceTemperature": -19.61,
                "maxSurfaceTemperature": 3.69,
                "maxSnowAccumulation": 49.08,
                "avgExternalTemp": -9.96724137931034,
                "readingCount": 29,
                "safetyStatus": "Unsafe",
                "id": "Dow's Lake-2025-12-09T20:05:00Z",
                "_rid": "FE1eALTbrdeNAgAAAAAAAA==",
                "_self": "dbs/FE1eAA==/colls/FE1eALTbrdc=/docs/FE1eALTbrdeNAgAAAAAAAA==/",
                "_etag": "\"26009052-0000-0a00-0000-693880ef0000\"",
                "_attachments": "attachments/",
                "_ts": 1765310703
                },
                {
                "windowEndTime": "2025-12-09T20:05:00.0000000Z",
                "location": "Fifth Avenue",
                "avgIceThickness": 29.0320689655172,
                "minIceThickness": 10.57,
                "maxIceThickness": 44.77,
                "avgSurfaceTemperature": -8.1951724137931,
                "minSurfaceTemperature": -18.87,
                "maxSurfaceTemperature": 4.99,
                "maxSnowAccumulation": 49.15,
                "avgExternalTemp": -7.95965517241379,
                "readingCount": 29,
                "safetyStatus": "Caution",
                "id": "Fifth Avenue-2025-12-09T20:05:00Z",
                "_rid": "FE1eALTbrdePAgAAAAAAAA==",
                "_self": "dbs/FE1eAA==/colls/FE1eALTbrdc=/docs/FE1eALTbrdePAgAAAAAAAA==/",
                "_etag": "\"26009252-0000-0a00-0000-693880ef0000\"",
                "_attachments": "attachments/",
                "_ts": 1765310703
                },
                {
                "windowEndTime": "2025-12-09T20:05:00.0000000Z",
                "location": "NAC",
                "avgIceThickness": 30.3155172413793,
                "minIceThickness": 10.09,
                "maxIceThickness": 44.34,
                "avgSurfaceTemperature": -6.5048275862069,
                "minSurfaceTemperature": -19.32,
                "maxSurfaceTemperature": 4.39,
                "maxSnowAccumulation": 48.98,
                "avgExternalTemp": -11.4431034482759,
                "readingCount": 29,
                "safetyStatus": "Safe",
                "id": "NAC-2025-12-09T20:05:00Z",
                "_rid": "FE1eALTbrdeOAgAAAAAAAA==",
                "_self": "dbs/FE1eAA==/colls/FE1eALTbrdc=/docs/FE1eALTbrdeOAgAAAAAAAA==/",
                "_etag": "\"26009152-0000-0a00-0000-693880ef0000\"",
                "_attachments": "attachments/",
                "_ts": 1765310703
                }
            ]
    }
   ```

2. `/api/history/:location` gets historical data for a specific location

    Example request: `http://localhost:3000/api/history/NAC`

    Example response: 

    ```json
        {
            "success": true,
            "location": "NAC",
            "data": [
                {
                "windowEndTime": "2025-12-09T07:55:00.0000000Z",
                "location": "NAC",
                "avgIceThickness": 26.5520689655172,
                "minIceThickness": 13.12,
                "maxIceThickness": 44.35,
                "avgSurfaceTemperature": -6.16448275862069,
                "minSurfaceTemperature": -19.99,
                "maxSurfaceTemperature": 4.45,
                "maxSnowAccumulation": 49.84,
                "avgExternalTemp": -8.38965517241379,
                "readingCount": 29,
                "safetyStatus": "Caution",
                "id": "NAC-2025-12-09T07:55:00Z",
                "_rid": "FE1eALTbrddtAgAAAAAAAA==",
                "_self": "dbs/FE1eAA==/colls/FE1eALTbrdc=/docs/FE1eALTbrddtAgAAAAAAAA==/",
                "_etag": "\"0a00c9d6-0000-0a00-0000-6937d5da0000\"",
                "_attachments": "attachments/",
                "_ts": 1765266906
                },
                {
                "windowEndTime": "2025-12-09T08:00:00.0000000Z",
                "location": "NAC",
                "avgIceThickness": 29.7362068965517,
                "minIceThickness": 10.76,
                "maxIceThickness": 42.77,
                "avgSurfaceTemperature": -8.34655172413793,
                "minSurfaceTemperature": -19.33,
                "maxSurfaceTemperature": 1.23,
                "maxSnowAccumulation": 45.71,
                "avgExternalTemp": -8.02275862068966,
                "readingCount": 29,
                "safetyStatus": "Caution",
                "id": "NAC-2025-12-09T08:00:00Z",
                "_rid": "FE1eALTbrddwAgAAAAAAAA==",
                "_self": "dbs/FE1eAA==/colls/FE1eALTbrdc=/docs/FE1eALTbrddwAgAAAAAAAA==/",
                "_etag": "\"0b007702-0000-0a00-0000-6937d7060000\"",
                "_attachments": "attachments/",
                "_ts": 1765267206
                }
            ]
        }
    ```

3. `/api/status` gets the overall safety status

    Example request: `http://localhost:3000/api/status`

    Example response:

    ```json
        {
            "success": true,
            "overallStatus": "Unsafe",
            "locations": [
                {
                "location": "Dow's Lake",
                "safetyStatus": "Unsafe",
                "windowEndTime": "2025-12-09T20:05:00.0000000Z"
                },
                {
                "location": "Fifth Avenue",
                "safetyStatus": "Caution",
                "windowEndTime": "2025-12-09T20:05:00.0000000Z"
                },
                {
                "location": "NAC",
                "safetyStatus": "Safe",
                "windowEndTime": "2025-12-09T20:05:00.0000000Z"
                }
            ]
        }
    ```

4. `/api/all` gets all the data

   Example request: `http://localhost:3000/api/all`

   Example response: 

