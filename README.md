# 🎬 Boolflix

**Boolflix** is a Vue.js web application that allows users to search for movies and TV series by integrating with the TMDB (The Movie Database) API. It provides users with detailed information, including posters, original titles, ratings, and country of origin.

## 📚 Table of Contents

- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Components](#components)
- [API Integration](#api-integration)
- [Future Improvements](#future-improvements)
- [Author](#author)

## 🚀 Features

- Search for movies and TV series by title.
- Display movie and TV series posters with details.
- Show average ratings as stars.
- Display country flags based on the original language of the movie or TV series.
- Responsive design.

## 🛠️ Technologies Used

- **Vue.js** for building the UI components.
- **Axios** for making HTTP requests to the TMDB API.
- **TMDB API** for fetching movie and TV series data.
- **FontAwesome** for star icons representing ratings.
- **Flag Icons** to display country flags based on language codes.
- **SCSS** for custom styling.

## 🛠️ Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/GulliWeb/Boolflix.git
   cd Boolflix

2. Install dependencies:
   ```bash
   npm install

3. Get a TMDB API Key:
   
	•	Go to the TMDB website and sign up for a free account.

	•	After signing in, navigate to your account’s API section to generate your personal API key.

	•	Create a .env file in the root directory of the project and add your TMDB API key like this:
    ```bash
    VUE_APP_TMDB_API_KEY=your_api_key_here

5. Run the application:
   ```bash
   npm run dev

6.	Open your browser at http://localhost:8080.

## 📹 Video Demo

Watch the Boolflix presentation video (https://vimeo.com/manage/videos/1017172613)

## 🎯 Usage

  1. Use the search bar to input the name of a movie or TV series.		
  
  2. Press Enter or click the search icon to trigger the search.

  3. Results will be displayed in a grid, showing the title, poster, rating, and country flag.

## 📦 Components

### **AppFilmCards.vue**
Responsible for rendering movie and TV series cards.

- **Props**:
  - `films` (Array): Array of film objects.
  - `tvSeries` (Array): Array of TV series objects.

- **Methods**:
  - `setFlag(lang)`: Returns the appropriate flag based on the language code.
  - `getIntVote(vote)`: Converts the vote to a value representing stars.

### **AppSearch.vue**
Handles the search input, API calls, and data binding to child components.

- **Methods**:
  - `apiCall()`: Makes an API call to TMDB for both movies and TV series based on user input.
  - `toggleSearch()`: Toggles the visibility of the search input.

## 🌐 API Integration

This project uses the TMDB API to fetch data for movies and TV series. The API endpoints used are:

  •	Movies: /search/movie
	•	TV Series: /search/tv

Make sure to sign up for an API key on TMDB and add it to your environment variables.

## 🚀 Future Improvements

- Add pagination to handle large result sets.
- Implement more detailed filters (e.g., genre, release year).
- Add a “load more” button for continuous scrolling.
- Improve the design with more animations and transitions.

## 👨‍💻 Author

- **GulliWeb**  
  Feel free to check out my [GitHub profile](https://github.com/GulliWeb) for more projects!

