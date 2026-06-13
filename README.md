# MovieFlix - AI-Powered Movie Recommendation System

A modern, next-generation Flask web application for personalized movie recommendations using machine learning. Built with a sleek UI, smooth animations, and responsive design.

## 🎬 Features

- **AI-Powered Recommendations**: Uses content-based filtering with cosine similarity
- **Beautiful UI**: Modern, gradient-based design with smooth animations
- **Mobile Responsive**: Works perfectly on desktop, tablet, and mobile devices
- **Real-time Suggestions**: Dynamic dropdown with instant movie suggestions
- **Rich Movie Details**: Display ratings, genres, release dates, and descriptions
- **Similarity Scores**: Shows how closely recommendations match your selection
- **Comparison Charts**: Visual representation of recommendation accuracy
- **Lightning Fast**: Instant recommendations using pre-computed similarity matrices

## 📋 Project Structure

```
movie-recommender/
├── app.py                          # Flask application backend
├── requirements.txt                # Python dependencies
├── model/
│   ├── movie_list.pkl             # Pickled movie dataframe
│   └── similarity.pkl             # Pickled similarity matrix
├── templates/
│   ├── base.html                  # Base template with navbar & footer
│   ├── index.html                 # Home page with search interface
│   └── recommendations.html       # Results page
├── static/
│   ├── css/
│   │   └── style.css              # Complete stylesheet with animations
│   ├── js/
│   │   └── script.js              # Frontend JavaScript utilities
│   └── images/                    # Optional: Store custom images
└── README.md                      # This file
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Git (optional)

### Installation

1. **Clone or download the project**
   ```bash
   git clone <repository-url>
   cd movie-recommender
   ```

2. **Create a virtual environment** (Recommended)
   ```bash
   # On Windows
   python -m venv venv
   venv\Scripts\activate

   # On macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Prepare your model files**
   - Ensure you have `model/movie_list.pkl` and `model/similarity.pkl` in the model directory
   - These files are generated from your Jupyter notebook using:
     ```python
     import pickle
     pickle.dump(new_df[['title', 'movie_id']], open('model/movie_list.pkl', 'wb'))
     pickle.dump(similar, open('model/similarity.pkl', 'wb'))
     ```

5. **Run the application**
   ```bash
   python app.py
   ```

6. **Open in browser**
   - Navigate to `http://localhost:5000`
   - Start searching for your favorite movies!

## 🎨 Design Features

### Modern UI Elements
- **Gradient Backgrounds**: Smooth color transitions throughout the app
- **Glassmorphism**: Frosted glass effect on cards and containers
- **Smooth Animations**: Every interaction has a polished transition
- **Dark Theme**: Easy on the eyes with vibrant accent colors
- **Floating Elements**: Subtle animations in the hero section

### Responsive Design
- Mobile-first approach
- Hamburger menu on small screens
- Flexible grid layouts
- Touch-friendly buttons and inputs

### Performance Optimized
- Lazy loading for images
- Caching for API requests
- Optimized CSS with CSS variables
- Minimal JavaScript dependencies

## 🔧 Configuration

### Environment Variables (Optional)

Create a `.env` file in the root directory:

```env
FLASK_ENV=development
FLASK_DEBUG=True
API_KEY=your_tmdb_api_key_here
```

### TMDB API Key

The app uses TMDB API to fetch movie posters and details. The default API key is included, but you can replace it:

```python
# In app.py, line 23
TMDB_API_KEY = "your_api_key_here"
```

Get your free API key from: https://www.themoviedb.org/settings/api

## 📱 Browser Compatibility

- ✅ Chrome (latest)
- ✅ Firefox (latest)
- ✅ Safari (latest)
- ✅ Edge (latest)
- ✅ Mobile browsers

## 🎯 How to Use

1. **Search for a Movie**
   - Type in the movie input field
   - See suggestions appear as you type
   - Click a suggestion or press Enter

2. **View Recommendations**
   - Click "Get Recommendations"
   - Wait for the system to find matches
   - See 5 most similar movies displayed

3. **Explore Details**
   - Click "View Details" on any movie card
   - See full description, rating, and genres
   - Check similarity score percentage

4. **Compare Recommendations**
   - Scroll down to see comparison chart
   - Visual representation of match accuracy
   - Find your next favorite movie!

## 🔍 Algorithm Details

The recommendation system uses:

1. **Content-Based Filtering**
   - Analyzes genres, keywords, cast, and crew
   - Creates feature vectors using CountVectorizer
   - Measures similarity using cosine similarity

2. **Similarity Calculation**
   - Cosine similarity between movie vectors
   - Scores range from 0 to 1 (0-100%)
   - Pre-computed for fast retrieval

3. **Recommendation Logic**
   - Sorts movies by similarity score
   - Returns top 5 recommendations
   - Displays with percentage match

## 📊 Data Sources

- **TMDB API**: Movie posters, ratings, descriptions
- **Dataset**: TMDB 5000 movies dataset
- **Processing**: Pandas, NumPy, Scikit-learn

## 🚀 Deployment Options

### Heroku Deployment

1. **Create Procfile**
   ```
   web: gunicorn app:app
   ```

2. **Create runtime.txt**
   ```
   python-3.10.12
   ```

3. **Deploy**
   ```bash
   heroku login
   heroku create your-app-name
   git push heroku main
   ```

### PythonAnywhere Deployment

1. Upload files to your account
2. Create web app with Flask
3. Point to app.py
4. Reload and visit your URL

### Railway Deployment

Similar to Heroku with minimal configuration needed.

### Docker Deployment

Create `Dockerfile`:
```dockerfile
FROM python:3.10-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

CMD ["gunicorn", "app:app"]
```

Build and run:
```bash
docker build -t movieflix .
docker run -p 5000:5000 movieflix
```

## 🛠️ Troubleshooting

### Models Not Loading
- Check if `model/movie_list.pkl` and `model/similarity.pkl` exist
- Verify file paths are correct
- Regenerate pickle files from your notebook

### TMDB API Issues
- Check internet connection
- Verify API key is correct
- Check if API rate limit exceeded
- Try using fallback posters

### Port Already in Use
```bash
# Change port in app.py
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5001)
```

Or kill the process:
```bash
# On Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# On macOS/Linux
lsof -i :5000
kill -9 <PID>
```

## 🔒 Security Considerations

- API keys stored in environment variables
- Input validation on all forms
- XSS protection through template escaping
- CSRF protection can be added with Flask-WTF
- Rate limiting recommended for production

## 📈 Performance Tips

1. **Cache Results**
   ```python
   @app.cache.cached(timeout=300)
   def get_movies():
       pass
   ```

2. **Load Balancing**
   - Use Gunicorn with multiple workers
   - Load balance with Nginx or HAProxy

3. **Database**
   - Cache similarity matrix in memory
   - Pre-compute recommendations

4. **CDN**
   - Serve static files from CDN
   - Use image optimization

## 🎓 Learning Resources

- Flask Documentation: https://flask.palletsprojects.com/
- Machine Learning: https://scikit-learn.org/
- TMDB API: https://www.themoviedb.org/settings/api
- Cosine Similarity: https://en.wikipedia.org/wiki/Cosine_similarity

## 📝 License

This project is open source and available under the MIT License.

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new features
- Submit pull requests
- Improve documentation

## 📧 Contact & Support

For questions or issues:
- Open an issue on GitHub
- Check the documentation
- Review the code comments

## 🎉 Acknowledgments

- TMDB for the movie database
- Flask community for the framework
- Scikit-learn for ML algorithms
- All contributors and users

---

**Made with ❤️ for movie lovers** 🎬

Happy watching! 🍿
#   m o v i e _ f l i x  
 