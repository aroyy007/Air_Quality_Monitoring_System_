# API Documentation

This document provides a comprehensive overview of the API endpoints available in the project. The API is designed to handle sensor data, weather data, and email alerts.

## Base URL

The base URL for the API is:
```
http://localhost:<PORT>
```
Replace `<PORT>` with the value defined in your `.env` file (default is `5000`).

## Table of Contents

* [Authentication](#authentication)
* [Sensor Data Endpoints](#sensor-data-endpoints)
* [Weather Data Endpoints](#weather-data-endpoints)
* [Email Alerts Endpoints](#email-alerts-endpoints)
* [Error Handling](#error-handling)

## Authentication

No authentication is required for these endpoints. However, you can add authentication middleware if needed.

## Sensor Data Endpoints

### 1. Get Sensor Data

**Endpoint**: `/api/sensors`  
**Method**: `GET`  
**Description**: Fetch the latest sensor data from the database.

#### Request

No request body is required.

#### Response

```json
{
  "data": {
    "pm25": 12.5,
    "pm10": 25.3,
    "o3": 0.03,
    "co": 0.5,
    "so2": 0.02,
    "no2": 0.01,
    "nh3": 0.03,
    "temperature": 25.5,
    "humidity": 60,
    "aqi": 75
  }
}
```

#### Errors

* `500`: Internal Server Error

## Weather Data Endpoints

### 1. Get Weather Data

**Endpoint**: `/api/weather`  
**Method**: `GET`  
**Description**: Fetch weather data from the OpenWeatherMap API and merge it with sensor data.

#### Request

No request body is required.

#### Response

```json
{
  "data": {
    "temperature": 25.5,
    "humidity": 60,
    "pm25": 12.5,
    "pm10": 25.3,
    "o3": 0.03,
    "co": 0.5,
    "so2": 0.02,
    "no2": 0.01,
    "nh3": 0.03,
    "aqi": 75
  }
}
```

#### Errors

* `500`: Internal Server Error

## Email Alerts Endpoints

### 1. Subscribe to Email Alerts

**Endpoint**: `/api/alerts/subscribe`  
**Method**: `POST`  
**Description**: Subscribe to email alerts for air quality updates.

#### Request

```json
{
  "email": "user@example.com",
  "threshold": 100
}
```

#### Response

```json
{
  "message": "Subscription created successfully",
  "subscription": {
    "email": "user@example.com",
    "threshold": 100,
    "active": true
  }
}
```

#### Errors

* `400`: Email or threshold is missing
* `500`: Internal Server Error

### 2. Unsubscribe from Email Alerts

**Endpoint**: `/api/alerts/unsubscribe`  
**Method**: `POST`  
**Description**: Unsubscribe from email alerts.

#### Request

```json
{
  "email": "user@example.com"
}
```

#### Response

```json
{
  "message": "Unsubscribed successfully"
}
```

#### Errors

* `400`: Email is missing
* `404`: Subscription not found
* `500`: Internal Server Error

## Error Handling

All endpoints return errors in the following format:

```json
{
  "error": "Error message",
  "details": "Detailed error description (if available)"
}
```

### Common Errors

* `400`: Bad Request (e.g., missing required fields)
* `404`: Not Found (e.g., resource not found)
* `500`: Internal Server Error (e.g., database or server issues)

## Notes

* Ensure the `.env` file is properly configured with the required API keys and database connection string.
* The weather data is fetched using the OpenWeatherMap API. Make sure the `WEATHER_API_KEY` is set in the `.env` file.
* The email alerts functionality requires an email service API key. Ensure the `EMAIL_API_KEY` is set in the `.env` file.
