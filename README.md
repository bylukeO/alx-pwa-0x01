# alx-project-0x14

## API Overview

The MoviesDatabase API is a comprehensive RESTful web service that provides access to an extensive collection of movie, TV show, and entertainment industry data. This API offers complete and updated information for over 9 million titles including movies, TV series, and individual episodes, along with detailed profiles for more than 11 million actors, directors, writers, and crew members. The API includes rich metadata such as YouTube trailer URLs, award information, full biographies, plot summaries, ratings, release dates, genres, and cast details, making it an ideal solution for developers building entertainment applications, movie discovery platforms, or content recommendation systems.

## Version

API Version: Latest (Current version as available on RapidAPI platform)
Base URL: `https://moviesdatabase.p.rapidapi.com`

## Available Endpoints

- **GET /titles** - Retrieve multiple titles with filtering and sorting options based on various lists and categories
- **GET /titles/{id}** - Get detailed information for a specific title using its unique identifier
- **GET /titles/search/title/{title}** - Search for titles by name with optional exact matching
- **GET /titles/x/titles-by-ids** - Fetch multiple titles using a list of specific title IDs
- **GET /titles/{id}/episodes** - Retrieve all episodes for a specific TV series in ascending order
- **GET /titles/{id}/episodes/{season}** - Get episodes for a specific season of a TV series
- **GET /titles/utils/genres** - Retrieve available genre categories for filtering
- **GET /titles/utils/lists** - Get available title lists and collections
- **GET /actors** - Retrieve multiple actor profiles with filtering options
- **GET /actors/{id}** - Get detailed information for a specific actor using their unique identifier
- **GET /actors/search/name/{name}** - Search for actors by name

## Request and Response Format

### Request Structure
All API requests require specific headers for authentication and should follow this format:

```
GET https://moviesdatabase.p.rapidapi.com/endpoint
Headers:
  X-RapidAPI-Key: your_api_key_here
  X-RapidAPI-Host: moviesdatabase.p.rapidapi.com
```

### Query Parameters
Most endpoints accept optional query parameters:
- `info`: Specifies additional information to include in response
- `list`: Defines the collection/category to query from
- `page`: Page number for pagination (default: 1)
- `limit`: Number of results per page
- `exact`: Boolean for exact name matching in search endpoints

### Response Structure
All endpoints return a JSON object with a consistent structure:

```json
{
  "page": 1,
  "next": "string_url_for_next_page",
  "entries": 50,
  "results": [
    {
      "id": "tt0111161",
      "titleText": {
        "text": "The Shawshank Redemption"
      },
      "titleType": {
        "text": "Movie"
      },
      "releaseYear": {
        "year": 1994
      },
      "genres": {
        "genres": [
          {
            "text": "Drama"
          }
        ]
      },
      "primaryImage": {
        "url": "https://example.com/image.jpg",
        "width": 1000,
        "height": 1500
      },
      "ratingsSummary": {
        "aggregateRating": 9.3,
        "voteCount": 2500000
      },
      "runtime": {
        "seconds": 8520
      },
      "plot": {
        "text": "Plot summary text"
      }
    }
  ]
}
```

## Authentication

The MoviesDatabase API uses RapidAPI's authentication system requiring two specific headers:

### Required Headers
- **X-RapidAPI-Key**: Your personal API key obtained from RapidAPI subscription
- **X-RapidAPI-Host**: Must be set to `moviesdatabase.p.rapidapi.com`

### Getting API Access
1. Create an account on RapidAPI platform
2. Subscribe to the MoviesDatabase API
3. Copy your unique API key from the RapidAPI dashboard
4. Include the required headers in every API request

### Example Authentication
```javascript
const headers = {
  'X-RapidAPI-Key': 'your_api_key_here',
  'X-RapidAPI-Host': 'moviesdatabase.p.rapidapi.com'
};
```

## Error Handling

The API returns standard HTTP status codes to indicate request success or failure:

### Common HTTP Status Codes
- **200 OK**: Request successful, data returned
- **400 Bad Request**: Invalid request parameters or malformed query
- **401 Unauthorized**: Missing or invalid API key
- **403 Forbidden**: API key valid but quota exceeded or access denied
- **404 Not Found**: Requested resource does not exist
- **429 Too Many Requests**: Rate limit exceeded, slow down requests
- **500 Internal Server Error**: Server-side error, try again later

### Error Response Format
```json
{
  "error": {
    "code": 401,
    "message": "Unauthorized access. Please check your API key.",
    "details": "Additional error information if available"
  }
}
```

### Error Handling Best Practices
- Always check HTTP status codes before processing responses
- Implement retry logic with exponential backoff for 429 and 5xx errors
- Validate API key and headers for 401/403 errors
- Log errors for debugging while avoiding exposure of sensitive information
- Provide user-friendly error messages in your application

## Usage Limits and Best Practices

### Rate Limits
- Rate limits vary by subscription plan (Free, Pro, Ultra, Mega)
- Typical limits range from 100 to 10,000 requests per month
- Monitor usage in RapidAPI dashboard to avoid quota exceeded errors
- Implement request queuing and throttling in high-volume applications

### Best Practices
- **Caching**: Store frequently accessed data locally to reduce API calls
- **Pagination**: Handle paginated responses properly using 'next' field
- **Error Handling**: Implement robust error handling with appropriate retry mechanisms
- **API Key Security**: Store API keys in environment variables, never in source code
- **Request Optimization**: Use specific 'info' parameters to request only needed data
- **Batch Requests**: Use bulk endpoints like `/titles/x/titles-by-ids` when fetching multiple items
- **Rate Limiting**: Implement client-side rate limiting to stay within quota
- **Monitoring**: Track API usage and performance metrics
- **Timeout Handling**: Set appropriate request timeouts for network reliability
